<template>
  <div class="smart-box">
    <Box :box="currentItem" :key="currentItem.url"></Box>
    <div class="smart-select">
      <a-select v-model:value="currentItem" style="width: 240px" size="large">
        <a-select-option
          v-for="item in optionsList"
          :key="item.url"
          :value="item"
          >{{ item.label }}</a-select-option
        >
      </a-select>
    </div>
  </div>
</template>

<script>
import { defineComponent, ref } from 'vue'
import Box from './box.vue'

export default defineComponent({
  components: {
    Box,
  },
  setup() {
    const leftList = [
      {
        label: '智能墙壁开关',
        desc: '支持语音 & APP 控制智能操控开关',
        url: 'https://cdn.aqara.com/cdn/website/mainland/static/lodash-4.17.15/E1-zhutu.png',
      },
      {
        label: '智能灯光模块',
        desc: '支持颜色控制、亮度色温控制、渐明渐暗',
        url: 'https://cdn.aqara.com/cdn/website/mainland/static/lodash-4.17.15/led_t1_247-247.png',
      },
      {
        label: '扫地机器人',
        desc: '扫净一切垃圾',
        url: 'https://cdn.cnbj0.fds.api.mi-img.com/b2c-shopapi-pms/pms_1621234077.16667984.jpg',
      },
      {
        label: '智能摄像机',
        desc: '捕捉家中异常，为家庭提供一个安全环境',
        url: 'https://cdn.aqara.com/cdn/website/mainland/static/lodash-4.17.15/g3主图.png',
      },
      {
        label: '空调伴侣',
        desc: '让传统空调秒变智能，可被智能控制',
        url: 'https://cdn.aqara.com/cdn/website/static/lodash-4.17.15/202003171521034Gye.png',
      },
    ]

    const optionsList = ref(leftList)
    const getFirstOne = optionsList.value[0]
    const currentItem = ref(getFirstOne)
    return { optionsList, currentItem }
  },
})
</script>


<style lang="less" scoped>
.smart-box {
  width: 340px;
  display: flex;
  flex-direction: column;
  align-items: center;
  border-radius: 2px;
  border: 2px solid #f0f0f0;
  padding: 12px;
  box-shadow: 0 2px 8px rgb(0 0 0 / 9%);

  .smart-select {
    width: 240px;
    // margin: auto;
    margin-top: 12px;
  }
}
</style>