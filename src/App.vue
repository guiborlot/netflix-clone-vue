<template>
  <div id="app">
    <section v-for="item in list" :key="item.title" class="lists">
      <div>
        <movie-row v-bind:title="item.title" v-bind:items="item.items"/>
      </div>
    </section>
  </div>
</template>

<script>
import Tmdb from "@/Tmdb";
import MovieRow from "@/components/MovieRow";

export default {
  name: 'App',
  components: {
    'movie-row': MovieRow,
  },
  data(){
    return{
      list: {}
    }
  },
  methods: {
    async getFilmes() {
      // Pegando a lista total
      this.list = await Tmdb.getHomeList();
      console.log(this.list);

    },

  },
  mounted() {
    this.getFilmes();
  },


}
</script>

<style>

</style>
