<script setup>
import { ref } from 'vue';

const items = ref([
  {
    id: 1,
    kinds: '중식',
    food: '짜장면'
  },
  {
    id: 2,
    kinds: '한식',
    food: '비빔밥'
  },
  {
    id: 3,
    kinds: '일식',
    food: '돈까스'
  },
]);
</script>

<template>
  <h2>List Rendering</h2>
  <div class="container">
    <div v-for="item in items" :key="item.id" class="card">
      <p>{{ item.kinds }}</p>
      <span>{{ item.food }}</span>
    </div>
  </div>
</template>

<style>
.container {
  padding: 20px;
  background-color: #fff;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
}
.card {
  flex: 1;
  padding: 20px;
  border: 1px solid #f4f5f6;
  border-radius: 10px;
}
.card p {
  font-size: 14px;
  margin: 5px 0;
  color: #666;
}
.card span {
  font-weight: bold;
  color: #454545;
}
</style>