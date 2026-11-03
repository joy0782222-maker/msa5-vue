<script setup>
import { onBeforeMount, onMounted } from "vue";

onBeforeMount(() => {
    alert("마운트 전 실행");
});
onMounted(() => {
    alert("마운트 후 실행");
});
</script>

<template>
    <h2>Life Cycle</h2>
</template>

<style scoped></style>
