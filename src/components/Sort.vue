<script setup lang="ts">
import { onUnmounted, ref } from "vue";
import { VueDraggableNext } from "vue-draggable-next";
import InputModal from "./InputModal.vue";
import { generateRandomString } from "../libs.ts";

interface IPeople {
  email: string;
  potatoes: number;
  name: string;
}
const totalPeople = ref<number>(0);
const poepleInfoList = ref<IPeople[]>([]);
const isInputModalVisible = ref<boolean>(false);
const isSortInProgress = ref<boolean>(false);
const timer = ref<number>(0);
let intervalId: number | null = null;

const openInputModal = () => {
  isInputModalVisible.value = true;
};

const closeInputModal = () => {
  isInputModalVisible.value = false;
};
const startSorting = (count: number) => {
  isInputModalVisible.value = false;
  const tmp: IPeople[] = [];
  for (let i = 0; i < count; i++) {
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
  isSortInProgress.value = true;
  totalPeople.value = count;
  startTimer();
};

const startTimer = () => {
  timer.value = 0;
  if (intervalId) clearInterval(intervalId);
  intervalId = setInterval(() => {
    timer.value++;
  }, 1000);
};
const onDragEnd = () => {
  let sorted = true;

  for (let i = 0; i < poepleInfoList.value.length - 1; i++) {
    if (
      poepleInfoList.value[i].potatoes < poepleInfoList.value[i + 1].potatoes
    ) {
      sorted = false;
      break;
    }
  }
  if (sorted) {
    clearInterval(intervalId!);
    isSortInProgress.value = false;
    alert(
      `Congrats. You took ${timer.value} seconds to sort the people based on potatoes`
    );
  }
};

// Cleanup timer when component unmounts
onUnmounted(() => {
  if (intervalId) clearInterval(intervalId);
});
</script>

<template>
  <InputModal
    v-if="isInputModalVisible"
    @close="closeInputModal"
    @start="startSorting"
  />
  <div class="sortContainer">
    <div class="titleContainer">
      <div class="title">Sorting Training System</div>

      <div class="button" v-if="!isSortInProgress" @click="openInputModal">
        Start sorting!
      </div>
      <div class="button" v-if="isSortInProgress">Time: {{ timer }}</div>
    </div>
    <div class="sortingTableContainer" v-if="isSortInProgress">
      <div class="title">{{ totalPeople }} people in the list</div>
      <div class="sortTable">
        <div class="people">
          <div>Eamil</div>
          <div>Name</div>
          <div>Potatoes</div>
        </div>
        <VueDraggableNext
          @end="onDragEnd"
          v-model="poepleInfoList"
          tag="div"
          item-key="email"
        >
          <div
            v-for="(people, index) in poepleInfoList"
            :key="index"
            class="people"
          >
            <div>{{ people.email }}</div>
            <div>{{ people.name }}</div>
            <div>{{ people.potatoes }}</div>
          </div>
        </VueDraggableNext>
      </div>
    </div>
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
  .sortingTableContainer {
    margin-top: 20px;
    box-shadow: 0px 4px 4px 0px #00000040;
    border: 1px solid #dddddd;
    .title {
      font-size: 14px;
      font-weight: 700;
      text-align: right;
      padding: 20px;
    }
    .sortTable {
      .people {
        border: 1px solid #dddddd;
        display: grid;
        grid-template-columns: 1fr 1fr 1fr;
        cursor: pointer;
        /* padding: 15px; */
        font-size: 14px;
        font-weight: 400;
        color: #555555;
      }
      .people > *:first-child {
        border-right: 1px solid #dddddd;
      }

      .people > * {
        padding: 15px;
      }
    }
  }
}
</style>
