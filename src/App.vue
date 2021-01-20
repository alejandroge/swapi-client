<template>
  <div id="app">
    <div v-for="film in films" :key="film.id">
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
