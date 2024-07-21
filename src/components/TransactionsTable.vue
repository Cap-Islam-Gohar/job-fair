<template>
    <Card>
        <template #card-title>
            <h1 class="text-lg font-bold leading-6 text-gray-900">Transactions</h1>
            <p class="mt-2 text-sm text-gray-700">Transactions table which diplay all transactions data with customer info</p>
        </template>

        <template #card-option>
            <Search @change-filter="onChangeFilter"></Search>
        </template>

        <template #card-body>
            <Table :show="filteredTransactions">

                <template #thead>
                    <th class="whitespace-nowrap text-left text-sm font-semibold">#Id</th>
                    <th class="whitespace-nowrap p-4 text-left text-sm font-semibold">Customer</th>
                    <th class="whitespace-nowrap p-4 text-left text-sm font-semibold">Amount</th>
                    <th class="whitespace-nowrap p-4 text-left text-sm font-semibold">Data</th>
                </template>

                <template v-if="filteredTransactions.length" #tbody>
                    <tr v-for="(item, index) in filteredTransactions" :key="`row-${index}`">
                        <td class="whitespace-nowrap text-sm font-medium text-gray-500">{{ item.id }}</td>
                        <td class="whitespace-nowrap p-4 text-sm font-medium text-gray-800">{{ item.customer.name }}</td>
                        <td class="whitespace-nowrap p-4 text-sm text-green-500">{{ item.amount.toFixed(2) }}</td>
                        <td class="whitespace-nowrap p-4 text-sm text-gray-500">{{ item.date }}</td>
                    </tr>
                </template>

                <template v-else="filteredTransactions.length === 0" #tfoot>
                    No Data Founded
                </template>
            </Table>
        </template>
    </Card>

</template>

<script setup>
    import { computed, ref } from 'vue';
    import Card from './Card.vue';
    import Table from './Table.vue';
    import Search from './Search.vue';

    const props = defineProps({
        data: Object,
    });

    const transactions = computed(() => {
        return props.data;
    });

    const filter = ref({
        query: "",
        column: "customer",
    });

    //return object with filter params
    const onChangeFilter = (details) => {
        filter.value = details || {
            query: "",
            column: "customer"
        };
    }    

    const filteredTransactions = computed(() => {
        // if no filter
        if(filter.value.query === ""){
            return transactions.value;
        }

        //if user write somthing
        return transactions.value.filter(t => {
            if(filter.value.column === "Amount"){
                return t.amount.toString().includes(filter.value.query);
            }else{
                return t.customer.name.toLowerCase().startsWith(filter.value.query.toLowerCase());
            }
        });
    });

</script>