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
  value: {
    type: String,
    required: false,
  }
});

const values = inject('values', {});

const handleChange = (e) => {
  values[props.name] = e.target.value;
};
</script>

<template>
    <component :is="as" :name="name" :value="values[name]" @input="handleChange">
      <slot />
    </component>
</template>

<style scoped>

</style>