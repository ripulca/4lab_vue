<template>
    <div class="select-box">
      <span>{{label}}</span>
      <br>
      <select @input="$emit('update:modelValue', $event.target.value)">
        <option v-for="(option, index) in options" v-bind:key="index" 
        :value="option">
          {{ option }}
        </option>
      </select>
    </div>
  </template>
  
  <script>
  export default {
    name: 'resumeSelect',
    props: {
      label: String,
      modelValue: String,
      options: Array
    },
    emits: ['update:modelValue']
  }
  </script>