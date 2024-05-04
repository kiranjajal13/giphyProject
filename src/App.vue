<template>
  <div :class="classes" class="container">
    <div id="app">
      <appTheme @theme="onThemeChange"></appTheme>
      <search-gif @gifKeyword="onInput"></search-gif>
      <gifsList :gifs="gifs"></gifsList>
    </div>
  </div>
</template>

<script>
import SearchGif from './components/searchGif.vue'
import gifsList from './components/gifsList.vue'
import appTheme from './components/appTheme.vue'
import { API_KEY } from './constants/index'

export default {
  name: 'App',
  components: {
    SearchGif,
    gifsList,
    appTheme
  },
  data() {
    return {
      gifs: [],
      classes: [],
      offset: 0,
      keyword: ''
    }
  },
  beforeMount() {
    this.fetchInitialGifs()
  },
  mounted() {
    this.fetchNewGifs()
  },
  methods: {
    async fetchInitialGifs() {
      const response = await fetch(`https://api.giphy.com/v1/gifs/search?api_key=${API_KEY}&limit=50`)
      const gifData = await response.json()
      this.totalItems = gifData?.pagination?.total_count
      this.gifs = [...this.gifs, ...gifData.data]
    },
    async onInput(keyword) {
      this.keyword = keyword
      const response = await fetch(`https://api.giphy.com/v1/gifs/search?api_key=${API_KEY}&q=${keyword}&limit=50&offset=0`)
      const gifData = await response.json()
      this.totalItems = gifData.pagination.total_count
      this.gifs = [...this.gifs, ...gifData.data]
    },
    async fetchNewGifs() {
        this.offset+=50
        window.onscroll = async () => {
          let bottomOfWindow = document.documentElement.scrollTop + window.innerHeight === document.documentElement.offsetHeight;
          if (bottomOfWindow) {
            const response = await fetch(`https://api.giphy.com/v1/gifs/search?api_key=${API_KEY}&q=${this.keyword}&limit=50&offset=${this.offset}`)

            this.offset+=50

            const newGifs = await response.json()

            this.gifs = [...this.gifs, ...newGifs?.data]
            console.log("after: ",this.gifs)
          }
        }
    },
    onThemeChange(theme) {
      if(theme === 'dark') {
        this.classes = ['darkTheme']
      } else {
        this.classes = []
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.container {
  width: 100%;
}
.darkTheme {
  background-color: grey;
}
</style>
