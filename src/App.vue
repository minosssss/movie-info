<template>
  <h1>영화정보</h1>
  <div v-for="(movie, i) in data" :key="i" class="item" @keyup.esc="isModal=false">
    <figure>
      <img :src="`${movie.imgUrl}`" :alt="movie.title">
    </figure>
    <div class="info">
      <h3 class="bg-yellow">{{ movie.title }}</h3>
      <p>개봉: {{ movie.year }}</p>
      <p>장르: {{ movie.category }}</p>
      <button @:click="increseLike(i)">좋아요
      </button>
      <span>{{ movie.like }}</span>
      <p>
        <!-- 상세보기 버튼 클릭시 해당 영화 데이터를 selectedData에 저장 -->
        <button @click="showDetail(movie)">상세보기</button>
      </p>
    </div>
  </div>

  <div class="modal" v-if="isModal"  tabindex="0">
    <div class="inner">
      <h3>{{ selectedData.title }}</h3>
      <img :src="selectedData.imgUrl" :alt="selectedData.title" style="width: 200px; margin-bottom: 1rem;">
      <p><strong>개봉년도:</strong> {{ selectedData.year }}</p>
      <p><strong>장르:</strong> {{ selectedData.category }}</p>
      <p><strong>좋아요:</strong> {{ selectedData.like }}</p>
      <p><strong>감독:</strong> {{ selectedData.director }}</p>
      <p><strong>줄거리:</strong> {{ selectedData.plot }}</p>
      <button @click="closeModal">닫기</button>
    </div>
  </div>
</template>

<script>
import data from './assets/movies'; // 영화 데이터
console.log(data);

export default {
  name: 'App',
  data() {
    return {
      isModal: false,
      data,
      selectedData: null,
    }
  },
  methods: {
    increseLike(i) {
      this.data[i].like += 1;
    },
    // 상세보기 메서드
    showDetail(movie) {
      this.selectedData = movie;  // 선택된 영화 데이터 저장
      this.isModal = true;        // 모달 열기
    },
    // 모달 닫기 메서드
    closeModal() {
      this.isModal = false;
      this.selectedData = null;   // 선택 데이터 초기화 (선택사항)
    }
  }
}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
}

body {
  max-width: 768px;
  margin: 0 auto;
  padding: 20px;
}

h1,
h2,
h3 {
  margin-bottom: 1rem;
}

p {
  margin-bottom: 0.5rem;
}

button {
  margin-right: 10px;
  margin-top: 1rem;
}

.item {
  width: 100%;
  border: 1px solid #ccc;
  display: flex;
  margin-bottom: 20px;
  padding: 1rem;
}

.item figure {
  width: 30%;
  margin-right: 1rem;
}

.item img {
  width: 100%;
}

.item .info {
  width: 100%;
}

.modal {
  background: rgba(0, 0, 0, 0.7);
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal .inner {
  background: #fff;
  width: 80%;
  padding: 20px;
  border-radius: 10px;
}
</style>