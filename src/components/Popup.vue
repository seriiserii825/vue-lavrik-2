<template>
  <div class="popup">
    <div class="popup-content">
      <button type="button" class="close" @click="$emit('hide-popup')">x</button>
      <h3>Check data</h3>
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {}
</script>

<style>
.popup {
  position: fixed;
  top: 0;
  left: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 100vh;
  z-index: 100;
}
.popup-content {
  position: relative;
  padding: 1rem 1rem 1rem;
  width: 30rem;
  background-color: white;
  z-index: 102;
}
.popup-content h3 {
  margin-bottom: 1rem;
}
.popup .close {
  position: absolute;
  top: 1rem;
  right: 1rem;
}
.popup .buttons button {
  margin-right: 0.5rem;
}
</style>
