<template>
  <button class="btn">
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: 'Button',
}
</script>

<style>
.btn {
  padding: 10px 15px;
  width: 130px;
  background: none;
  color: black;
  cursor: pointer;
}
</style>