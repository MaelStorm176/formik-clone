<script setup>
import { inject } from "vue";

const props = defineProps({
  name: {
    type: String,
    required: true,
  },
  as: {
    type: String,
    required: false,
    default: "text",
  }
});

const errors = inject('errors');
</script>

<template>
  <component v-show="errors && errors[name]" :is="as" :name="name">
    {{ errors[name] }}
  </component>
</template>

<style scoped>

</style>