<script setup>
defineEmits(["addCnt"]);
</script>

<template>
    <h2>CE Child</h2>
    <button @click="$emit('addCnt')">btn</button>
    <button @click="$emit('mtc', 2)">mt-btn</button>
</template>

<style scoped></style>
