<template>
  <div class="modal" v-if="isModal">
    <div class="inner">
      <h3>{{ data[selectedMovie].title }}</h3>
      <p>{{ data[selectedMovie].category }}</p>
      <button @click="isModal = false">닫기</button>
    </div>
  </div>
</template>
<script>
export default {
  name: "ModalComponent",
};
</script>
<style></style>
