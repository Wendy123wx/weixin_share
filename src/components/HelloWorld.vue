<template>
   <div class="circle-progress">
    <div class="progress">
      <div v-for="item in 2" :key="item" class="semi-circle" :class="`semi-circle${item}`">
        <div
          v-if="rate < 0.5 * item"
          class="modal"
          :class="`modal${item}`"
          :style="{transform: getProgress(item)}"
        ></div>
      </div>
    </div>
    <div class="content">观看{{rate}}</div>
  </div>
</template>

<script>
export default {
  name: 'circle-progress',
  props: {
    rate: {
      default: 0
    }
  },
  methods: {
    getProgress (index) {
      const { rate } = this
      if (index === 1) {
        return `rotate(${(rate / 0.5) * 180}deg)`
      }
      if (index === 2) {
        if (rate > 0.5) {
          return `rotate(${((rate - 0.5) / 0.5) * 180}deg)`
        }
      }
    }
  }
}
</script>
<style lang="less" scoped>
  .circle-progress {
    width: 500px;
    height: 500px;
    line-height: 500px;
    color: #fff;
    background-color: #5c5a68;
    border-radius: 100%;
    overflow: hidden;
  .progress,
  .content {
    width: 100%;
    height: 100%;
  }
  .content{
    margin-top: -500px;
  }
  .progress {
    display: flex;
    flex-direction: row-reverse;
    .semi-circle {
      width: 50%;
      height: 100%;
      background-color: red;
      opacity: 0.4;
      .modal {
        width: 100%;
        height: 100%;
        background-color: rgb(11, 12, 11);
        &1 {
          transform-origin: 0 50%;
        }
        &2 {
          transform-origin: 100% 50%;
        }
      }
    }
    // .semi-circle-right{
    //   transform-origin: 0 50%;
    // }
    // .semi-circle-left{
    //   transform-origin: 50% 0;
    // }
  }
}

</style>
