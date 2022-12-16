<script setup>
import {inject} from "vue";

const props = defineProps({
  name: {
    type: String,
    required: true,
  },
  as: {
    type: String,
    required: false,
    default: 'text',
  },
  modelValue: {
    type: String,
    required: false,
    default: '',
  },
});

const {values, updateSingleValue} = inject('values');

</script>

<template>
  <component :is="as" :name="name" @input="updateSingleValue(name, $event.target.value)">
    <slot />
  </component>
</template>

<style scoped>

</style>