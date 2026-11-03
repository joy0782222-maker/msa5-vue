<script setup>
import axios from "axios";
import { onBeforeMount, ref } from "vue";

const cards = ref([]);
const page = ref(1);
const limit = 3;

const getNextPage = async () => {
    try {
        const url = "https://picsum.photos/v2/list";

        const config = {
            params: {
                page: page.value,
                limit,
            },
        };

        const response = await axios.get(url, config);
        cards.value.push(...response.data);
        page.value++;
    } catch (error) {
        console.error(error);
    }
};

const reset = () => {
    // cards.value = [];
    // page.value = 1;
    // getNextPage();
    cards.value = cards.value.slice(0, limit);
    // cards.value = cards.value.splice(0, limit);
    page.value = 2;
};

onBeforeMount(getNextPage);
</script>

<template>
    <div class="card-con">
        <div v-for="item in cards" :key="item.id" class="card">
            <div
                class="card-img"
                :style="{ backgroundImage: `url(${item.download_url})` }"
            ></div>
            <div class="card-text">{{ item.id }}:{{ item.author }}</div>
            <!-- <div class="card-text">{{ `${item.id }: ${ item.author }`}}</div> -->
        </div>
    </div>

    <div class="btn">
        <button @click="getNextPage">next</button>
        <button @click="reset">reset</button>
    </div>
</template>

<style scoped>
.card-con {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    gap: 10px;
}
.card {
    display: flex;
    flex-direction: column;
    gap: 10px;
}
.card-img {
    aspect-ratio: 4/3;
    background-position: center;
    background-repeat: no-repeat;
    background-size: cover;
    border-radius: 5px;
}
</style>
