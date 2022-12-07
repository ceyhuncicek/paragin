<template>
  <tr class="table__row">
    <slot />
  </tr>
</template>
<script>
export default {
  name: 'TableRow',
};
</script>
<style scoped>
tr:nth-child(even) {
  background-color: #f2f2f2;
}
</style>
