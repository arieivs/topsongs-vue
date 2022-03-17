<template>
  <div class="container">
    <h1>Top 100 Albuns</h1>
    <searchBar @search-submitted="filter"></searchBar>
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
    // register components here later
  },
  data: () => ({
    albuns: [
      {
        id: '1594677532',
        title: 'Encanto (Original Motion Picture Soundtrack)',
        artist: 'Lin-Manuel Miranda, Germaine Franco, Stephanie Beatriz, Olga Merediz & Jessica Darrow',
        url: 'https://music.apple.com/us/album/encanto-original-motion-picture-soundtrack/1594677532?uo=2',
        coverURL: 'https://is4-ssl.mzstatic.com/image/thumb/Music126/v4/94/4d/9a/944d9a8d-0549-f537-5706-5b083bd84a7d/21UM1IM38949.rgb.jpg/170x170bb.png'
      },
      {
        id: '1592745677',
        title: 'Sing 2 (Original Motion Picture Soundtrack)',
        artist: 'Various Artists',
        url: 'https://music.apple.com/us/album/sing-2-original-motion-picture-soundtrack/1592745677?uo=2',
        coverURL: 'https://is5-ssl.mzstatic.com/image/thumb/Music126/v4/c2/d2/6d/c2d26dcf-7e1b-ed4c-f598-f8dcb42b0f75/21UM1IM35664.rgb.jpg/170x170bb.png'
      },
      {
        id: '1605201128',
        title: 'LION',
        artist: 'Elevation Worship',
        url: 'https://music.apple.com/us/album/lion/1605201128?uo=2',
        coverURL: 'https://is4-ssl.mzstatic.com/image/thumb/Music116/v4/be/e6/8d/bee68d7f-e72c-8673-d47a-7f65aa0ad5c3/886449816774.jpg/170x170bb.png'
      },
      {
        id: '1611504686',
        title: 'I NEVER DIE',
        artist: '(G)I-DLE',
        url: 'https://music.apple.com/us/album/i-never-die/1611504686?uo=2',
        coverURL: 'https://is1-ssl.mzstatic.com/image/thumb/Music126/v4/9c/fe/5e/9cfe5eec-89b5-240f-5229-59244360e89d/8804775250422_Cover.jpg/170x170bb.png'
      },
    ]
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
            coverURL: entry['im:image'][2].label
          }
        })
      })
  },
  methods: {
    filter(content) {
      if (!content)
        return this.albuns;
      return this.albuns.filter(album => {
        return album.title.toLowerCase().includes(content.toLowerCase()) || album.artist.toLowerCase().includes(content.toLowerCase())
      })
    }
  }
  // TODO: Change how data is pushed into albuns, check life cycle methods
  // How to use filter in a smart way? Should I copy data (original and filtered)? Add a display none?
}
</script>

<style>
/*#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}*/
</style>
