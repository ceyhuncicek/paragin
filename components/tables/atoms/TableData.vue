<template>
  <td class="table__th">
    <slot />
  </td>
</template>
<script>
export default {
  name: 'TableData',
};
</script>
<style scoped>
.table__th {
  vertical-align: middle;
  padding: 10px;
}
.table__th:last-child {
  text-align: right;
  padding-right: 10px;
}
</style>
