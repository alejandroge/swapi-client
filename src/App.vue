<template>
  <div id="app">
    <div class="headers">
      <span>Episode</span>
      <span>Title</span>
      <span>Release Date</span>
      <span>Director</span>
      <span>Producer</span>
    </div>
    <div v-for="film in films" :key="film.id" class="film">
      <span>{{ film.episode_id }}</span>
      <span>{{ film.title }}</span>
      <span>{{ getDate(film.release_date) }}</span>
      <span>{{ film.director }}</span>
      <span>{{ film.producer }}</span>
      <div class="wrapper">
        <div class="poster">
          <template v-if="!film.photo_url">
            <label :for="`photo_url${film.id}`">Photo URL: </label>
            <input type="text" name="photo-url" :id="`photo_url${film.id}`" v-model="photoUrls[film.id]">
            <button type="submit" @click="submitPhoto(film)">Save photo</button>
          </template>
          <img v-else :src="film.photo_url" alt="Poster" width="250">
        </div>
        <div class="opening-crawl">
          {{ film.opening_crawl }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import { format, parseISO } from 'date-fns'

export default {
  name: 'App',
  data() {
    return {
      loading: false,
      films: [],
      photoUrls: {}
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
  methods: {
    getDate(date) {
      return format(parseISO(date), 'MMMM do, yyyy');
    },
    submitPhoto(film) {
      axios.post(
        `http://localhost:3000/swapi_films/${film.id}/submit_photo`,
        { photo_url: this.photoUrls[film.id] }
      ).then(() => {
        film.photo_url = this.photoUrls[film.id]
      }).catch((error) => {
        console.log(error)
      });
    }
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
    width: 20%;
  }

  .film span:nth-of-type(2),
  .headers span:nth-of-type(2) {
    width: 20%;
  }

  .film span:nth-of-type(3),
  .headers span:nth-of-type(3) {
    width: 20%;
  }

  .film span:nth-of-type(4),
  .headers span:nth-of-type(4) {
    width: 20%;
  }

  .film span:nth-of-type(5),
  .headers span:nth-of-type(5) {
    width: 20%;
  }

  .film {
    margin-bottom: 10px;
    border-bottom: 1px solid black;
  }

  .headers {
    border-bottom: 2px solid black;
    margin-bottom: 10px;
  }

  .opening-crawl {
    display: -webkit-inline-box !important;
    -webkit-line-clamp: 4;
    -webkit-box-orient: vertical;
    overflow: hidden;
    text-overflow: ellipsis;
    width: 60%;
  }

  .poster {
    width: 30%;
  }

  .wrapper {
    margin: 10px 0px;
    display: flex;
    align-items: center;
  }
</style>
