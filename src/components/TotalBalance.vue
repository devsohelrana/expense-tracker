<script setup>
defineProps({
    total: {
        type: Number,
        required: true,
    },
});
</script>

<template>
    <div class="text-center">
        <h4 class="font-semibold">Your Main Balance</h4>
        <h1 class="text-2xl font-bold text-dark">${{ total }}</h1>
    </div>
</template>