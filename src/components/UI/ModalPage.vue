<template>
  <div class="modal" v-if="show" @click="hideModal">
    <div @click.stop class="modal_content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ModalPage',
  props: {
    show: {
      type: Boolean,
      default: false,
    }
  },
  methods: {
    hideModal() {
      this.$emit('update:show', false);
    }
  }
}
</script>

<style>
.modal {
  top: 0;
  bottom: 0;
  right: 0;
  left: 0;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  display: flex;
}
.modal_content {
  margin: auto;
  background: white;
  min-width: 500px;
  min-height: 100px;
  padding: 15px;
}
</style>