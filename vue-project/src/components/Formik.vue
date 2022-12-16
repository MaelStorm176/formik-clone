<script setup>
import {provide, reactive, toRefs} from "vue";

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

const values = reactive(props.initialValues);

const updateSingleValue = (name, value) => {
  values[name] = value;
};

provide('values', {...toRefs(values), updateSingleValue});

// provide errors to child components
const errors = reactive(props.initialErrors || {});
provide('errors', errors);

const handleSubmit = (e) => {
  console.log(values, props.initialValues);
  e.preventDefault();
  if (props.validate) {
    const errorsValues = props.validate(values);
    if (Object.keys(errorsValues).length > 0) {
      Object.assign(errors, errorsValues);
      console.log(errors);
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