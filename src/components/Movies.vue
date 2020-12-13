<template>
  <v-row>
    <template
      v-if="loading"
    >
      <v-container
        class="px-10 py-10"
        style="text-align:center"
      >
        <v-progress-circular
          size="70"
          color="blue"
          indeterminate
        />
      </v-container>
    </template>
    <template
      v-else
    >
      <v-col
        v-for="item in movieInternalItems" :key="item.id"
        cols="12"
        sm="6"
        md="4"
        style="text-align: center"
      >
        <div>
          <iframe
            :src="item.url"
            width="290"
            height="163.125"
            frameborder="0"
          />
          <p>{{ item.comment }}</p>
        </div>
      </v-col>
    </template>
  </v-row>
</template>

<script>
	export default {
    props: {
      movieItems: {
        type: Array,
        default: null,
      },
      loading: {
        type: Boolean,
        required: true,
        default: true,
      },
    },

    data () {
      return {
        movieInternalItems: {},
      }
    },

    methods: {
      // 動画の初期表示処理
      init () {
        this.movieInternalItems = []
        Object.keys(this.movieItems[0]).forEach(i => {
          const newItem = {
            id: this.movieItems[0][i].url,
            url: 'https://www.youtube.com/embed/' + this.movieItems[0][i].url + '?controls=1&loop=1&playlist=' + this.movieItems[0][i].url,
            comment: this.movieItems[0][i].comment,
          }
          this.movieInternalItems.push(newItem)
        })
      },
    },
  }
</script>
