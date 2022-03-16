<template>
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
</template>

<script>
export default {
  name: 'cardAlbum',
  props: {
    album: Object
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
