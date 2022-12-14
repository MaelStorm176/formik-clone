<script setup>
//create formik for vue 

import { defineProps, defineEmits, defineExpose, VueElement, Vue } from 'vue'

const props = defineProps({
    name: {
        type: String,
        required: true
    },
    as: {
        type: String,
        required: true
    }
})

const emits = defineEmits(['update:modelValue'])

const value = 'value'

const updateValue = (value) => {
    emits('update:modelValue', value)
}

Vue.components('input', {
    props: {
        name: {
            type: String,
            required: true
        }
    },
    emits: ['update:modelValue'],
    setup(props, { emit }) {
        const value = 'value'

        const updateValue = (value) => {
            emit('update:modelValue', value)
        }

        return {
            value,
            updateValue
        }
    },
    template: `
        <div>
            <label for={props.name}>{props.name}</label>
            <input
                type="text"
                name={props.name}
                value={value}
                onInput={(e) => updateValue(e.target.value)}
            />
        </div>
    `
})

Vue.components('textarea', {
    props: {
        name: {
            type: String,
            required: true
        }
    },
    emits: ['update:modelValue'],
    setup(props, { emit }) {
        const value = 'value'

        const updateValue = (value) => {
            emit('update:modelValue', value)
        }

        return {
            value,
            updateValue
        }
    },
    template: `
        <div>
            <label for={props.name}>{props.name}</label>
            <textarea
                name={props.name}
                value={value}
                onInput={(e) => updateValue(e.target.value)}
            />
        </div>
    `
})

const components = {
    input: Vue.components('input'),
    textarea: Vue.components('textarea')
}

const Component = components[props.as]
</script>

<template>
    <div>
        <label for={props.name}>{props.name}</label>
        <Component />
    </div>
</template>