<template>
  <div class="wrapper">
    <editor-text-simple v-model="text" />
  </div>
</template>

<script setup>
import EditorTextSimple from "@/components/EditorTextSimple.vue";
import { ref } from "vue";

const text = ref(
  "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
);
</script>
<style>
.wrapper {
  text-align: center;
  padding-left: 200px;
  padding-right: 200px;
}
</style>
