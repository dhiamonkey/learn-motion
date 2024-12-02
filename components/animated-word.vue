<script setup lang="ts">
import { useWindowScroll } from '@vueuse/core';

import AnimatedChar from './animated-char.vue';

defineProps<{
  removeChar: string;
  text?: string;
}>();

const { y } = useWindowScroll();
</script>

<template>
  <div class="flex-center">
    <AnimatedChar
      v-for="char in text"
      :key="char"
      class="text-h2"
      :char="char"
      :remove-char="removeChar"
      :y="y"
    />
  </div>
</template>

<style lang="css" scoped>
.text-h2 {
    font-size: 150px;
    line-height: 154px;
}

.flex-center{
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>

