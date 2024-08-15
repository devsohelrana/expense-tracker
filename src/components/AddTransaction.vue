<script setup>
import { ref } from 'vue';
import { toast } from 'vue3-toastify';

const text = ref('');
const amount = ref('');

const emit = defineEmits(['transactionSubmitted']);

const onSubmit = () => {

    if (!text.value || !amount.value) {
        toast.error("Both fields must be filled! ", {
            position: toast.POSITION.BOTTOM_RIGHT,
            autoClose: 5000,
        });
        return;
    }

    const transactionData = {
        text: text.value,
        amount: parseFloat(amount.value)
    }

    emit('transactionSubmitted', transactionData);

    text.value = '';
    amount.value = '';
};
</script>

<template>
    <h3 class="text-xl font-semibold">Add new transaction</h3>
    <div class="w-full h-px bg-gray-200 my-3"></div>
    <form @submit.prevent="onSubmit">
        <div class="space-y-4">
            <div class="flex flex-col">
                <label class="text-md font-semibold" for="text">Name Income or Expenses</label>
                <input id="text" v-model="text" class="w-full border shadow-md p-2 rounded-md focus:outline-none"
                    type="text" placeholder="Name Income or Expenses" autofocus>
            </div>
            <div class="flex flex-col">
                <label class="text-md font-semibold" for="amount">
                    Amount
                </label>
                <input id="amount" v-model="amount" class="w-full border shadow-md p-2 rounded-md focus:outline-none"
                    type="text" placeholder="Enter amount">

                <span class="text-sm my-1"><span class="text-green-500">Positive</span> - income, <span
                        class="text-red-500">Negative</span>
                    -
                    expense</span>
            </div>
            <button
                class="w-full bg-purple-600 py-2 rounded-md text-white focus:ring focus:ring-offset-1 ring-purple-400">Add
                transaction</button>
        </div>
    </form>
</template>