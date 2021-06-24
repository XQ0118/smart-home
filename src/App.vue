<template>
  <div class="container">
    <LeftPart></LeftPart>
    <div class="wifi-container">
      <Wifi class="wifi"></Wifi>
    </div>
    <RightPart></RightPart>
    
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
  padding: 200px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: relative;

  .wifi-container {
    // position: fixed;
    top: 0;
    left: 48%;
    .wifi {
      width: 100px;
      height: 100px;
    }
  }
}
</style>