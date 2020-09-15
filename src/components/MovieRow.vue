<template>
  <div>
    <h2>{{title}}</h2>
    <div class="movieRow--listarea" v-for="item in items.results" :key="item.results">
      <img src="https://image.tmdb.org/t/p/w300">
    </div>
  </div>
</template>

<script>
export default {
  name: "MovieRow",
  props: {
    title: String,
    items: Object
  },
  mounted() {
    
  }
}

</script>

<style scoped>

</style>