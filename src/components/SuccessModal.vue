<script setup lang="ts">
import MyIcon from "../assets/cross.svg";
const emits = defineEmits(["close"]);
const props = defineProps(["time"]);
</script>

<template>
  <div class="modalContainer">
    <div class="modal">
      <div class="cross" @click="emits('close')">
        <MyIcon />
      </div>
      <div class="title">Congratulations</div>
      <div class="description">
        You have completed the task in
        <span class="value"> {{ props.time }}</span> seconds
      </div>
    </div>
  </div>
</template>

<style scoped>
.modalContainer {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 100;
  .modal {
    width: 437px;
    border-radius: 5px;
    border: 1px solid #00000040;

    background-color: #fff;
    box-shadow: 0px 4px 4px 0px #00000040;
    padding: 30px 15px;
    text-align: center;
    position: relative;

    .cross {
      position: absolute;
      right: 10px;
      top: 10px;
      cursor: pointer;
    }
    .title {
      font-size: 24px;
      font-weight: bold;
      color: green;
    }
    .description {
      margin-top: 10px;
      font-weight: bold;
      font-size: 14px;
      .value {
        font-size: 18px;
      }
    }
  }
}
</style>
