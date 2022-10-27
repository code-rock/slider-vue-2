<template>
  <button class="button" @click="handleClick">
    <slot></slot>
  </button>
</template>

<script>
export default {
  methods: {
    handleClick() {
      this.$emit("click");
    },
  },
};
</script>

<style scoped>
.button {
  padding: 10px 15px;
  border: none;
  box-shadow: 1px 1px 5px lightgray;
  cursor: pointer;
}
</style>
