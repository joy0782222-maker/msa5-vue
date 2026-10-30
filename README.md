# 💚 msa5-vue

> MSA 기반 자바 풀스택 과정 — **Vue 수업 기록**
> Vite로 Vue 프로젝트를 만들고, 배운 내용을 직접 따라 치면서 정리하는 저장소예요.

<br>

## 📂 목차

| 파일 | 주제 | 핵심 키워드 |
|---|---|---|
| [`src/App.vue`](./src/App.vue) | 첫 컴포넌트 & 데이터 바인딩 | `<script setup>` · `ref` · `{{ }}` · `@click` |
| [`src/main.js`](./src/main.js) | 앱 시작점 | `createApp` · `mount('#app')` |
| [`ex.js`](./ex.js) · [`test.js`](./test.js) | 모듈 내보내기/가져오기 | `export` · `export default` · `import` |
| [`package.json`](./package.json) | 프로젝트 설정 | `dependencies` · `devDependencies` · `scripts` |

<br>

## 🚀 실행 방법

```bash
npm i          # 패키지 설치 (node_modules 생성)
npm run dev    # 개발 서버 실행 → localhost:5173
npm run build  # 배포용 완성본 생성 → dist 폴더
```

> 개발 서버 종료는 터미널에서 `Ctrl + C`

<br>

## ✏️ 오늘의 한 줄 정리

**Vite로 프로젝트 만들기**
> `npm create vite@latest .` → 점(`.`)은 **지금 폴더에 바로** 만들라는 뜻.
> Vite는 개발 서버를 빠르게 띄워주고, 저장하면 브라우저에 바로 반영된다.

**dependencies vs devDependencies**
> 서버 구분이 아니라 **"돌릴 때도 쓰냐, 만들 때만 쓰냐"** 의 차이.

| dependencies | devDependencies |
|---|---|
| 서비스 돌릴 때 필요 | 개발할 때만 필요 |
| `vue`, `axios` | `vite`, `@vitejs/plugin-vue` |
| `npm i 패키지` | `npm i -D 패키지` |

**dev vs build**
> `npm run dev`는 내 컴퓨터에서 확인하는 용, `npm run build`는 서버에 올릴 **포장**.
> `dist` 안의 파일을 Nginx의 `html` 폴더에 넣으면 배포 끝! (폴더째 말고 **안의 파일**만)

**package.json vs package-lock.json**
> `package.json`은 **장보기 목록**(대충 버전), `package-lock.json`은 **영수증**(정확한 버전).
> `node_modules`는 OS마다 내용이 달라서 복사하지 말고, 받은 쪽에서 `npm i` 새로 하기.

**export vs export default**
> `export`는 여러 개 가능, 가져올 때 `{ }` + **이름 똑같이**.
> `export default`는 파일당 **하나만**, `{ }` 없이 이름 자유.

```js
// ex.js
export const num = 1;
export function text() { return 3; }

// test.js
import { num, text } from "./ex.js";
```

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
> Vite가 칸별로 꺼내서 JS/CSS로 변환하니까 **순서 상관없고 `defer`도 필요 없음.**
> `<style scoped>` 쓰면 이 컴포넌트에서만 스타일 적용, `lang="scss"` 붙이면 `&:hover` 같은 중첩 가능.

<br>

## 🤝 팀플 npm 규칙

1. `node_modules` ❌ 안 올림 (`.gitignore` 확인)
2. 패키지 추가하면 팀원한테 공유 → 받은 사람은 `pull` 후 `npm i`
3. Node 버전 통일
4. lock 충돌 나면 손으로 고치지 말고 지우고 `npm i`

<br>

## 🗓️ 다음에 배울 것

- [x] Vite로 Vue 프로젝트 만들기
- [x] `ref`로 데이터 바인딩
- [ ] 컴포넌트 나누기
