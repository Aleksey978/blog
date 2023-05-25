<script>
export default {
  name: 'my-button'
}
</script>

<template>
  <button class="btn">
    <slot></slot>
  </button>
</template>

<style>
.btn {
  background: teal;
  border: none;
  padding: 15px;
  color: white;
  cursor: pointer;
}
</style>