<template>
  <div class="page">
    <Modal title="Add new correction round">
      <template #content>
        <p>Modal content</p>
      </template>
      <template #secondaryButton>
        <Button variant="outlined" borderRadius="1x">Cancel</Button>
      </template>
      <template #primaryButton>
        <Button variant="contained" color="danger" borderRadius="1x">
          <i class="fas fa-exclamation-triangle"></i>
          Save this correction round
        </Button>
      </template>
    </Modal>
  </div>
</template>

<script>
import Button from '../components/forms/atoms/Button';
import Modal from '../components/modals/molecules/Modal';
export default {
  components: { Modal, Button },
  name: 'IndexPage',
};
</script>
<style>
:root {
  font-family: Arial, Helvetica, sans-serif;
  --main-color: #66aa11;
  --general-error: #cf191e;
  --text-title: #4a4a4a;
  --link-color: #3273f6;
  --white: #ffffff;
  --box-color: #fafafa;
  --box-zebra-inside: #f1f1f1;
  --box-border-outer: #ececec;
  --box-outer: #f1f1f1;
}

body {
  background-color: rgba(0, 0, 0, 0.7);
}
</style>

<style scoped>
.page {
  margin: 32px;
}
</style>
