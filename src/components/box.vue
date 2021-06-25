<template>
  <div class="smart-item">
    <h2 style="margin-bottom: 50px;">{{ getLabel }}</h2>
    <div class="box">
      <img class="smart-img" :src="getUrl" :alt="getLabel" />
    </div>
    <p class="smart-desc">{{ getDesc }}</p>
  </div>
</template>

<script>
import { computed, defineComponent, ref, toRefs } from 'vue'

export default defineComponent({
  props: {
    box: {
      type: Object,
      default: () => {},
    },
  },
  setup(props) {
    const { box } = toRefs(props)
    const getUrl = computed(() => box.value.url)
    const getLabel = computed(() => box.value.label)
    const getDesc = computed(() => box.value.desc)
    return { getUrl, getDesc, getLabel }
  },
})
</script>


<style lang="less" scoped>
.smart-item {
  width: 300px;
  display: flex;
  flex-direction: column;
  align-items: center;
  .box {
    width: 300px;
    height: 300px;
    overflow: hidden;
    .smart-img {
      width: 300px;
      height: 300px;
      object-fit: contain;
      cursor: pointer;
    }
  }

  .smart-desc {
    font-size: 16px;
    width: auto;
    white-space: nowrap;
    border-right: 2px solid transparent;
    animation: typing 3.5s steps(15, end), blink-caret 0.75s step-end infinite;
    overflow: hidden;
  }
}
/* 打印效果 */
@keyframes typing {
  from {
    width: 0;
  }
  to {
    width: 80%;
  }
}
/* 光标闪啊闪 */
@keyframes blink-caret {
  from,
  to {
    box-shadow: 1px 0 0 0 transparent;
  }
  50% {
    box-shadow: 1px 0 0 0;
  }
}
</style>