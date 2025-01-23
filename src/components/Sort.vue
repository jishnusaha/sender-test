<script setup lang="ts">
import { ref } from "vue";
import Modal from "./Modal.vue";
import { generateRandomString } from "../libs.ts";

interface IPeople {
  email: string;
  potatoes: number;
  name: string;
}
const isModalVisible = ref<boolean>(false);
const poepleInfoList = ref<IPeople[]>([]);

const openModal = () => {
  isModalVisible.value = true;
};

const closeModal = () => {
  isModalVisible.value = false;
};
const startSorting = (totalPeople: number) => {
  isModalVisible.value = false;
  const tmp: IPeople[] = [];
  for (let i = 0; i < totalPeople; i++) {
    const firstName = generateRandomString(5);
    const lastName = generateRandomString(4);
    tmp.push({
      email: `${firstName}.${lastName}${i + 1}@gmail.com`,
      potatoes: i + 1,
      name: `${firstName} ${lastName}`,
    });
  }
  // shuffling
  for (let i = tmp.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [tmp[i], tmp[j]] = [tmp[j], tmp[i]]; // Swap elements
  }
  poepleInfoList.value = tmp;
};
</script>

<template>
  <Modal v-if="isModalVisible" @close="closeModal" @start="startSorting" />
  <div class="sortContainer">
    <div class="titleContainer">
      <div class="title">Sorting Training System</div>
      <div class="button" @click="openModal">Start sorting!</div>
    </div>
    <div class="sortingTable"></div>
  </div>
</template>

<style scoped>
.sortContainer {
  padding: 0 72px;
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
  .sortingTable {
    margin-top: 20px;
    box-shadow: 0px 4px 4px 0px #00000040;
  }
}
</style>
