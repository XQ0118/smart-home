<template>
  <div class="container">
    <LeftPart :disabled="isDisabled" :working="isWorking"></LeftPart>
    <div class="wifi-container">
      <Wifi class="wifi"></Wifi>
    </div>
    <RightPart :disabled="isDisabled" @working="handleWorking"></RightPart>
    <Message class="message"></Message>
  </div>
</template>

<script>
import { defineComponent, ref } from 'vue'
import LeftPart from './components/leftPart.vue'
import RightPart from './components/rightPart.vue'
import Wifi from './components/wifi.vue'
import Message from './components/message.vue'

export default defineComponent({
  components: {
    LeftPart, RightPart, Wifi, Message
  },
  setup () {

    const isWorking = ref(false)
    const rfa = ref(null)

    const isDisabled = ref(false)

    const move = () => {
      const el = document.querySelector('.message')
      const left = el.getBoundingClientRect().left
      el.style.left = `${left - 10}px`

      if (left === 350) {
        cancelAnimationFrame(rfa.value)
        isWorking.value = true
        isDisabled.value = false
      } else {
        rfa.value = requestAnimationFrame(move)
      }

    }

    const handleWorking = (state) => {

      isDisabled.value = state

      if (state) {
        // move(-50)
        rfa.value = requestAnimationFrame(move)
      } else {
        console.log('done ', state)
        const el = document.querySelector('.message')
        el.style.left = ''
        el.style.right = '300px'
        isWorking.value = false

      }
    }


    return { isWorking, handleWorking, isDisabled }
  },
})
</script>


<style lang="less" scoped>
.container {
  width: 100vw;
  height: 100vh;
  min-width: 1300px;
  min-height: 800px;
  position: relative;
  overflow: auto;

  .smart-box-left {
    position: absolute;
    top: 20%;
    left: 200px;
  }

  .smart-box-right {
    position: absolute;
    top: 20%;
    right: 200px;
  }

  .smart-box-right-ani {
    position: absolute;
    top: 20%;
    right: 200px;
  }

  .wifi-container {
    position: absolute;
    top: 40%;
    left: 47.5%;
    .wifi {
      width: 100px;
      height: 100px;
    }
  }

  .message {
    position: absolute;
    top: 250px;
    right: 340px;
  }
}
</style>