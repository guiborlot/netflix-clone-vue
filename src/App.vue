<template>
  <div id="app">
    <header-movie :setBlack="setBlackHeader" />
    <featured-movie v-if="setFeaturedData == true" :featuredData="featuredData" />
    <section class="lists">
      <div v-for="item in list" :key="item.title">
        <div>
          <movie-row :title="item.title" :items="item.items"/>
        </div>
      </div>
    </section>
    <footer>
      Feito por Guilherme Borlot Oliveira com intuito de aprendizado<br/>
      Direitos de imagem para Netflix<br/>
      Dados pegos do site Themoviedb.org
    </footer>
    <div v-if="list == ''" class="loading">
      <img src="./assets/loading.gif" alt="loading">
    </div>
  </div>

</template>

<script>
import Tmdb from './services/Tmdb'
import MovieRow from "@/components/MovieRow";
import FeaturedMovie from "@/components/FeaturedMovie";
import Header from "@/components/Header"


export default {
  name: 'App',
  components: {
    'movie-row': MovieRow,
    'featured-movie': FeaturedMovie,
    'header-movie': Header
  },
  data() {
    return {
      list: [],
      setFeaturedData: false,
      featuredData: [],
      setBlackHeader: false
    }
  },
  methods: {
    async getList(){
      const res = await Tmdb.getHomeList()
      this.list = res;


      let originals = res.filter(i=>i.slug === 'originals');
      let randomChosen = Math.floor(Math.random() * (originals[0].items.results.length - 1))
      let chosen = originals[0].items.results[randomChosen];
      let choseInfo = await Tmdb.getMovieInfo(chosen.id, 'tv');

      this.featuredData = choseInfo;
      this.setFeaturedData = true;
    }
  },
  mounted() {
    this.getList();
    const scrollListener = () =>{
      if(window.scrollY > 10){
        this.setBlackHeader = true
      } else{
        this.setBlackHeader = false
      }
    }
    window.addEventListener('scroll', scrollListener);
    return () => {
      window.removeEventListener('scroll', scrollListener)
    }
  }

}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');
*{
  box-sizing: border-box;
}

body{
  background: #111;
  color: #fff;
  margin: 0;
  font-family: 'Roboto', sans-serif;
}

.lists{
  margin-top: -150px;
}

footer{
  margin: 50px 0;
  text-align: center;
}

.loading{
  position: fixed;
  left: 0;
  right: 0;
  bottom: 0;
  top: 0;
  z-index: 99;
  background: #000;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
