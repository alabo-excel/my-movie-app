<template>
  <div class="hello">
    <header>
      <form>
        <div class="flex pt-4 justify-center">
          <input v-model="searchValue" type="text" class="rounded-xl p-2 m-3" placeholder="Enter Movie Title">
          <input v-on:click="getSearch" class="p-2 rounded-xl m-3" type="button" value="search">
        </div>
      </form>
    </header>
    <div class="md:flex flex-wrap justify-center">
      <div class="md:w-32 lg:w-48 rounded-md p-3 bg-purple-300 m-4" v-for="(movie, index) in movies" :key="index">
        <div class="">
          <img :src="img + movie.poster_path" alt="" />
        </div>
        <div>
          <p class="text-xl font-extrabold">{{ movie.title }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "movie",
  data: () => ({
    movies: [],
    img: 'https://image.tmdb.org/t/p/w500/',
    searchValue: ''
  }),
  mounted() {
    fetch(
      "https://api.themoviedb.org/3/trending/movie/week?api_key=890a77e69b7432001d5a0fb13d5c720c&language=en-US&page=5"
    )
      .then(response => response.json())
      .then(data => {
        this.movies = data.results;
      });
  },
  methods: {
    getSearch(){
          console.log(this.searchValue),
      fetch(`https://api.themoviedb.org/3/search/movie?api_key=890a77e69b7432001d5a0fb13d5c720c&language=en-US&query=${this.searchValue}&page=1&include_adult=false`)
      .then(response => response.json())
      .then(data => {
        this.movies = data.results;
      });
    }
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
