<template>
  <div class="wrapper">
    <div class="line">
      <transition name="bounce" appear>
        <div v-if="show" class="indicator"></div>
      </transition>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    show: {
      type: Boolean,
      default: false,
    },
  },
};
</script>

<style scoped>
.wrapper {
  overflow: hidden;
}
.line {
  position: relative;
  width: 100%;
  height: 6px;
  background: lightgray;
}
.indicator {
  position: absolute;
  width: calc(100% - 2px);
  top: 1px;
  left: 1px;
  height: 4px;
  background: lightgreen;
}
.bounce-enter-active {
  transition: all 5s ease;
}
.bounce-leave-active {
  transition: all 0s ease;
}
.bounce-enter,
.bounce-leave-to {
  transform: translateX(-100%);
}
</style>
