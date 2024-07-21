<template>
    <Cart>
        <template #card-title>
            <h1 class="text-lg font-bold leading-6 text-gray-900">Customer Chart</h1>
            <p class="mt-2 text-sm text-gray-700">This Chart diplay transactions data for customer per day</p>
        </template>

        <template #card-option>
            <label for="search-customer" class="block text-sm font-medium leading-6 text-gray-900">Select Customer</label>
            <div class="my-3">
                <select id="search-customer" v-model="customerId" class="block w-full rounded-md border-0 py-1.5 text-gray-900 shadow-sm ring-1 ring-inset ring-gray-300 focus:ring-2 focus:ring-inset focus:ring-indigo-600 sm:max-w-xs sm:text-sm sm:leading-6">
                    <option v-for="(customer, index) in customers" :key="`customer${index}`" :value="customer.id" class="text-xs sm:text-sm">{{
                customer.name }}</option>
                </select>
            </div>
        </template>

        <template #card-body>
            <VueApexCharts width="100%" height="350" :options="options" :series="series" />
        </template>
    </Cart>
</template>
  
<script setup>
import { ref, computed } from 'vue';
import Cart from './Card.vue';
import VueApexCharts from 'vue3-apexcharts';

const props = defineProps({
    data: Object,
});

const customers = computed(() => {
    return props.data;
});

const customerId = ref(1);

const transactions = computed(() => {
    return customers.value.find(c => c.id === customerId.value).transactions ?? [];
});

const series = computed(() => {
    return [{
        name: 'transaction Amount',
        type: 'line',
        data: transactions.value.map(t => t.amount)
    }]
});

const options = computed(() => {
    return {
        chart: {
            width: "100%",
            type: "area",
            animations: {
                initialAnimation: {
                    enabled: false
                }
            }
        },
        xaxis: {
            type: "datetime",
            categories: transactions.value.map(t => t.date),
        },
        zoom: {
            type: 'x',
            enabled: true,
            autoScaleYaxis: true
        },
        toolbar: {
            autoSelected: 'zoom'
        }
    };
});

// const months = ["Jan", "Feb", "Mar", "Apr", "May", "Jun", "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"];
// const labels = transactions.value.map(t => {
//     let date = new Date(value);
//     return `${months[date.getMonth()]} ${date.getDate()}`
// });
// const dataset = transactions.value.map(t => t.amount);

</script>
  