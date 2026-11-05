# 💚 msa5-vue

> MSA 기반 자바 풀스택 과정 — **Vue 수업 기록**
> 배운 내용을 직접 따라 치면서 정리하는 저장소예요.

<br>

## 📂 목차

| 파일 | 주제 | 핵심 키워드 |
|---|---|---|
| [`src/main.js`](./src/main.js) | 앱 시작점 | `createApp` · `mount('#app')` |
| [`src/App.vue`](./src/App.vue) | 컴포넌트 불러와서 화면에 붙이기 | `import` · `<컴포넌트 />` |
| [`DataBinding.vue`](./src/components/DataBinding.vue) | 데이터 바인딩 | `ref` · `{{ }}` · `@click` · `:class` · `v-model` |
| [`ConditionalRendering.vue`](./src/components/ConditionalRendering.vue) | 조건부 렌더링 | `v-if` · `v-else-if` · `v-else` · `v-show` |
| [`ListRendering.vue`](./src/components/ListRendering.vue) | 리스트 렌더링 | `v-for` · `:key` |
| [`TabUI.vue`](./src/components/TabUI.vue) | 실습: 탭 UI | `ref` + `:class` + `v-if` |
| [`Watchers.vue`](./src/components/Watchers.vue) | 감시자 | `watch` · 정규식 검사 |
| [`props/`](./src/components/props) | 부모 → 자식 데이터 전달 | `defineProps` · `:item="user"` |
| [`slot/`](./src/components/slot) | 자식에 내용 끼워넣기 | `<slot>` · 기본값 |
| [`componentEvent/`](./src/components/componentEvent) | 자식 → 부모 이벤트 전달 | `defineEmits` · `$emit` |
| [`lifeCycle.vue`](./src/components/lifeCycle.vue) | 라이프사이클 | `onBeforeMount` · `onMounted` |
| [`cardList.vue`](./src/components/cardList.vue) | 실습: 이미지 카드 목록 | `axios` · `onBeforeMount` · 더보기/리셋 |

<br>

## ✏️ 한 줄 정리

### 1. 기초

**앱 시작점**
> `createApp(App).mount('#app')` → `App.vue`를 `index.html`의 `#app` 자리에 붙인다.

**.vue 파일 (SFC)**
> `<script setup>` · `<template>` · `<style>` 은 진짜 태그가 아니라 **칸막이(블록)**.
> 칸별로 꺼내서 JS/CSS로 변환하니까 **순서 상관없고 `defer`도 필요 없음.**
> `<style scoped>` 쓰면 이 컴포넌트에서만 스타일 적용.

**가상 DOM**
> 진짜 DOM을 매번 고치면 느리니까, **복사본(가상 DOM)에서 먼저 바꿔보고 달라진 곳만** 진짜 DOM에 반영.
> 종이에 스케치해보고 달라진 데만 벽에 칠하는 느낌.

<br>

### 2. 데이터 바인딩 — `DataBinding.vue`

> `ref(0)`로 만든 값이 바뀌면 화면이 **알아서** 다시 그려진다.
> `querySelector`로 DOM을 직접 안 건드리고 **데이터만 바꾸면 끝**.

| 문법 | 뜻 | 예시 |
|---|---|---|
| `{{ }}` | 값 출력 | `{{ count }}` |
| `@click` | 이벤트 연결 (`v-on:click` 줄임) | `@click="count++"` |
| `:class` | 속성에 값 연결 (`v-bind:class` 줄임) | `:class="bgColor"` |
| `v-model` | 입력창 ↔ 데이터 **양방향** 연결 | `v-model="email"` |

```vue
<script setup>
import { ref } from "vue";
const count = ref(0);
const bgColor = ref("");

const toggleBgColor = () => {
  // script 안에서는 .value 붙여야 함
  bgColor.value = bgColor.value === "" ? "bg-red" : "";
};
</script>

<template>
  <!-- template 안에서는 .value 없이 바로 씀 -->
  <div @click="count++" :class="bgColor">Count is {{ count }}</div>
  <button @click="toggleBgColor">Toggle</button>
</template>
```

> ⚠️ `ref` 값은 **script에서는 `.value`**, **template에서는 그냥 이름**으로 쓴다.

<br>

### 3. 조건부 렌더링 — `ConditionalRendering.vue`

> `v-if` / `v-else-if` / `v-else` 로 조건에 맞는 태그만 화면에 그린다. (JS의 if문이랑 똑같은 흐름)

```vue
<p v-if="num === 0">0</p>
<p v-else-if="num % 2 === 0">{{ num }} is even</p>
<p v-else>{{ num }} is odd</p>
```

**`v-if` vs `v-show`**

| | `v-if` | `v-show` |
|---|---|---|
| 거짓일 때 | 태그 자체를 **없앰** | 태그는 두고 `display: none` |
| 어울리는 곳 | 잘 안 바뀌는 것 | 자주 껐다 켜는 것 |

**`:class` 객체 문법**
> `:class="{ 'btn-toggle': flg === false }"` → 조건이 참일 때만 클래스가 붙는다.

<br>

### 4. 리스트 렌더링 — `ListRendering.vue`

> 배열을 `v-for`로 돌면서 태그를 반복해서 만든다. `:key`에는 **겹치지 않는 값(id)** 을 꼭 넣기.

```vue
<div v-for="item in items" :key="item.id" class="card">
  <p>{{ item.kinds }}</p>
  <span>{{ item.food }}</span>
</div>
```

<br>

### 5. 실습: 탭 UI — `TabUI.vue`

> 지금 선택된 탭 이름 하나만 `ref`로 들고 있으면 끝.
> 버튼은 `:class="{ active: tabBtn === 'profile' }"` 로 색 바꾸고, 내용은 `v-if`로 골라서 보여준다.

```vue
<button :class="{ active: tabBtn === 'profile' }" @click="tabBtn = 'profile'">profile</button>

<div v-if="tabBtn === 'profile'">Profile Page</div>
<div v-else-if="tabBtn === 'setting'">Setting Page</div>
<div v-else>Post Page</div>
```

<br>

### 6. 감시자 — `Watchers.vue`

> `watch(감시할값, (바뀐값) => { ... })` → 값이 **바뀔 때마다** 함수가 실행된다.
> 실습: 입력값이 영어만 있으면 초록 `o`, 아니면 빨간 `x` 표시.

```js
watch(test, (val) => {
  const pattern = /^[a-zA-Z]+$/u;
  if (val === "") testErrorMsg.value = "";
  else if (pattern.test(val)) { testErrorMsg.value = "o"; testColer.value = "color: green;"; }
  else { testErrorMsg.value = "x"; testColer.value = "color: red;"; }
});
```

<br>

### 7. 컴포넌트끼리 주고받기

```
   부모  ── props (데이터) ──▶  자식
   부모  ◀── emit (이벤트) ──   자식
   부모  ── slot (태그/내용) ─▶  자식
```

**props — 부모 → 자식** (`props/`)
> 부모가 `:이름="값"` 으로 넘기고, 자식은 `defineProps`로 받는다.

```vue
<!-- parent.vue -->
<child :item="user" :str="str" />

<!-- child.vue -->
<script setup>
const { item, str } = defineProps({ item: Object, str: String });
</script>
<template><p>{{ item.name }}</p></template>
```

**emit — 자식 → 부모** (`componentEvent/`)
> 자식은 데이터를 직접 못 바꾸니까 **"버튼 눌렸어!" 신호만** 보낸다. 실제로 바꾸는 건 부모.
> 두 번째 값을 넣으면 신호랑 같이 데이터도 보낼 수 있다.

```vue
<!-- CEChild.vue -->
<button @click="$emit('addCnt')">btn</button>
<button @click="$emit('mtc', 2)">mt-btn</button>

<!-- CEParent.vue -->
<CEChild @addCnt="addCnt" @mtc="mtc" />
```

**slot — 부모가 자식 안에 내용 끼워넣기** (`slot/`)
> 자식의 `<slot>` 자리에 부모가 쓴 내용이 들어간다. 아무것도 안 넣으면 `<slot>기본</slot>` 의 **기본값**이 나온다.

```vue
<!-- slotChild.vue -->
<button><slot>기본</slot></button>

<!-- slotParent.vue -->
<SlotChild>내가 만든 버튼</SlotChild>  <!-- "내가 만든 버튼" -->
<SlotChild></SlotChild>                <!-- "기본" -->
```

<br>

### 8. 라이프사이클 — `lifeCycle.vue`

> 컴포넌트가 화면에 붙기 **전/후**에 원하는 코드를 실행할 수 있다.

| 함수 | 언제 |
|---|---|
| `onBeforeMount` | 화면에 붙기 **직전** |
| `onMounted` | 화면에 붙은 **직후** (DOM 접근 가능) |

<br>

### 9. 실습: 이미지 카드 목록 — `cardList.vue`

> 지금까지 배운 걸 합친 실습. [Picsum API](https://picsum.photos)에서 사진을 3장씩 받아와 카드로 보여준다.

- `onBeforeMount(getNextPage)` → 처음 뜰 때 첫 페이지 불러오기
- `axios.get(url, { params: { page, limit } })` → 페이지 번호로 요청
- `cards.value.push(...response.data)` → 기존 카드 뒤에 이어 붙이기 (**next**)
- `cards.value.slice(0, limit)` + `page.value = 2` → 첫 3장만 남기기 (**reset**)
- ``:style="{ backgroundImage: `url(${item.download_url})` }"`` → 받아온 주소로 배경 이미지 지정

<br>

## 🗓️ 진도 체크

- [x] Vue 프로젝트 만들기
- [x] `ref`로 데이터 바인딩
- [x] 조건부 · 리스트 렌더링
- [x] 감시자 (`watch`)
- [x] 컴포넌트 나누기 (props · emit · slot)
- [x] 라이프사이클
- [x] Vue 입문 완료 🎉
