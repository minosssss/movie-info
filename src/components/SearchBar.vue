<script>
import {defineComponent} from 'vue'

export default defineComponent({
  name: "SearchBar",
  props: {
    modelValue: { type: String, default: '' }, // v-model
  },
  computed: {
    inputText: {
      get() { return this.modelValue },
      set(v) { this.$emit('update:modelValue', v) },
    },
  },
  emits: ['update:modelValue'],

})
</script>

<template>
  <div class="search-box">
    <input
        type="search"
        placeholder="검색어 입력"
        v-model.trim="inputText"
    >
    <button @click="$emit('update:modelValue', inputText)">검색</button>
  </div>
  <p>{{ inputText }}</p>
</template>
<style>
.search-box {
  padding: 10px;
  display: flex;
  justify-content: center;
}

.search-box input {
  padding: 5px 10px;
}

.search-box button {
  margin: 0;
}
</style>