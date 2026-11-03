<script setup>
import { ref } from 'vue';

const num = ref(0);
const flg = ref(true);
</script>

<template>
  <input type="number" v-model="num" value="num">
  <p v-if="num === 0">0</p>
  <p v-else-if="num % 2 === 0">{{ num.toLocaleString() }} is even</p>
  <p v-else>{{ num.toLocaleString() }} is odd</p>

  <br>
  <br>
  
  <button @click="flg = !flg" :class="{ 'btn-toggle' : flg === false }">Toggle</button>
  <!-- <button @click="flg = !flg" :class="flg ? 'btn-toggle' : '' ">Toggle</button> -->
  <p v-if="flg">v-if</p>
  <p v-show="flg">v-show</p>
</template>

<style>
.btn-toggle {
  background-color: #2f7679;
  color: #f4f5f6;
}
</style>