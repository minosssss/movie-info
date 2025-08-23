<template>
  <Navbar />
  <Event :text="text"/>
  <SearchBar v-model="query"/>
  <Movies :data="viewData" @showDetail="showDetail" @increaseLike="increaseLike" @closeModal="closeModal"/>
  <Modal :isModal="isModal" :selectedData="selectedData" @closeModal="isModal = false"/>
</template>

<script>
import mock from './assets/movies';
import Navbar from "@/components/Navbar.vue";
import EventItem from "@/components/EventItem.vue";
import Modal from "@/components/Modal.vue"; // 영화 데이터
import Movies from "@/components/Movies.vue";
import SearchBar from "@/components/SearchBar.vue";
import data from "@/assets/movies";
export default {
  name: 'App',
  data() {
    return {
      isModal: false,
      data: mock,
      query: '',
      selectedData: null,
      text:"NETFLIX 강렬한 운명의 드라마, 경성크리처"
    }
  },
  computed: {
    // 화면에 뿌릴 리스트(필터링 규칙은 여기서 관리)
    viewData() {
      const query = this.query.trim().toLowerCase()
      if (!query) return this.data
      const results = data.filter(item => item.title.includes(query));
      // 여기서 “1개 이상이면 바꿔 보여주기”가 자연스럽게 만족됨
      // (0개면 빈 목록, 필요하면 원본으로 되돌릴 수도 있음)
      if (results.length === 0) {
        return [];
      }
      return results.length > 0 && results // 0개일 땐 원본 유지하려면 이 라인 유지
    },
  },

  methods: {
    increaseLike(viewIndex) {
      // viewData의 인덱스를 data 매핑해서 원본을 수정
      const movieInView = this.viewData[viewIndex]
      const idx = this.data.indexOf(movieInView)
      if (idx !== -1) this.data[idx].like += 1
      // 👇 더 안전하게 하려면 각 항목에 id를 두고 findIndex(id)로 찾는 걸 추천
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
  },
  components: {
    Navbar: Navbar,
    Modal: Modal,
    Event: EventItem,
    Movies: Movies,
    SearchBar: SearchBar,
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