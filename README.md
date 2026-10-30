# 💚 msa5-vue

> MSA 기반 자바 풀스택 과정 — **Vue 수업 기록**
> 배운 내용을 직접 따라 치면서 정리하는 저장소예요.

<br>

## 📂 목차

| 파일 | 주제 | 핵심 키워드 |
|---|---|---|
| [`src/App.vue`](./src/App.vue) | 첫 컴포넌트 & 데이터 바인딩 | `<script setup>` · `ref` · `{{ }}` · `@click` |
| [`src/main.js`](./src/main.js) | 앱 시작점 | `createApp` · `mount('#app')` |

<br>

## ✏️ 오늘의 한 줄 정리

**앱 시작점**
> `createApp(App).mount('#app')` → `App.vue`를 `index.html`의 `#app` 자리에 붙인다.

**데이터 바인딩 (`ref`)**
> `ref(0)`로 만든 값이 바뀌면 화면이 **알아서** 다시 그려진다.
> `querySelector`로 DOM을 직접 안 건드리고 **데이터만 바꾸면 끝**.

```vue
<script setup>
import { ref } from "vue";
const count = ref(0);
</script>

<template>
  <div @click="count++">count is {{ count }}</div>
  <button @click="count = 0">reset</button>
</template>
```

**가상 DOM**
> 진짜 DOM을 매번 고치면 느리니까, **복사본(가상 DOM)에서 먼저 바꿔보고 달라진 곳만** 진짜 DOM에 반영.
> 종이에 스케치해보고 달라진 데만 벽에 칠하는 느낌.

**.vue 파일 (SFC)**
> `<script setup>` · `<template>` · `<style>` 은 진짜 태그가 아니라 **칸막이(블록)**.
> 칸별로 꺼내서 JS/CSS로 변환하니까 **순서 상관없고 `defer`도 필요 없음.**
> `<style scoped>` 쓰면 이 컴포넌트에서만 스타일 적용.

<br>

## 🗓️ 다음에 배울 것

- [x] Vue 프로젝트 만들기
- [x] `ref`로 데이터 바인딩
- [ ] 컴포넌트 나누기
