<template>
  <button class="btn-all btn-prim">{{ content }}</button>
</template>

<script>
  export default {
    name: 'buttonPrimary',
    props: {
      content: String
    }
  }
</script>

<style>
  .btn-all {
    border: none;
    border-radius: 30px;
  }

  .btn-prim {
    padding: 10px 22px;
    background: linear-gradient(to left, #5717a8, #a340c2);
    color: #fff !important;
  }

  .btn-prim:hover {
    background: linear-gradient(to left, #6423b6, #bf5ade);
  }
</style>
