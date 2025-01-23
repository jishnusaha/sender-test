<script setup lang="ts">
import { ref } from "vue";
import MyIcon from "../assets/cross.svg";
const emits = defineEmits(["close", "start"]);
const inputValue = ref<number>(20);
const showError = ref<boolean>(false);
const startSorting = () => {
  if (inputValue.value && inputValue.value >= 20 && inputValue.value <= 100) {
    emits("start", inputValue.value);
  } else {
    showError.value = true;
  }
};
</script>

<template>
  <div class="modalContainer">
    <div class="modal">
      <div class="header">
        <div class="title">How many people?</div>
        <div class="cross" @click="emits('close')">
          <MyIcon />
        </div>
      </div>
      <div class="content">
        <div class="description">
          Enter a number of how many people you want to add to the list.
        </div>
        <input
          type="number"
          class="input"
          v-model="inputValue"
          min="20"
          max="100"
        />
        <p style="color: red" v-show="showError">
          Number of people should be between 20 and 100
        </p>
      </div>
      <div class="footer">
        <div class="button cancel" @click="emits('close')">Cancel</div>
        <div class="button start" @click="startSorting">Start</div>
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
    background-color: #fff;
    box-shadow: 0px 4px 4px 0px #00000040;
    .header {
      padding: 15px;
      display: flex;
      justify-content: space-between;
      .title {
        font-size: 18px;
        font-weight: 700;
      }
      .cross {
        cursor: pointer;
      }
      border-bottom: 1px solid #cccccc;
    }
    .content {
      padding: 15px 15px 40px 15px;
      .description {
        font-size: 13px;
        font-weight: 400;
      }
      .input {
        width: 100%;
        padding: 10px;
        border: 1px solid #cccccc;
        border-radius: 5px;
        margin-top: 10px;
        box-sizing: border-box;
      }
    }
    .footer {
      padding: 15px;
      display: flex;
      justify-content: flex-end;
      gap: 10px;
      border-top: 1px solid #cccccc;
      .button {
        padding: 10px;
        color: white;
        display: inline-block;
        color: white;
        background-color: #ff8d00;
        font-size: 14px;
        font-weight: 700;
        border-radius: 5px;
        cursor: pointer;
      }
      .cancel {
        color: #555555;
        background-color: #eeeeee;
      }
    }
  }
}
</style>
