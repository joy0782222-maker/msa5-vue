<script setup>
import { ref } from "vue";
import child from "./child.vue";

const user = ref({
    id: 1,
    name: "홍길동",
    age: 20,
});
const str = ref("전달 문자열");
</script>

<template>
    <h2>parent</h2>
    <child :item="user" :str="str" />
</template>

<style></style>
