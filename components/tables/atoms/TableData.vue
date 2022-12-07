<template>
  <td class="table__td">
    <slot />
  </td>
</template>
<script>
export default {
  name: 'TableData',
};
</script>
<style scoped>
.table__td {
  vertical-align: middle;
  padding: 10px;
}
.table__td:last-child {
  text-align: right;
  padding-right: 10px;
}
</style>
