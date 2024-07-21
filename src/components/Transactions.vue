<template>
	<TransactionsTable :data="intilizedData.transactions" />
	<TransactionsGraph :data="intilizedData.customers"/>
</template>

<script setup>
	import { computed } from 'vue';
	import TransactionsTable from './TransactionsTable.vue';
	import TransactionsGraph from './TransactionsGraph.vue';

	let customersResponse = await fetch('http://localhost:3000/customers'); 
    let transactionsResponse = await fetch('http://localhost:3000/transactions'); 
  
    let customersData = await customersResponse.json(); 
    let transactionsData = await transactionsResponse.json(); 

	const intilizedData = computed(() => {
		return {
			transactions: transactionsData.map(t => {
				t.customer = customersData.find(c => {
					return c.id === t.customer_id
				});
				return t;
			}),
			customers: customersData.map(c => {
				c.transactions = transactionsData.filter(t => {
					return t.customer_id === c.id
				});
				return c;
			}),
		}
	});

</script>