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
  display: flex;
  flex-direction: column;
  overflow: scroll;
  font-size: 18px;
  margin: auto;
  background: white;
  border-radius: 12px;
  min-height: 50px;
  min-height: 300px;
  max-height: 80vh;
  max-width: 80vw;
  padding: 20px;
}
</style>
