<template>
  <!-- code... -->
  <div class="dropdown" ref="dropdownRef">
    <a href="#" class="btn btn-outline-light my-2 dropdown-toggle" @click.prevent="toggleOpen">
      {{ title }}
    </a>
    <ul class="dropdown-menu" :style="{ display: 'block' }" v-if="isOpen">
      <slot></slot>
    </ul>
  </div>
</template>
<script lang="ts" setup>
import { onMounted, onUnmounted, ref } from "vue";

const dropdownRef = ref<null | HTMLElement>(null);
const handler = (e: MouseEvent) => {
  if (dropdownRef.value) {
    if (!dropdownRef.value.contains(e.target as HTMLElement) && isOpen.value) {
      isOpen.value = false;
    }
  }
};

onMounted(() => {
  document.addEventListener("click", handler);
});
onUnmounted(() => {
  document.removeEventListener("click", handler);
});

const props = defineProps({
  title: {
    type: String,
    required: true,
  },
});

const isOpen = ref(false);
const toggleOpen = () => {
  isOpen.value = !isOpen.value;
};
</script>
<style scoped>
/* code... */
</style>
