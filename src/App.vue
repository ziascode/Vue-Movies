<template>
  <div class='app'>
    <div class="nav">
      <img src="https://upload.wikimedia.org/wikipedia/commons/9/95/Vue.js_Logo_2.svg" alt="">
      <h1>VUE MOVIES</h1>
      <!-- <img class='icon' src="https://mir-s3-cdn-cf.behance.net/project_modules/disp/64623a33850498.56ba69ac2a6f7.png" alt=""> -->
    </div>

    <Display :displayMovie='displayMovie' :title='title' :poster='poster' :desc='desc'/>
    <Request :API_KEY='API_KEY' :imgUrl='imgUrl' />
    <Rows :movieBase='category[0]' :API_KEY='API_KEY' :baseUrl='baseUrl' :imgUrl='imgUrl' :genre='genre[0]'/>
    <Rows :movieBase='category[1]' :API_KEY='API_KEY' :baseUrl='baseUrl' :imgUrl='imgUrl' :genre='genre[1]'/>
    <Rows :movieBase='category[2]' :API_KEY='API_KEY' :baseUrl='baseUrl' :imgUrl='imgUrl' :genre='genre[2]'/>
    <Rows :movieBase='category[3]' :API_KEY='API_KEY' :baseUrl='baseUrl' :imgUrl='imgUrl' :genre='genre[3]'/>
    
  </div>
</template>

<script>
import Display from './components/Display.vue'
import Rows from './components/Rows.vue'
import Request from './components/Request.vue'

export default {          
  name:'App', 
  components:{ Display, Rows, Request},
  data(){
    return { 
      baseUrl:'https://api.themoviedb.org/3',
      imgUrl:'https://image.tmdb.org/t/p/original',
      API_KEY:'6e291f4f26c7459d67c95b1f2798dc9b',
      displayMovie:'',
      title :'',
      poster:'',
      desc:'',
      genre:['Top Rated', 'Action Movies', 'Netflix Originals', 'Comedies'], 
      category:[1,2,3,4]
    
    }
  },
  mounted(){
    
    
    this.category[0]= `${this.baseUrl}/discover/movie?api_key=${this.API_KEY}&with_genres=28`
    this.category[1]= `${this.baseUrl}/movie/top_rated?api_key=${this.API_KEY}&language=en-US`
    this.category[2]= `${this.baseUrl}/discover/tv?api_key=${this.API_KEY}&with_networks=213`
    this.category[3]= `${this.baseUrl}/discover/tv?api_key=${this.API_KEY}&with_genres=35`


    fetch(`${this.baseUrl}/trending/all/week?api_key=${this.API_KEY}&language=en-US`)
      .then(res => {
        return res.json();   
      }).then(data =>{
        this.displayMovie = data.results[Math.floor(Math.random() * 20)];
        console.log(this.displayMovie)
        this.title =  (this.displayMovie.name?this.displayMovie.name:this.displayMovie.original_title);
        this.poster = `${this.imgUrl}${this.displayMovie.backdrop_path}`;
        this.desc = this.displayMovie.overview;
        console.log(this.title)
        console.log(data)
        
      })
  }
}
</script>

<style>
*{
  margin:0;
  padding:0;
  box-sizing:border-box;
}
body{
  background:rgba(12, 11, 24, 0.993);
  
}
.app{
  color:aliceblue;
  font-family:'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}
.app span{
  color:rgb(56, 146, 78);
}
.app h1{
  display:flex;
  justify-content:center;
  margin:20px auto;
}
.nav {
  padding:15px 10px;
  background:rgba(29, 26, 26, 0);
  display:flex;
  justify-content:start;
  width:15%;
}
.nav img{
  width:100px;
}
.nav .icon{
  width:50px;
}
.nav h1{
  background-image:linear-gradient(60deg, #174374, #1cb5ab, #2dbe70);
  background-clip:text;
  color:transparent;
}
</style>
