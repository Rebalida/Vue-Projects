<template>
    <h4>
        Your Balance
    </h4>
    <h1 id="balance">₱{{ total }}</h1>
</template>

<script setup>

    import { defineProps } from 'vue';

    const props = defineProps({
        total: {
            type: Number,
            required: true,
        },
    });

</script>

<style scoped>

h4 {
    margin: 0;
    text-transform: uppercase;
}

h1 {
    letter-spacing: 1px;
    margin: 0;
}

</style>
