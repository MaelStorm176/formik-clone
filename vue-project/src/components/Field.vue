<script setup>
const props = defineProps({
  name: {
    type: String,
    required: true,
  },
  as: {
    type: String,
    required: false,
    default: 'input',
  },
});
</script>

<template>
  <component :is="as" :name="name" />
</template>

<style scoped>

</style>