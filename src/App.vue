<template>
  <div class="container">
    <h1>Top 100 Albuns</h1>
    <searchBar @search-submitted="filter"></searchBar>
    <p v-if="!albuns.length" style="text-align:center;">Getting some coffee, please wait...</p>
    <div style="text-align:center; margin-bottom: 20px;">
      <!-- TODO Turn these buttons into a nice togle -->
      <button @click="displayStyle='cardGrid'" class="btn-all btn-prim"><font-awesome-icon icon="fa-solid fa-border-all" size="xl"/></button>
      <button @click="displayStyle='cardList'" class="btn-all btn-prim"><font-awesome-icon icon="fa-solid fa-list" size="xl"/></button>
    </div>
    <div class="flex-wrap">
      <component :is="displayStyle"
        v-for="album in albuns"
        :key="album.id"
        :album="album">
      </component>
    </div>
  </div>
</template>

<script>
import cardGrid from './components/cardGrid.vue'
import searchBar from './components/searchBar.vue'

export default {
  name: 'App',
  components: {
    cardGrid,
    searchBar
  },
  data: () => ({
    albuns: [],
    displayStyle: 'cardGrid'
  }),
  created: function () {
    fetch('https://itunes.apple.com/us/rss/topalbums/limit=100/json')
      .then(response => response.json())
      .then(data => {
        this.albuns = data.feed.entry.map(entry => {
          return {
            id: entry.id.attributes['im:id'],
            title: entry['im:name'].label,
            artist: entry['im:artist'].label,
            url: entry.id.label,
            coverURL: entry['im:image'][2].label,
            display: true
          }
        })
      })
  },
  methods: {
    filter(content) {
      if (content) {
        this.albuns.forEach(album => {
          if (album.title.toLowerCase().includes(content.toLowerCase()) || album.artist.toLowerCase().includes(content.toLowerCase()))
            album.display = true;
          else
            album.display = false;
        })
      } else {
        this.albuns.forEach(album => { album.display = true; })
      }
    }
  }
  // computed: {
  //   albunsDisplay: {
  //     get: function () {
  //       return this.albuns
  //     },
  //     set: function (searchContent) {
  //       if (!searchContent)
  //         return this.albuns
  //       return this.albuns.map(album => {
  //         return album.title.toLowerCase().includes(searchContent.toLowerCase()) || album.artist.toLowerCase().includes(searchContent.toLowerCase())
  //       })
  //     }
  //   }
  // }
}
</script>

<style>
  /* Check style/index.css */
</style>
