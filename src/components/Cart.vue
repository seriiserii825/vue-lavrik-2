<template>
  <div class="cart">
    <div>Price: {{ price }}</div>
    <div>Quantity: {{ cnt }}</div>
    <div>Total: {{ price * cnt }}</div>
  </div>
</template>
<script>
export default {
  props: ['price', 'cnt']
}
</script>
