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
        Object.keys(this.movieItems).forEach(i => {
          const newItem = {
            id: this.movieItems[i].id,
            url: 'https://www.youtube.com/embed/' + this.movieItems[i].url + '?controls=1&loop=1&playlist=' + this.movieItems[i].url,
            comment: this.movieItems[i].comment,
          }
          this.movieInternalItems.push(newItem)
        })
        this.movieInternalItems.sort(this.descending)
      },
      // IDの降順に並び換え
      descending (a, b) {
        let comparison = 0
        if (a.id > b.id) {
          comparison = -1
        } else if (b.id > a.id) {
          comparison = 1
        }
        return comparison
      },
    },
  }
</script>
