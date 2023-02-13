<template>
    <div class="input">
        <span>{{ label }}</span>
        <br>
        <input :type="type_inp" :value="modelValue" @input="$emit('update:modelValue', $event.target.value)">
        <div v-if="!valid && error_message">
            <span class="error-message">{{ error_message }}</span>
        </div>
    </div>
</template>

<script>
export default {
    name: 'resumeInput',
    props: {
        modelValue: String,
        label: String,
        error_message: String,
        type_inp:{
            type:String,
            default: "span"
        },
        regex: {
            type: String,
            default: ""
        }
    },
    computed: {
        valid() {
            if (this.modelValue) {
                return new RegExp(this.regex).test(this.modelValue)
            }
            return true;
        },
    },
    emits: ['update:modelValue']
}
</script>
