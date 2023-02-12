<template>
    <div class="input">
      <span>{{label}}</span>
      <br>
      <input type="span" :value="modelValue"
      @input="$emit('update:modelValue', $event.target.value)">
      <br v-if="!valid && error_message">
      <span v-if="!valid && error_message" class="error-message">{{error_message}}</span>
    </div>
  </template>
  
  <script>
  export default {
    name: 'resumeInput',
    props: {
      modelValue: String,
      label: String,
      error_message: String,
      regex: {
          type: String,
          default: ""
        }
    },
    computed: {
      valid() {
        return new RegExp(this.regex).test(this.modelValue)
      },
    },
    emits: ['update:modelValue']
  }
  </script>
  