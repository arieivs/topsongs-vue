<template>
  <div class="container">
    <h1>Top 100 Albuns</h1>
    <searchBar @search-submitted="filter"></searchBar>
    <p v-if="!albuns.length" style="text-align:center;">Getting some coffee, please wait...</p>
    <div class="flex-wrap">
      <cardAlbum v-for="album in albuns"
        :key="album.id"
        :album="album">
      </cardAlbum>
    </div>
  </div>
</template>

<script>
import cardAlbum from './components/cardAlbum.vue'
import searchBar from './components/searchBar.vue'

export default {
  name: 'App',
  components: {
    cardAlbum,
    searchBar
  },
  data: () => ({
    albuns: []
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
}
</script>

<style>
</style>
