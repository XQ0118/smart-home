<template>
  <div :class="classObject">
    <Box :box="currentItem" :key="currentItem.url"></Box>
    <div class="smart-select">
      <a-select v-model:value="currentItem" style="width: 200px; margin-right: 8px" size="large">
        <a-select-option v-for="item in optionsList" :key="item.url" :value="item">{{ item.label }}</a-select-option>
      </a-select>
      <a-button size="large" type="primary" @click="handleClick">
        {{
        isPlay
        }}
      </a-button>
    </div>
    <transition name="fade">
      <a-alert type="info" message="我发出指令啦！" show-icon class="show-working" v-show="play"></a-alert>
    </transition>
  </div>
</template>

<script>
import { computed, defineComponent, ref } from 'vue'
import Box from './box.vue'

export default defineComponent({
  components: {
    Box,
  },
  setup (props, { emit }) {
    const rightList = [
      {
        label: '手机',
        desc: '智能手机，极致体验，改变生活',
        url: 'https://store.storeimages.cdn-apple.com/8756/as-images.apple.com/is/iphone-12-family-select-2021?wid=940&hei=1112&fmt=jpeg&qlt=80&.v=1617135051000',
      },
      {
        label: '平板电脑',
        desc: '身材小，本事大，速度快',
        url: 'https://store.storeimages.cdn-apple.com/8756/as-images.apple.com/is/ipad-air-select-wifi-green-202009?wid=470&hei=556&fmt=png-alpha&.v=1598650644000, https://store.storeimages.cdn-apple.com/8756/as-images.apple.com/is/ipad-air-select-wifi-green-202009?wid=940&hei=1112&fmt=png-alpha&.v=1598650644000',
      },
      {
        label: '智能门锁',
        desc: '指纹解锁，保护家庭安全',
        url: 'https://cdn.aqara.com/cdn/website/static/lodash-4.17.15/N200_fengmian.png',
      },
      {
        label: '光照传感器',
        desc: '智能感知家中光感变化',
        url: 'https://cdn.aqara.com/cdn/website/static/lodash-4.17.15/light-brightness-sensor-t1.png',
      },
      {
        label: '人体传感器',
        desc: '智能感知人体或动物的移动',
        url: 'https://cdn.aqara.com/cdn/website/static/lodash-4.17.15/motion-detector-t1.png',
      },
      {
        label: '温湿度传感器',
        desc: '监测温湿度状况实时反馈',
        url: 'https://cdn.aqara.com/cdn/website/static/lodash-4.17.15/温湿度传感器.png',
      },
      {
        label: '烟雾报警器',
        desc: '时刻守护家庭火情安全',
        url: 'https://cdn.aqara.com/cdn/website/static/lodash-4.17.15/烟雾报警器.png',
      },
    ]

    const optionsList = ref(rightList)
    const getFirstOne = optionsList.value[0]
    const currentItem = ref(getFirstOne)
    const play = ref(false)

    const classObject = computed(() => {
      return play.value
        ? { 'smart-box-right-ani': true, ripple: play.value }
        : {
          'smart-box-right': true,
        }
    })

    const isPlay = computed(() => (play.value ? '结束' : '工作'))

    const handleClick = () => {
      console.log('handle click =>')

      play.value = !play.value
      // document.querySelector('#audio').play()

      emit('working', play.value)
    }

    return { optionsList, currentItem, play, isPlay, classObject, handleClick }
  },
})
</script>


<style lang="less" scoped>
.smart-box-right {
  width: 340px;
  display: flex;
  flex-direction: column;
  align-items: center;
  border-radius: 2px;
  border: 2px solid #f0f0f0;
  padding: 12px;
  box-shadow: 0 2px 8px rgb(0 0 0 / 9%);

  .smart-select {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 250px;
    // margin: auto;
    margin-top: 12px;
  }

  .show-working {
    color: #1890ff;
    font-size: 20px;
    font-weight: 700;
    top: -50px;
    // left: 0;
    border: 2px solid #1890ff;
    padding: 0 12px;
    border-radius: 4px;
    position: absolute;
  }
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.smart-box-right-ani {
  width: 340px;
  display: flex;
  flex-direction: column;
  align-items: center;
  border-radius: 2px;
  border: 2px solid #f0f0f0;
  padding: 12px;
  box-shadow: 0 2px 8px rgb(0 0 0 / 9%);

  position: relative;

  animation-play-state: paused;
  -webkit-animation-play-state: paused;

  .smart-select {
    display: flex;
    justify-content: space-between;
    align-items: center;
    width: 250px;
    // margin: auto;
    margin-top: 12px;
  }

  .show-working {
    color: #1890ff;
    font-size: 20px;
    font-weight: 700;
    top: -50px;
    // left: 0;
    border: 2px solid #1890ff;
    padding: 0 12px;
    border-radius: 4px;
    position: absolute;
  }
}

.smart-box-right-ani::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 400px;
  height: 400px;
  border: 2px solid #1890ff;
  border-radius: 50%;
  pointer-events: none;
  opacity: 0;
  animation: ripple 2s linear 1s infinite;
  animation-play-state: paused;
  -webkit-animation-play-state: paused;
}

.smart-box-right-ani::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 400px;
  height: 400px;
  border: 2px solid #1890ff;
  border-radius: 50%;
  pointer-events: none;
  opacity: 0;
  animation: ripple 2s linear infinite;
  animation-play-state: paused;
  -webkit-animation-play-state: paused;
}
.ripple {
  animation-play-state: running;
  -webkit-animation-play-state: running;
}
.ripple:before {
  animation-play-state: running;
  -webkit-animation-play-state: running;
}
.ripple:after {
  animation-play-state: running;
  -webkit-animation-play-state: running;
}
@keyframes ripple {
  0% {
    transform: scale(1);
    opacity: 0;
  }

  25% {
    transform: scale(1.25);
    opacity: 0.1;
  }

  50% {
    transform: scale(1.5);
    opacity: 0.3;
  }

  75% {
    transform: scale(1.75);
    opacity: 0.5;
  }

  100% {
    transform: scale(2);
    opacity: 0;
  }
}
</style>