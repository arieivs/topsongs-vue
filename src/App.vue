<template>
  <div class="container">
    <h1>Top 100 Albuns</h1>
    <searchBar @search-submitted="filter"></searchBar>
    <p v-if="!albuns.length" style="text-align:center;">Getting some coffee, please wait...</p>
    <div class="toggle">
      <button @click="displayStyle='cardsGrid'" :class="['btn-all', { 'btn-prim': displayStyle === 'cardsGrid' }]"><font-awesome-icon icon="fa-solid fa-border-all" size="xl"/></button>
      <button @click="displayStyle='cardsList'" :class="['btn-all', { 'btn-prim': displayStyle === 'cardsList' }]"><font-awesome-icon icon="fa-solid fa-list" size="xl"/></button>
    </div>

    <component :is="displayStyle"
      :albuns="albuns">
    </component>
  </div>
</template>

<script>
import searchBar from './components/searchBar.vue'
import cardsGrid from './components/cardsGrid.vue'
import cardsList from './components/cardsList.vue'

export default {
  name: 'App',
  components: {
    searchBar,
    cardsGrid,
    cardsList
  },
  data: () => ({
    albuns: [],
    displayStyle: 'cardsGrid'
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
