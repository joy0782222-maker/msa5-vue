<script setup>
import { ref } from 'vue';

const count = ref(0);
const bgColor = ref('');
const email = ref('aaa');

const toggleBgColor = () => {
  if(bgColor.value === '') {
    bgColor.value = 'bg-red';
  } else {
    bgColor.value = '';
  }
};
</script>

<template>
  <div class="btn-cnt" @click="count++" :class="bgColor">Count is {{ count }}</div>
  <button @click="count = 0">Count Reset</button>
  <button @click="count--">Count Down</button>
  <button @click="bgColor = 'bg-red'">Red</button>
  <button @click="bgColor = ''">Color Reset</button>
  <button @click="toggleBgColor">Toggle</button>
  <br>
  <br>
  <input type="text" name="email" id="email" v-model="email" placeholder="insert email address">
  <p>{{ email }}</p>
</template>

<style>
.btn-cnt { 
  width: fit-content;
  margin: 50px auto;
  padding: 10px 20px;
  border: 1px solid #cdd1d5;
  border-radius: 4px;
  cursor: pointer;
  transition: 0.3s;
}
.btn-cnt:hover{
  background-color: #f4f5f6;
}
button{
  width: 120px;
  padding: 10px 20px;
  margin: 0 auto;
  border: 1px solid #cdd1d5;
  border-radius: 4px;
  background-color: #fff;
  color: #454545;
  cursor: pointer;
  transition: 0.3s;
}
button:hover{
  background-color: #f4f5f6;
}
button {
  margin-top: 10px;
}
.bg-red {
  background-color: #ff4b4b;
  color: #f4f5f6;
}
input{
  padding: 10px;
  border: 1px solid #cdd1d5;
}
</style>