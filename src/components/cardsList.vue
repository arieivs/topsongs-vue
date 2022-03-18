<template>
  <div class="small-container">
    <div v-for="album in albuns"
          :key="album.id"
          v-show="album.display"
          class="card">
      <a :href="album.url" target="_blank" rel="noreferrer" class="card-link">
        <div class="card-content">
          <div class="card-cover">
            <img :src="album.coverURL" alt="" />
            <buttonPrimary :content="'Play'" class="card-btn-play"></buttonPrimary>
          </div>
          <div>
            <h2 class="card-title">{{ album.title }}</h2>
            <p class="card-artist">{{ album.artist }}</p>
          </div>
        </div>
      </a>
    </div>
  </div>
</template>

<script>
import buttonPrimary from './buttonPrimary.vue'

export default {
  name: 'cardsList',
  components: {
    buttonPrimary
  },
  props: {
    albuns: Object
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .card {
    margin: 15px auto;
  }

  .card-link {
    text-decoration: none;
  }

  .card-content {
    display: flex;
    align-items: center;
  }

  .card-cover {
    position: relative;
    margin-right: 20px;
  }

  .card-cover img {
    border-radius: 5px;
  }

  .card-link:hover .card-cover img {
    filter: brightness(50%);
  }

  .card-btn-play {
    position: absolute;
    left: 48px;
    top: 63px;
    opacity: 0;
  }

  .card-link:hover .card-btn-play {
    opacity: 1;
    cursor: pointer;
  }

  .card-title {
    display: inline-block;
    font-size: 16px;
    color: #fff;
    margin: 5px 0;
  }

  .card-link:hover .card-title {
    color: #fff;
  }

  .card-artist {
    font-size: 14px;
    color: #8D91B4;
    margin: 0;
  }

  .card-link:hover .card-artist {
    color: #fff;
  }
</style>
