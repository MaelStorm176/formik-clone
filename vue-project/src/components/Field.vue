<script setup>

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
</script>

<template>
  <div>
    <label v-if="label" :for="name">{{ label }}</label>
    <input v-if="allowedInputTypes.includes(as)" :id="name" :name="name" :type="as" :value="value" @input="$emit('input', $event.target.value)"/>
    <component :is="as" v-else :name="name" :value="value" @input="$emit('input', $event)">
      <slot />
    </component>
  </div>
</template>

<style scoped>

</style>