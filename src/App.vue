

<template>

	<Suspense>

		<Transactions />

		<template #fallback>
			...Loading
		</template>

	</Suspense>
</template>

<script setup>
import Transactions from './components/Transactions.vue';
</script>

