<template>
  <div id="#search" class='search'>
      <div class="search-box">
          <input  type="text" size="30" v-model="query" @keypress="searchMovie">
          <button>Search</button>
          <button>Clear</button>
      </div>
      
      <p v-if="submit">Search Results for {{query}}</p>
      <div class="list">
          <li v-for="item in movieResult" :key="item">
            <img :src="imgUrl+item.backdrop_path" alt="">
          </li>
      </div>
      
  </div>
</template>

<script>
export default {
    props: ['API_KEY', 'imgUrl'],
    data(){
        return{
            searchUrl: 'https://api.themoviedb.org/3/search/movie?api_key=###&query=the+avengers',
            query: '',
            movieResult: '',
            submit: false
        }
    },
    methods: {
        searchMovie(e){
            
            if(e.key == 'Enter'){
                this.submit = true
                fetch(`https://api.themoviedb.org/3/search/movie?api_key=${this.API_KEY}&query=${this.query}`)
                    .then(res =>{
                        return res.json();
                    }).then( data => { 
                        console.log(data.results)
                        this.movieResult = data.results
                    })
            }
        } 
    }
}
</script>

<style>

.search{
    display: flex;
    flex-direction: column;
    align-items: center;
}
.list{
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    justify-content: center;
    
}
.search-box{
    display: flex;
    flex-wrap: wrap;
}
.search-box input{
    padding: 10px 10px;
    border-radius: 10px;
    outline: none;
    border: none;
}
.search-box button{
    padding: 10px 10px;
    width: 70px;
    margin: 0 0 0 10px;
    border-radius: 10px;
    outline: none;
    border: none;
    background: rgb(64, 131, 207);
    cursor: pointer;
}
.search-box button: :hover{
    
}
</style>