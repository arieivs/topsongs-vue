<template>
  <div id="app">
    <div class="container">
      <h1>Top 100 Albuns</h1>
      <div class="card">
        <a :href="album.url" target="_blank" rel="noreferrer" class="card-link">
          <div class="card-cover">
            <img :src="album.coverURL" alt="" />
            <button class="btn-all btn-prim card-btn-play">Play</button>
          </div>
          <h2 class="card-title">{{ album.title }}</h2>
          <p class="card-artist">{{ album.artist }}</p>
        </a>
      </div>
    </div>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    // register components here later
  },
  data: () => ({
    album: {
      title: 'Encanto (Original Motion Picture Soundtrack)',
      artist: 'Lin-Manuel Miranda, Germaine Franco, Stephanie Beatriz, Olga Merediz & Jessica Darrow',
      url: 'https://music.apple.com/us/album/encanto-original-motion-picture-soundtrack/1594677532?uo=2',
      coverURL: 'https://is4-ssl.mzstatic.com/image/thumb/Music126/v4/94/4d/9a/944d9a8d-0549-f537-5706-5b083bd84a7d/21UM1IM38949.rgb.jpg/170x170bb.png'
    }
  })
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
