<script setup>
// declare props
import {provide, reactive} from "vue";

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
  initialErrors: {
    type: Object,
    required: false,
  },
});

// provide initial values to child components
const values = reactive(props.initialValues);
provide('values', values);

// provide errors to child components
const errors = reactive(props.initialErrors || {});
provide('errors', errors);

const handleSubmit = (e) => {
  e.preventDefault();
  if (props.validate) {
    const errorsValues = props.validate(values);
    if (Object.keys(errorsValues).length > 0) {
      Object.assign(errors, errorsValues);
      return;
    }
  }
  props.onSubmit(values);
};

</script>

<template>
  <form @submit.prevent="handleSubmit">
    <slot />
  </form>
</template>

<style scoped>

</style>