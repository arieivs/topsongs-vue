<template>
  <!-- <form className="d-flex flex-grow-1"> -->
  <form @submit.prevent="onSubmit">
    <input v-model="content" placeholder="Search for an Album or Artist" class="search-bar">
    <input type="submit" value="Search" class="btn-all btn-prim">
  </form>
</template>

<script>
export default {
  name: 'searchBar',
  data: () => ({
    content: null
  }),
  methods: {
    onSubmit() {
      // event: search-submitted
      // value passed with it: content
      this.$emit('search-submitted', this.content)
    }
  }
}
</script>

<style scoped>
  form {
    display: flex;
    max-width: 750px;
    margin: 50px auto;
  }

  .search-bar {
    min-width: 256px;
    padding: 10px 22px;
    background-color: #222451;
    color: #8D91B4;
    border: solid 2px #222451;
    border-radius: 30px;
    flex-grow: 1;
    margin-right: 5px;
  }

  .search-bar:focus-visible {
    color: #fff;
    outline: none;
  }
</style>
