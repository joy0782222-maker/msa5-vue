<script setup>
import SlotChild from "./slotChild.vue";
</script>

<template>
    <h2>slot parent</h2>
    <SlotChild>내가 만든 버튼</SlotChild>
    <SlotChild></SlotChild>
    <SlotChild>전송</SlotChild>
</template>

<style scoped></style>
