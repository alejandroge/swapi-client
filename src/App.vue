<template>
  <div id="app">
    <div class="headers">
      <span>Episode</span>
      <span>Title</span>
      <span>Release Date</span>
      <span>Director</span>
      <span>Producer</span>
      <span>Opening Crawl</span>
    </div>
    <div v-for="film in films" :key="film.id" class="film">
      <span>{{ film.episode_id }}</span>
      <span>{{ film.title }}</span>
      <span>{{ film.release_date }}</span>
      <span>{{ film.director }}</span>
      <span>{{ film.producer }}</span>
      <span>{{ film.opening_crawl }}</span>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'App',
  data() {
    return {
      loading: false,
      films: [],
    }
  },
  mounted() {
    this.loading = true
    axios.get('http://localhost:3000/swapi_films')
      .then((response) => {
        this.films = response.data
      })
      .catch(error => {
        console.log(error)
      })
      .finally(() => {
        this.loading = false

      })
  },
}
</script>

<style scoped>
  .film span,
  .headers span {
    display: inline-block;
  }

  .film span:nth-of-type(1),
  .headers span:nth-of-type(1) {
    width: 10%;
  }

  .film span:nth-of-type(2),
  .headers span:nth-of-type(2) {
    width: 10%;
  }

  .film span:nth-of-type(3),
  .headers span:nth-of-type(3) {
    width: 10%;
  }

  .film span:nth-of-type(4),
  .headers span:nth-of-type(4) {
    width: 10%;
  }

  .film span:nth-of-type(5),
  .headers span:nth-of-type(5) {
    width: 10%;
  }

  .film span:nth-of-type(6),
  .headers span:nth-of-type(6) {
    width: 50%;
  }
</style>
