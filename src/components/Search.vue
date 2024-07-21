<template>
    <label for="search" class="hidden sm:block text-sm font-medium leading-6 text-gray-900">Search</label>
    <div class="relative sm:mt-2 rounded-md shadow-sm">
        <div class="pointer-events-none absolute inset-y-0 left-0 flex items-center px-2">
            <span class="text-gray-500 sm:text-sm">
                <svg class="w-4 h-4" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24"
                    stroke-width="1.5" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round"
                        d="m21 21-5.197-5.197m0 0A7.5 7.5 0 1 0 5.196 5.196a7.5 7.5 0 0 0 10.607 10.607Z" />
                </svg>
            </span>
        </div>
        <input v-model="search.query" type="text" id="search"
            class="block w-full rounded-md border-0 py-1.5 pl-7 pr-24 text-sm leading-6 text-gray-900 ring-1 ring-inset ring-gray-300 placeholder:text-gray-400 focus:ring-2 focus:ring-inset focus:ring-indigo-600"
            placeholder="Search">
        <div class="absolute inset-y-0 right-0 flex items-center">
            <label for="column" class="sr-only">Column</label>
            <select id="column" v-model="search.column"
                class="h-full text-xs sm:text-sm pl-1 pr-6 sm:pr-7 rounded-md border-0 bg-transparent text-gray-500 focus:ring-2 focus:ring-inset focus:ring-indigo-600">
                <option value="customer" class="text-xs sm:text-sm">Customer</option>
                <option value="Amount" class="text-xs sm:text-sm">Amount</option>
            </select>
        </div>
    </div>
</template>

<script setup>
    import { ref, watch } from 'vue';


    const search = ref({
        query: "",
        column: "customer",
    });

    const emits = defineEmits(['changeFilter']);

    watch( search, (search) => {
        emits('changeFilter', search);
    },{ 
        deep: true ,
        immediate: true
    });


</script>