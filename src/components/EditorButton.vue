<template>
  <button>
    <i>
      <slot name="icon"></slot>
    </i>
  </button>
</template>
<style lang="scss" scoped>
@import "@/assets/main.scss";

button {
  border: none;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  cursor: pointer;
  background-color: $darker;
}
</style>