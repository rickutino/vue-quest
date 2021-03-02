<template>
  <v-container>
    <InputForm 
      formRounded="xl"
      :formElevation="formElevation"
      @storeMovie="storeMovie"
    />
    <v-messages
      :value="responseError"
      color="red"
      class="response-error my-5 text-center"
    />
    <Movies
      ref="movies"
      :movie-items="movieItems"
      :loading="loading"
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
        responseError:[],
        loading: true,
      }
    },

    created() {
      this.getMovies()
    },

    methods: {
      init() {
        this.movieInternalItems = []
        Object.keys(this.movieItems).forEach(index => {
          const newItem = {
          id: this.movieItems[index].id,
          url: 'https://www.youtube.com/embed/' + this.movieItems[index].url + '?controls=1&loop=1&playlist=' + this.movieItems[index].url,
          comment: this.movieItems[index].comment,
          }
          this.movieInternalItems.push(newItem);
        })
        this.movieInternalItems.sort(this.descending);
      },
      descending(a,b) {
        let comparison = 0
        if(a.id > b.id) {
          comparison - 1
        } else if(b.id > a.id) {
          comparison = 1
        }
        return comparison
      },
      getMovies() {
        axios.get('https://youtube-curation.herokuapp.com/rest/1'
        ).then((response) => {
          this.movieItems = response.data.user.movies
        }).catch((error) => {
          console.log(error)
          this.responseError = ['動画の取得に失敗しました']
        }).finally(() => {
          setTimeout(() => {
            this.loading = false
          }, 1000)
          this.$refs.movies.init()
        })
      },
      storeMovie(movieUrl, comment) {
        console.log(movieUrl, comment)
      },
    },
  }
</script>

<style>
  .response-error .v-messages__message {
    font-size: 18px;
  }
</style>