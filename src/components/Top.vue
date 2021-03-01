<template>
  <v-container>
    <InputForm 
      formRounded="xl"
      :formElevation="formElevation"
      @storeMovie="storeMovie"
    />
    <Movies
      ref="movies"
      :movie-ittems="movieItems"
    />
  </v-container>
</template>

<script>
  import InputForm from './InputForm';
  import Movies from './Movies';
  import axios from 'axios';

  export default {
    name: 'Top',
    components: {
      InputForm,
      Movies,
    },

    data() {
      return {
        formElevation: "10",
        movieItems: [{}],
      }
    },

    created() {
      this.getMovies()
    },

    methods: {
      getMovies() {
        axios.get('https://youtube-curation.herokuapp.com/rest/1'
        ).then((response) => {
          this.movieItems = response.data.user.movies
        }).cattch((error) => {
          console.log(error)
        }).finally(() => {
          this.$refs.movies.init()
        })
      },
      storemovie(movieUrl, comment) {
        console.log(movieUrl, comment)
      },
    },
  }
</script>