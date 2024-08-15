<script setup>
defineProps({
    income: {
        type: Number,
        required: true,
    },
    expenses: {
        type: Number,
        required: true,
    },
});
</script>


<template>
    <div class="flex justify-around items-center px-2 py-4 bg-white shadow-md border border-gray-100 rounded-md ">
        <div>
            <h4 class="font-semibold">Income</h4>
            <p class="text-green-600">+${{ income }}</p>
        </div>
        <div class="w-px h-10 bg-slate-200"></div>
        <div>
            <h4 class="font-semibold">Expense</h4>
            <p class="text-red-400">-${{ expenses }}</p>
        </div>
    </div>
</template>