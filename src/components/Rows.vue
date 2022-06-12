<template>
<div class="row-wrapper">
    <button @click="toggleShow"><p>{{genre}}</p></button>
    <div class="row" v-if="show">
        <li v-for="item in movieList" :key="item">
            <img :src="imgUrl+item.backdrop_path" alt="">
            <p>{{item.name?item.name:item.original_title}}</p>
        </li>
    </div>
</div>

  
</template>

<script> 
export default {
    props: ['movieBase', 'API_KEY', 'baseUrl', 'imgUrl', 'genre'],
    data(){ 
        return {
            movieList : '',
            itemTitle: '',
            show: false
        }
    }, 
    methods: {
        toggleShow(){
            this.show = !this.show
        fetch(this.movieBase)
            .then(res => {
                return res.json();
            }).then(data =>{
                console.log(data)
                this.movieList = data.results
                console.log(this.itemTitle)
            })
        }
    }
 
}
</script>

<style>
.row-wrapper{
    padding: 5px 0;
    background: rgba(12, 11, 24, 0.411);
}
.row-wrapper p{
    text-align: left;
    font-size: 25px;
    font-weight: 600;
    padding: 20px 30px;
}
.row-wrapper button{
    border: none;
    background: none;
    color: whitesmoke;
    cursor: pointer;
}
.row{
    white-space: nowrap;
    overflow-x: scroll;
    overflow-y: hidden;
    
} 
::-webkit-scrollbar {
    width: 0;  /* Remove scrollbar space */
    background: transparent;  /* Optional: just make scrollbar invisible */
}
li{
    display: inline-block;
    padding: 5px 10px;
    position: relative;
}
li img{
    height: 200px;
    border-radius: 20px;
}
li p{
    position: absolute;
    top: 70%;
    padding: 10px 20px;
    font-size: 15px;
    font-weight:500;
    z-index: 100;
}
</style> 