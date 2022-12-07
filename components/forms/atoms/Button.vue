<template>
  <button
    class="btn"
    :class="{
      '--contained': this.variant === 'contained',
      '--outlined': this.variant === 'outlined',
      '--border-1x': this.borderRadius === '1x',
      '--main': this.color === 'main',
      '--link': this.color === 'link',
      '--danger': this.color === 'danger',
      '--text-main': this.color === 'main' && this.variant === 'outlined',
      '--text-link': this.color === 'link' && this.variant === 'outlined',
      '--text-danger': this.color === 'danger' && this.variant === 'outlined',
    }"
    v-on="$listeners">
    <slot></slot>
  </button>
</template>

<script>
export default {
  name: 'Button',
  props: {
    variant: {
      type: String,
      default: 'text',
      validator: (value) => ['text', 'contained', 'outlined'].includes(value),
    },
    borderRadius: {
      type: String,
      default: 'none',
      validator: (value) => ['none', '1x', '20x'].includes(value),
    },
    color: {
      type: String,
      default: 'main',
      validator: (value) => ['main', 'link', 'danger'].includes(value),
    },
  },
};
</script>

<style scoped>
.btn {
  color: var(--white);
  border: none;
  border-radius: 0px;
  padding: 8px 10.5px;
  font-size: 16px;
  cursor: pointer;
}

.--contained {
  background-color: var(--general-error);
}

.--main {
  background-color: var(--main-color);
}

.--link {
  background-color: var(--link-color);
}

.--danger {
  background-color: var(--general-error);
}

.--text-main {
  color: var(--main-color);
  border: 1px solid var(--main-color);
}

.--text-link {
  color: var(--link-color);
  border: 1px solid var(--link-color);
}

.--text-danger {
  color: var(--general-error);
  border: 1px solid var(--general-error);
}

.--outlined {
  background-color: transparent;
}

.--border-1x {
  border-radius: 3px;
}
</style>
