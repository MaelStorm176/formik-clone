<script setup>

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

// if form is submitted, validate the form
const handleSubmit = () => {
  validate();
};

// execute function onSubmit if handleSubmit is called
const onSubmit = () => {
  props.onSubmit(values);
};
</script>

<template>
    <slot :validate="handleSubmit"/>
</template>

<style scoped>

</style>