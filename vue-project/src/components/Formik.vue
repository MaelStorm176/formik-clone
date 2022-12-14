<script setup>
// declare props
const props = defineProps({
  initialValues: {
    type: Object,
    required: true,
  },
  onSubmit: {
    type: Function,
    required: true,
  },
  validate: {
    type: Function,
    required: false,
  },
});

</script>

<template>
  <form @submit.prevent="onSubmit">
    <slot :values="values" />
  </form>
</template>

<style scoped>

</style>