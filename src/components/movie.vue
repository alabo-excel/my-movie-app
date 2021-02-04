<template>
  <div class="hello">
    <div v-for="(movie, index) in movies" :key="index">
      <p>{{movie.title}}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'movie',
  data: ()=> ({
    movies: []

  }),
  mounted(){
    fetch('https://api.themoviedb.org/3/trending/movie/week?api_key=890a77e69b7432001d5a0fb13d5c720c&language=en-US&page=1')
    .then(response => response.json())
    .then(data => {
      this.movies = data.results;
    })
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
