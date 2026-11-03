<script setup>
// import { defineProps } from "vue";

const { item, str } = defineProps({
    item: Object,
    str: String,
});
</script>

<template>
    <h2>child</h2>
    <p>{{ item.name }}</p>
</template>

<style></style>
