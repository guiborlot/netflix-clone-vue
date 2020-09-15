<template>
  <section class="featured" :style="{ 'backgroundImage': urlImg }">
    <div class="featured--vertical">
      <div class="featured--horizontal">
        <div class="featured--name">{{featuredData.name}}</div>
        <div class="featured--info">
          <div class="featured--points">{{featuredData.vote_average}} pontos</div>
          <div class="featured--year">{{date}}</div>
          <div class="featured--seasons">{{featuredData.number_of_seasons}} temporada{{ featuredData.number_of_seasons !== 1 ? 's' : '' }}</div>
        </div>
        <div class="featured--description">{{description}}</div>
        <div class="featured--buttons">
          <a href="" class="featured--watchbutton">► Assistir</a>
          <a href="" class="featured--mylistbutton">+ Minha Lista</a>
        </div>
        <div class="featured--genres"><strong>Gêneros:</strong> {{genres.join(', ')}}</div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "FeaturedMovie",
  props: {
    featuredData: Object
  },
  data(){
    return{
      urlImg: "",
      date: "",
      genres: [],
      description: ""
    }
  },
  methods:{
  },
  mounted() {
    this.urlImg = "url(https://image.tmdb.org/t/p/original" + this.featuredData.backdrop_path + ")";
    let date = new Date(this.featuredData.first_air_date);
    this.date = date.getFullYear();
    for(let i in this.featuredData.genres){
      this.genres.push(this.featuredData.genres[i].name)
    }

    this.description = this.featuredData.overview;

    if(this.featuredData.overview.length > 200){
      this.description = this.featuredData.overview.substring(0, 200) + '...';
    } else{
      this.description = this.featuredData.overview
    }
  }
}
</script>

<style scoped>
.featured{
  height: 100vh;
  background-size: cover;
  background-position: center;
}

.featured--vertical{
  width: inherit;
  height: inherit;
  background: linear-gradient(to top, #111 10%, transparent 90%);
}

.featured--horizontal{
  width: inherit;
  height: inherit;
  background: linear-gradient(to right, #111 30%, transparent 70%);
  display: flex;
  flex-direction: column;
  justify-content: center;
  padding-left: 30px;
  padding-bottom: 150px;
  padding-top: 70px;
}

.featured--name{
  font-size: 60px;
  font-weight: bold;
}

.featured--info{
  font-size: 18px;
  font-weight: bold;
  margin-top: 15px;
}

.featured--points, .featured--year, .featured--seasons{
  display: inline-block;
  margin-right: 15px;
}

.featured--points {
  color: #46d369;
}

.featured--description{
  margin-top: 15px;
  font-size: 20px;
  color: #999;
  max-width: 40%;
  white-space: normal;
  overflow: hidden;
  text-overflow: ellipsis;
  max-height: 40%;
}

.featured--buttons{
  margin-top: 15px;
}

.featured--watchbutton, .featured--mylistbutton{
  display: inline-block;
  font-size: 20px;
  font-weight: bold;
  padding: 12px 25px;
  border-radius: 5px;
  text-decoration: none;
  margin-right: 10px;
  opacity: 1;
  transition: all ease 0.2s;
}

.featured--watchbutton:hover, .featured--mylistbutton:hover{
  opacity: 0.7;
}

.featured--watchbutton{
  background: #fff;
  color: #000;
}

.featured--mylistbutton{
  background: #333;
  color: #fff;
}

.featured--genres{
  margin-top: 15px;
  font-size: 18px;
  color: #999;
}

@media(max-width: 760px){
  .featured{
    height: 90vh;
  }
  .featured--name{
    font-size: 40px;
  }
  .featured--info{
    font-size: 16px;
  }
  .featured--description{
    font-size: 14px;
    max-width: 100%;
    margin-right: 30px;
  }
  .featured--watchbutton, .featured--mylistbutton{
    font-size: 16px;
  }
  .featured--genres{
    font-size: 14px;
  }
}
</style>