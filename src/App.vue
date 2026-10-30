<script setup>
import { ref } from "vue";

const count = ref(0);
</script>

<template>
    <div @click="count++" class="btn-cnt">count is {{ count }}</div>
    <button @click="count = 0">reset</button>
</template>

<style>
.btn-cnt {
    cursor: pointer;
}
</style>
