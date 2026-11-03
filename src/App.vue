<script setup>
import ListRendering from "./components/ListRendering.vue";
import TabUI from "./components/TabUI.vue";
import Parent from "./components/props/parent.vue";
import SlotParent from "./components/slot/slotParent.vue";
import CEParent from "./components/componentEvent/CEParent.vue";

// import DataBinding from './components/DataBinding.vue';
// import ConditionalRendering from './components/ConditionalRendering.vue';
import Watchers from "./components/Watchers.vue";
import LifeCycle from "./components/lifeCycle.vue";
import CardList from "./components/cardList.vue";
</script>

<template>
    <h1>APP Component</h1>
    <!-- <DataBinding></DataBinding> 
  <DataBinding />
  <ConditionalRendering />
  <ListRendering /> -->
    <!-- <TabUI /> -->
    <!-- <Watchers /> -->
    <!-- <Parent /> -->
    <!-- <slotParent /> -->
    <!-- <CEParent /> -->
    <!-- <LifeCycle /> -->
    <card-list />
</template>

<style></style>
