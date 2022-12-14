<script setup>

import {inject} from "vue";

const allowedInputTypes = ["text", "email", "password", "tel", "number", "checkbox"];
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
  },
  label: {
    type: String,
    required: false,
  },
});

const values = inject('values');
const errors = inject('errors');
</script>

<template>
  <div>
    <label v-if="label" :for="name">{{ label }}</label>
    <input v-if="allowedInputTypes.includes(as)" :id="name" :name="name" :type="as" :value="values[name]" @input="$emit('input', $event.target.value)"/>
    <component :is="as" v-else :name="name" :value="values[name]" @input="$emit('input', $event)">
      <slot />
    </component>
    <small v-if="errors && errors[name]" style="color: red">{{ errors[name] }}</small>
  </div>
</template>

<style scoped>

</style>