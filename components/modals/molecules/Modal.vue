<template>
  <div class="container">
    <div class="header">
      <div class="header__title">{{ title }}</div>
      <div class="header__button">
        <slot name="headerButton">
          <Button
            class="header__button--narrow"
            variant="contained"
            color="danger">
            <i class="icon fa-solid fa-xmark"></i>
          </Button>
        </slot>
      </div>
    </div>
    <div class="content">
      <slot name="content" />
    </div>
    <div class="footer">
      <div class="footer__secondary"><slot name="secondaryButton"></slot></div>
      <div class="footer__primary"><slot name="primaryButton"></slot></div>
    </div>
  </div>
</template>

<script>
import Button from '../../forms/atoms/Button';
export default {
  name: 'Modal',
  components: { Button },
  props: {
    title: {
      type: String,
      default: '',
    },
  },
};
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  background-color: var(--main-color);
  color: var(--white);
  padding: 8px;
}

.header {
  display: flex;
  justify-content: center;
  align-items: center;
  padding-bottom: 8px;
}

.content {
  background-color: var(--box-color);
  padding: 10px;
  border-bottom: 1px solid var(---box-border-outer);
}

.footer {
  display: flex;
  justify-content: space-between;
  background-color: var(--box-color);
  padding: 10px;
}

.header__title {
  font-family: Arial, Helvetica, sans-serif;
  font-size: 16px;
  flex: 1;
  display: flex;
  justify-content: center;
}

.header__button {
  display: flex;
}

.header__button .header__button--narrow {
  padding: 4px 18.5px;
}
</style>
