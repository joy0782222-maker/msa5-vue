<script setup>
import { ref } from "vue";
import CEChild from "./CEChild.vue";

const count = ref(0);

const addCnt = () => {
    count.value++;
};

const mtc = (val) => {
    count.value *= val;
};
</script>

<template>
    <div class="cntBtn">
        <h2>CE Parent</h2>
        <p>카운트 : {{ count }}</p>

        <CEChild @addCnt="addCnt" @mtc="mtc" />
    </div>
</template>

<style scoped></style>
