<script setup>
import { ref, watch } from "vue";

const test = ref("");
const testErrorMsg = ref("");
const testColer = ref("");

// watchers
watch(test, (val) => {
    const pattern = /^[a-zA-Z]+$/u;
    if (val === "") {
        testErrorMsg.value = "";
    } else if (pattern.test(val)) {
        testErrorMsg.value = "o";
        testColer.value = "color: green;";
    } else {
        testErrorMsg.value = "x";
        testColer.value = "color: red;";
    }
});
</script>

<template>
    <h2>Watchers</h2>
    <input type="text" v-model="test" />
    <p :style="testColer">{{ testErrorMsg }}</p>
</template>

<style></style>
