<script setup lang="ts">
import { ref } from "vue";
import Modal from "./Modal.vue";

const isModalVisible = ref(false);

const openModal = () => {
  isModalVisible.value = true;
};

const closeModal = () => {
  isModalVisible.value = false;
};
const startSorting = (value: number) => {
  console.log("Sorting started with value:", value);
  isModalVisible.value = false;
};
</script>

<template>
  <Modal v-if="isModalVisible" @close="closeModal" @start="startSorting" />
  <div class="titleContainer">
    <div class="title">Sorting Training System</div>
    <div class="button" @click="openModal">Start sorting!</div>
  </div>
</template>

<style scoped>
.titleContainer {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
  .title {
    font-size: 32px;
    font-weight: 700;
  }
  .button {
    cursor: pointer;
    width: 161px;
    height: 50px;
    color: white;
    background-color: #ff8d00;
    border-radius: 5px;
    display: grid;
    align-items: center;
    justify-content: center;
    font-size: 15px;
  }
}
</style>
