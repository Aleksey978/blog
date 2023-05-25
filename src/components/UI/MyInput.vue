<script>
import { toHandlers } from 'vue';

export default {
  name: 'my-input',
  props: {
    modelValue: [String, Number]
  },
  methods: {
    updateInput(ev) {
      this.$emit('update:modelValue', ev.target.value)
    }
  }
}
</script>

<template>
  <input :value="modelValue" @input="updateInput" class="input" type="text">
</template>

<style>
.input {
  width: 100%;
  height: 50px;
  border: 1px solid teal;
  margin-top: 15px;
  padding: 15px;
  outline: none;
}
</style>