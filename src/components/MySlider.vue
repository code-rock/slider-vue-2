<template>
  <div class="slider__wrapper">
    <div class="slider" v-if="images.length">
      <MyButton v-on:click="handlePrev"> Назад </MyButton>
      <div><img class="picture" :src="images[id].url" :alt="images[id].title" /></div>
      <MyButton v-on:click="handleNext"> Вперед </MyButton>
    </div>
    <MyLine :show="show" />
  </div>
</template>

<script>
import MyButton from "@/components/MyButton.vue";
import MyLine from "@/components/MyLine.vue";

export default {
  components: {
    MyButton,
    MyLine,
  },
  props: {
    images: {
      type: Array,
      default: [],
    },
  },
  data() {
    return {
      id: 0,
      max: 0,
      interval: 5000,
      timer: null,
      show: false,
    };
  },
  computed: {
    maxValue() {
      return this.images.length - 1;
    },
  },
  methods: {
    handlePrev() {
      this.show = false;
      this.clearTimer();
      this.prevImage();
      this.createTimer();
      this.$nextTick(() => {
        this.show = true;
      });
    },
    handleNext() {
      this.show = false;
      this.clearTimer();
      this.nextImage();
      this.createTimer();
      this.$nextTick(() => {
        this.show = true;
      });
    },
    createTimer() {
      this.timer = setInterval(() => {
        this.show = false;
        this.nextImage();
        this.$nextTick(() => {
          this.show = true;
        });
      }, this.interval);
    },
    clearTimer() {
      clearInterval(this.timer);
    },
    prevImage() {
      if (this.id === 0) {
        this.id = this.maxValue;
      } else {
        this.id -= 1;
      }
    },
    nextImage() {
      if (this.id === this.maxValue) {
        this.id = 0;
      } else {
        this.id += 1;
      }
    },
  },
  mounted() {
    this.createTimer();
    this.show = true;
  },
};
</script>

<style scoped>
.slider {
  width: 100%;
  margin-bottom: 15px;
  display: flex;
  flex-direction: row;
}
.slider__wrapper {
  width: 100%;
}
.picture {
  width: 100%;
}
</style>
