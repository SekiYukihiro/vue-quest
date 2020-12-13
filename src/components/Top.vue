<template>
	<v-container>
    <input-form
      formRounded="xl"
      :formElevation="formElevation"
      @storeMovie="storeMovie"
    />
    <movies
      ref="movies"
      :movie-items="movieItems"
    />
  </v-container>
</template>

<script>
  import InputForm from './InputForm.vue'
  import Movies from './Movies.vue'
  import axios from 'axios'

	export default {
    components: {
      InputForm,
      Movies,
    },

    data () {
      return {
        formElevation: "10",
        movieItems: {},
      }
    },

    created () {
      this.getMovies()
    },

    methods: {
      async getMovies () {
        await axios.get('https://youtube-curation.herokuapp.com/rest/1'
        ).then((response) => {
          this.movieItems = [Object.assign({}, response.data.user.movies)]
        }).catch((error) => {
          console.log(error)
        }).finally(() => {
          this.$refs.movies.init() 
        })
      },
      storeMovie (movieUrl, comment) {
        console.log(movieUrl, comment)
      }
    },
  }
</script>
