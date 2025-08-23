<template>
  <div class="modal" v-if="isModal">
    <div class="inner">
      <h3>{{ selectedData.title }}</h3>
      <p>영화 상세정보</p>
      {{ JSON.stringify(selectedData)}}
      <button @click="$emit('closeModal')">닫기</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "ModalComponent",
  props: {
    isModal: Boolean,
    selectedData: Number,
  }
}

</script>

<style></style>