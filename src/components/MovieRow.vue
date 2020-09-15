<template>
  <div class="movieRow">
    <h2>{{title}}</h2>
    <div class="movieRow--left" v-on:click="handleLeftArrow()">
      <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="white" width="50px" height="50px"><path d="M0 0h24v24H0z" fill="none"/><path d="M15.41 7.41L14 6l-6 6 6 6 1.41-1.41L10.83 12z"/></svg>
    </div>
    <div class="movieRow--right" v-on:click="handleRightArrow()">
      <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="white" width="50px" height="50px"><path d="M0 0h24v24H0z" fill="none"/><path d="M10 6L8.59 7.41 13.17 12l-4.58 4.59L10 18l6-6z"/></svg>
    </div>
    <div class="movieRow--listarea" >
      <div class="movieRow--list" :style="{ marginLeft: scrollX + 'px', width: (items.results.length) * 150 + 'px'}">
        <div class="movieRow--item" v-for="item in items.results" :key="item.results">
          <img v-if="item.poster_path" :src="url + item.poster_path">
        </div>
      </div>

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
  data(){
    return{
      url: 'https://image.tmdb.org/t/p/w300',
      scrollX: 0
    }
  },
  methods:{
    handleLeftArrow(){
      this.scrollX = this.scrollX + Math.round(window.innerWidth / 2);
      if(this.scrollX > 0){
        this.scrollX = 0;
      }
      console.log(this.scrolX)
    },
    handleRightArrow(){
      this.scrollX = this.scrollX - Math.round(window.innerWidth / 2);
      let listW = this.items.results.length * 150;
      if((window.innerWidth - listW) > this.scrollX) {
        this.scrollX = (window.innerWidth - listW) - 60;
      }
    }
  },
  mounted() {
  }
}

</script>

<style scoped>
.movieRow{
  margin-bottom: 30px;
}
.movieRow h2{
  margin: 0px 0px 0px 30px;
}

.movieRow--listarea{
  overflow-x: hidden;
  padding-left: 30px;
}

.movieRow--list{
  transition: all ease 0.5s;
}

.movieRow--item{
  display: inline-block;
  width: 150px;
  cursor: pointer;
}
.movieRow--item img{
  width: 100%;
  transform: scale(0.9);
  transition: all ease 0.2s;
}
.movieRow--item img:hover{
  transform: scale(1);
}

.movieRow--left, .movieRow--right{
  position: absolute;
  width: 40px;
  height: 225px;
  background: rgba(0, 0, 0, 0.6);
  z-index: 99;
  display: flex;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  cursor: pointer;
  opacity: 0;
  transition: all ease 0.5s;
}

.movieRow--left{
  left: 0;
}
.movieRow--right{
  right: 0;
}

.movieRow:hover .movieRow--left, .movieRow:hover .movieRow--right{
  opacity: 1;
}

@media (max-width: 760px){
  .movieRow--right, .movieRow--left{
    opacity: 1;
  }
}
</style>