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
  font-size: 13px;
  font-weight: 600;
  color: #8ea4b5;
  text-transform: unset;
  border-bottom: none;
  border-top: none;
  vertical-align: middle;
  height: 52px;
  white-space: nowrap;
  vertical-align: middle;
}
</style>
