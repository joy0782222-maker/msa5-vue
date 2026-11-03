<script setup>
import { ref } from 'vue';

const tabBtn = ref('profile');
</script>

<template>
  <h2>Tab UI</h2>
  <div class="tab-container">
    <div class="btn-wrap">
      <button class="btn" :class="{ active : tabBtn === 'profile' }" @click="tabBtn = 'profile'">profile</button>
      <button class="btn" :class="{ active : tabBtn === 'setting' }" @click="tabBtn = 'setting'">setting</button>
      <button class="btn" :class="{ active : tabBtn === 'post' }" @click="tabBtn = 'post'">post</button>
    </div>
    <div class="tab-contents">
      <div v-if="tabBtn === 'profile'" class="tab-cnt">Profile Page</div>
      <div v-else-if="tabBtn === 'setting'" class="tab-cnt">Setting Page</div>
      <div v-else class="tab-cnt">Post Page</div>
    </div>
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Gowun+Batang&family=Gowun+Dodum&display=swap');
* {
  box-sizing: border-box;
  font-family: "Gowun Batang", serif;
  letter-spacing: 0.5px;
}
.tab-container {
  width: 100%;
  margin-top: 20px;
  padding: 20px;
  box-shadow: 0 0 4px #f0f0f0;
}
.btn-wrap {
  display: flex;
  align-items: center;
  justify-content: center;
}
.btn {
  background-color: #fff;
  padding: 15px 40px;
  border: 1px solid #f0f0f0;
  font-size: 15px;
  font-weight: bold;
  color: #a0a0a0;
  text-transform: uppercase;
  cursor: pointer;
  transition: 0.3s;
}
.btn:hover{
  color: #138dff;
}
.btn.active{
  background-color: #f5f9fd;
  border: 1px solid #138dff;
  color: #138dff;
}
.tab-contents {
  height: 40vh;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 24px;
  color: #454545;
  background-color: #fafdff;
  border-radius: 10px;
}
</style>