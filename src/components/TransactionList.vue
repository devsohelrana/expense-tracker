<script setup>
const emit = defineEmits(['transactionDeleted'])

defineProps({
    transactions: {
        type: Object,
        required: true,
    },
});

const deleteTransaction = (id) => {
    emit('transactionDeleted', id);
}
</script>

<template>
    <h3 class="text-xl font-semibold">History</h3>

    <div class="w-full h-px bg-gray-200 my-3"></div>

    <ul class="w-full space-y-4">
        <li v-for="transaction in transactions" :key="transaction.id"
            class="w-full grid grid-cols-[1fr_20px] items-center gap-2 border p-2 border-r-2 rounded-md"
            :class="transaction.amount < 0 ? 'border-r-red-500' : 'border-r-green-500'">
            <div class="flex justify-between">
                {{ transaction.text }}
                <span class="font-semibold">$ {{ transaction.amount }}</span>
            </div>
            <button @click="deleteTransaction(transaction.id)"
                class="bg-red-400 w-5 h-5 rounded-full text-white text-sm flex justify-center items-center">
                <svg aria-hidden="true" viewBox="0 0 14 16" class="h-4 w-4 fill-white">
                    <path fill-rule="evenodd"
                        d="M7.71 8.23l3.75 3.75-1.48 1.48-3.75-3.75-3.75 3.75L1 11.98l3.75-3.75L1 4.48 2.48 3l3.75 3.75L9.98 3l1.48 1.48-3.75 3.75z">
                    </path>
                </svg>
            </button>
        </li>
    </ul>
</template>
