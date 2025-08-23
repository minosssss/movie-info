<script>
import {defineComponent} from 'vue'

export default defineComponent({
  name: "MoviesComponent",
  props: {
    data: Array,
  },
  emits: ['increaseLike', 'showDetail', 'closeModal'],
})
</script>

<template>
  <h1>영화정보</h1>
  <div v-for="(movie, i) in data" :key="i" class="item" @keyup.esc="$emit('closeModal')">
    <figure>
      <img :src="`${movie.imgUrl}`" :alt="movie.title">
    </figure>
    <div class="info">
      <h3 class="bg-yellow">{{ movie.title }}</h3>
      <p>개봉: {{ movie.year }}</p>
      <p>장르: {{ movie.category }}</p>
      <button @click="$emit('increaseLike',i)">좋아요
      </button>
      <span>{{ movie.like }}</span>
      <p>
        <button @click="$emit('showDetail', movie)">상세보기</button>

      </p>
    </div>
  </div>
</template>

<style scoped>

</style>