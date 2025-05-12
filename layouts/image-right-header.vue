<script setup lang="ts">
import { computed } from 'vue'
import { handleBackground } from '@slidev/client/layoutHelper.ts'

const props = defineProps({
  image: {
    type: String,
  },
  imagedSize: {
    type: String,
    default: 'contain',
  },
  class: {
    type: String,
  },
  layoutClass: {
    type: String,
  },
})


const style = computed(() => handleBackground(props.image, false, props.imagedSize))
</script>

<template>
  <div class="slidev-layout image-right-header w-full h-full" :class="layoutClass">
    <div class="col-header">
      <slot />
    </div>
    <div class="col-left" :class="props.class">
      <slot name="left" />
    </div>
    <div class="image-right" :class="props.class" :style="style">
        <slot name="right" />
    </div>
  </div>
</template>

<style scoped>
.image-right-header {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-template-rows: none;
}

.col-header {
  grid-area: 1 / 1 / 2 / 3;
}
.col-left {
  grid-area: 2 / 1 / 3 / 2;
}
.image-right {
  grid-area: 2 / 2 / 3 / 3;
}
</style>
