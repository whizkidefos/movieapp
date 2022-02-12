<template>
  <div class="home">
    <HomePageBanner />
  </div>
</template>

<script>
import axios from '@nuxtjs/axios'
export default {
  name: 'IndexPage',
  head() {
    return {
      title: 'Movie App - Latest Streaming Movie Info',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Get all the latest streaming movies in theaters & online',
        },
        {
          hid: 'keywords',
          name: 'keywords',
          content: 'movies, stream, stremaing',
        },
      ],
    }
  },

  data() {
    return {
      movies: [],
      searchMovies: [],
      searchInput: ''
    }
  },

  async fetch() {
    await this.getMovies()
  },

  methods: {
    async getMovies() {
      const data = axios.get(
        `https://api.themoviedb.org/3/movie/now_playing?api_key=3eeecde7aaea8b160c2a49a41c7e1247&language=en-US&page=1`
      )
      const result = await data
      result.data.results.forEach((movie) => {
        this.movies.push(movie)
        console.log(this.movies)
      })
    },

    //   async searchMovies() {
    //   const data = axios.get(
    //     `https://api.themoviedb.org/3/search/movie?api_key=3eeecde7aaea8b160c2a49a41c7e1247&language=en-US&page=1&query=${this.searchInput}`
    //   )
    //   const result = await data
    //   result.data.results.forEach((movie) => {
    //     this.searchedMovies.push(movie)
    //   })
    // },
    clearSearch() {
      this.searchInput = ''
      this.searchedMovies = []
    },
  },
  watch: {
    searchInput() {
      console.log(this.searchInput)
    },
  },
}
</script>
