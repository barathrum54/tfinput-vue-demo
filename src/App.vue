<template>
  <div id="app">
    <div class="container">
      <h1>TfInput Demo</h1>
      <TfInput v-model="inputValue" :size="currentSize" title="Title" description="Description"
        :border-radius="currentRadius" :state="currentState" :dark="isDarkMode"
        @update:model-state="handleInputStateChange" @update:model-value="handleValueChange"></TfInput>
      <div class="dashboard">
        <div class="dashboard-item">
          <label for="state-select">
            Change State
          </label>
          <select name="state-select" id="state-select" v-model="currentState">
            <option v-for="state in STATES" :key="state" :value="state">{{ state }}</option>
          </select>
          <small>Current state: <b>{{ currentState }}</b></small>
        </div>
        <div class="dashboard-item">
          <label for="size-select">
            Size Select
          </label>
          <select name="size-select" id="size-select" v-model="currentSize">
            <option v-for="size in INPUT_SIZE" :key="size" :value="size">{{ size }}</option>
          </select>
          <small>Current state: <b>{{ currentSize }}</b></small>
        </div>
        <div class="dashboard-item">
          <label for="dark-mode-select">
            Dark Mode
          </label>
          <select name="dark-mode-select" id="dark-mode-select" v-model="isDarkMode">
            <option value="true">True</option>
            <option value="false">False</option>
          </select>
          <small>Current mode: <b>{{ isDarkMode }}</b></small>
        </div>
        <div class="dashboard-item">
          <label for="radius-select">
            Border Radius
          </label>
          <select name="radius-select" id="radius-select" v-model="currentRadius">
            <option v-for="radius in BORDER_RADIUS" :key="radius" :value="radius">{{ radius }}</option>
          </select>
          <small>Current radius: <b>{{ currentRadius }}</b></small>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import TfInput from '@/components/TfInput.vue';
import { computed, ref } from "vue"

const STATES = ['default', 'active', 'filled', 'warning', 'danger', 'success', 'disabled'];
const BORDER_RADIUS = ['Normal', 'Rounded', 'Full'];
const INPUT_SIZE = ["XSM", 'SM', 'MD', 'LG', 'XLG']



const inputValue = ref('');
const isDarkMode = ref('false');
const currentState = ref('default');
const currentSize = ref('XSM');
const currentRadius = ref('Normal');

const handleInputStateChange = (event: any) => {
  currentState.value = event;
  console.log(event)
}
const handleValueChange = (event: any) => {
  inputValue.value = event;
  console.log(event)
}







</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Roboto&display=swap');


#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  font-family: 'Roboto', sans-serif;

}

.container {
  display: flex;
  flex-flow: column;
  justify-content: center;
  align-items: center;
  padding: 5rem;

  h1 {
    margin-bottom: 5rem;
  }
}

.dashboard {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-evenly;
  gap: 1rem;
  margin-top: 3rem;
  padding: 1rem 2rem;
  border-radius: 1rem;
  background-color: #ededed;
  width: 300px;

  .dashboard-item {
    display: flex;
    flex-flow: column;
    gap: 15px;
    font-size: 1rem;
    width: calc(50% - 1rem);
    height: 120px;

    label {
      opacity: .8;
    }

    label,
    small {
      text-align: left;
      font-weight: bold;

      b {
        opacity: 1;
        font-weight: bold;
      }
    }

    select {
      width: 100%;
      outline: none;
      border: 1px solid rgba($color: #000000, $alpha: 0.3);
      padding: .2rem .4rem;
      font-size: 1.2rem;
      font-weight: 400;
    }
  }
}
</style>
