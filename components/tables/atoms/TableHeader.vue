<template>
  <th class="table__th">
    <slot />
  </th>
</template>
<script>
export default {
  name: 'TableHeader',
};
</script>
<style scoped>
.table__th {
  color: black;
  text-align: left;
  padding: 10px;
  font-size: 13px;
  font-weight: 600;
  text-transform: unset;
  border-bottom: none;
  border-top: none;
  vertical-align: middle;
  height: 52px;
  white-space: nowrap;
  vertical-align: middle;
}
.table__th:last-child {
  text-align: right;
  padding-right: 10px;
}
</style>
