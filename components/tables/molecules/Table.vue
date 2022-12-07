<template>
  <table class="table">
    <slot />
  </table>
</template>

<script>
export default {
  name: 'Table',
};
</script>

<style scoped>
.table {
  width: 100%;
  background-color: transparent;
  border-collapse: collapse;
  border-spacing: 0;
}
</style>
