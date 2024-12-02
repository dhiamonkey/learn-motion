<script lang="ts" setup>
import { computed, onMounted, ref } from 'vue';

const props = defineProps<{
  char: string;
  removeChar: string;
  y: number;
}>();

const charRef = ref<HTMLSpanElement>();
const initialWidth = ref(0);

function updateWidth() {
  initialWidth.value = charRef.value?.offsetWidth || 0;
}

onMounted(updateWidth);

const width = computed(() => {
  /* Width will be adjusted based on scroll position. The bigger the y, the smaller the width of the character,   which in the end will make the width as 0 */
  if (charRef.value && props.removeChar.includes(props.char) && props.y > 100) {
    return `${initialWidth.value * Math.max(300 - props.y, 0) / 200}px`;
  }
  return 'auto';
});
</script>

<template>
  <span
    ref="charRef"
    class="transition-opacity-280"
    :class="{
      'opacity-0 scale-x-0': y > 50 && removeChar.includes(char),
    }"
    :style="{ width }"
  >
    {{ char }}
  </span>
</template>
