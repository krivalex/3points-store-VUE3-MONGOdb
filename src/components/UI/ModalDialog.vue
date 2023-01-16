<template>
  <div class="dialog" @click="hideModel">
    <div class="dialog-client">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: 'modalDialog',
  methods: {
    hideModel() {
      this.$emit('hideModel');
    }
  },
  emits: ['hideModel']
}
</script>

<style scoped>
.dialog {
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  display: flex;
}

.dialog-client {
  margin: auto;
  background: white;
  border-radius: 12px;
  min-height: 50px;
  min-height: 300px;
}
</style>
