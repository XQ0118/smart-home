<template>
  <div class="container">
    <LeftPart></LeftPart>
    <RightPart></RightPart>
    <div class="wifi-container">
      <Wifi class="wifi"></Wifi>
    </div>
  </div>
</template>

<script setup>
import LeftPart from './components/leftPart.vue'
import RightPart from './components/rightPart.vue'
import Wifi from './components/wifi.vue'
</script>


<style lang="less" scoped>
.container {
  width: 100vw;
  height: 100vh;
  padding: 100px;
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  position: relative;

  .wifi-container {
    position: fixed;
    bottom: 0;
    left: 48%;
    .wifi {
      width: 100px;
      height: 100px;
    }
  }
}
</style>