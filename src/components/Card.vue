<script setup>
defineProps({
  bg: {
    type: String,
    default: 'gray-100',
  },
});
</script>

<template>
  <div :class="`${bg} p-6 rounded-lg shadow-md`">
    <slot></slot>
  </div>
</template>
