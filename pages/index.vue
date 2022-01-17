
<template>
<div class="home">
  <!-- Hero -->
  <Hero/>

  <!-- Movies -->
  <div class="container movies">
    <div id="movie-grid" class="movie-grid">
      <div class="movie" v-for="(movie, index) in movies" :key="index" >
        <div class="movie-img">
          <img :src="`https://image.tmdb.org/t/p/${movie.poster_path}`" alt="">
          <p class="review">{{movie.vote_average}}</p>
          <p class="overview">{{movie.overview}}</p>

        </div>
        <div class="info">
          <p class="title">{{movie.title.slice(0, 25) }}
            <span v-if="movie.title.length > 25">...</span>
          </p>
           <p class="release">
              Released:
              {{
                new Date(movie.release_date).toLocaleString('en-us', {
                  month: 'long',
                  day: 'numeric',
                  year: 'numeric',
                })
              }}
            </p>
            <NuxtLink class="button button-light" 
              :to="{name: 'movies-movieid', params: {movieid: movie.id}}"
            > Get more Info
            </Nuxtlink>
        </div>

      </div>

    </div>
  </div>

</div>
</template>

<script>
import axios from 'axios'
export default {
  data(){
    return {
      movies: [],
    }
  },
  async fetch(){
    await this.getMovies()

  },
  methods: {
    async getMovies() {
      const data = axios.get(
        'https://api.themoviedb.org/3/movie/550?api_key=fed76c248a19167c38ad419355118e0e&language=en-US&page=1'
      )
      const result = await data

      result.data.results.forEach((movie) => {
        this.movies.push(movie)
      })
      // eslint-disable-next-line no-console
      console.log(this.movies)
      },
  
},
}
</script>
