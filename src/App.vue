<script setup lang="ts">
import Calender from './components/Calender.vue';

const today = new Date();
</script>

<template>
  <div class="clip"></div>
  <Calender :today="today" :viewing="today"/>
</template>

<style lang="scss" scoped>
.clip {
  height: 50px;
  border-bottom: 2px solid #969fa6;
  position: relative;
  background-color: #eeeeee;

  &::after {
    content: '';
    display: block;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    width: 15px;
    height: 15px;
    border-radius: 50%;
    background: #969fa6;
    opacity: 0.5;
  }
}
</style>

<style>
body {
  margin: 0;
}

#app {
  background-color: #fcfcfc;
}

</style>
