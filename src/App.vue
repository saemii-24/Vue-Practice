<template>
  <Navbar />
  <Event :text="text" />
  <SearchBar :data="data_temp" @searchMovie="searchMovie($event)" />
  <p>
    <button @click="showAllMovie">전체보기</button>
  </p>
  <Movies
    :data="data_temp"
    @openModal="
      isModal = true;
      selectedMovie = $event;
    "
    @increaseLike="increaseLike($event)"
  />
  <Modal
    :data="data"
    :isModal="isModal"
    :selectedMovie="selectedMovie"
    @closeModal="isModal = false"
  />
</template>

<script>
// 자바스크립트코드
import data from "./assets/movies";
import Navbar from "./components/Navbar.vue";
import Modal from "./components/Modal.vue";
import Event from "./components/Event.vue";
import Movies from "./components/Movies.vue";
import SearchBar from "./components/SearchBar.vue";

export default {
  name: "App",
  data() {
    return {
      isModal: false,
      textRed: "color: black",
      data,
      data_temp: [...data],
      selectedMovie: 0,
      text: "짱구는 못말려 몰아보기 이벤트 진행중!",
    };
  },
  methods: {
    increaseLike(id) {
      // this.data[i].like += 1;
      this.data.find((movie) => {
        if (movie.id == id) {
          movie.like += 1;
        }
      });
    },
    searchMovie(title) {
      this.data_temp = this.data_temp.filter((movie) => {
        return movie.title.includes(title);
      });
    },
    showAllMovie() {
      this.data_temp = [...this.data];
    },
  },
  components: {
    Navbar: Navbar,
    Modal: Modal,
    Movies: Movies,
    Event: Event,
    SearchBar: SearchBar,
  },
};
</script>

<style>
/* css작성하기 */

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
  background: rgba(0, 0, 0, 0.3);
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
