<template>
    <div class="display">
        <img :src="poster" alt="">
        <div class="info">
            <p style="font-size: 70px; font-weight: bold">{{title}}</p>
            <div class="button">
                <button @click="toggleShowInfo" >More Info</button>
                <button @click="goDown">Search</button>
            </div>
            <div class="pp" v-show="showInfo"><p style="font-size: 16px" >{{desc}}</p></div>
        </div>
        
    </div>
</template>



<script>
export default {
    props: ['displayMovie', 'title', 'poster', 'desc'],
    data() {
        return {
            showInfo: false
        }
    },
    mounted(){
        //fetch api and display movie
        // console.log(this.displayMovie);
        
    },   
    methods: {
        toggleShowInfo(){
            this.showInfo = !this.showInfo;
        },
        goDown(){
            window.scrollTo(0, document.body.scrollHeight);
        }
    }

}
</script>








<style>
body{
    scroll-behavior: smooth;
}
.display{
    width: 90vw;
    height: 100vh;
}
.display img{
    width: 100%;
    height:100vh;
    object-position: top;
    object-fit: cover;
    position: absolute;
    top:0;
    z-index: -100;

}
.pp{
    background: rgba(65, 153, 65, 0.582);
    padding: 20px 30px;
    margin: 20px auto;
    border-radius: 20px;

    
}
.info{
    height: 100vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
    text-align: left;
    width: 500px;
    padding: 2%;
}
.info p{
    padding: 15px 0;
}
.button button{
    padding: 10px 10px;
    width: 25%;
    margin: 0 30px 0 0;
    border-radius: 5px;
    border:none;
    transition: 0.3s;
    font-weight: bold;
    font-size: 14px;
    color: rgb(66, 66, 66);
    cursor: pointer;
    background: rgba(245, 245, 245, 0.726);
    
}
.button button:hover{
    background: rgb(255, 255, 255);
}

</style>