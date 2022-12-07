<template>
  <div class="box">
    <div class="box__header">{{ title }}</div>
    <div class="box__content">
      <slot />
    </div>
  </div>
</template>

<script>
export default {
  name: 'Box',
  props: {
    title: {
      type: String,
      default: '',
    },
  },
};
</script>

<style scoped>
.box {
  background-color: var(--box-color);
  padding: 20px;
  border: 1px solid var(--box-border-outer);
}
.box__header {
  color: var(--text-title);
  font-weight: 400;
  font-size: 16px;
  margin-bottom: 20px;
}
</style>
