<template>
  <div class="radio-input">
    <label>
      <input
        type="radio"
        :checked="isChecked"
        :value="value"
        @change="$emit('change', $event.target.value)" />
      {{ label }}
    </label>
  </div>
</template>

<script>
export default {
  props: {
    value: {
      default: '',
    },
    label: {
      type: String,
      default: '',
    },
    radioState: {
      default: '',
    },
  },
  model: {
    prop: 'radioState',
    event: 'change',
  },
  computed: {
    isChecked() {
      return this.radioState == this.value;
    },
  },
};
</script>

<style scoped>
.radio-input {
  display: inline;
}
</style>
