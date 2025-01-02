<template>
    <button @click="moreInfo()" class="character-card">
        <img :src="image" alt="">
        <div class="info">
            <h1>{{ name }}</h1>
            <p>{{ species }} {{ gender }}
                <span v-if="status=='Alive'" class="alive">({{ status }})</span>
                <span v-if="status=='unknown'" class="unknown">(Unknown)</span>
                <span v-if="status=='Dead'" class="dead">({{ status }})</span>
            </p>
        </div> 
    </button>
    <transition name="fade">
        <div v-show="cachedInfo && show" class="characterInfo">
            <div class="card">
                <img :src="image" alt="">
                <div class="content">
                    <h1>{{ name }}</h1>
                    <p>{{ species }} {{ gender }} 
                        <span v-if="status=='Alive'" class="alive">({{ status }})</span>
                        <span v-if="status=='unknown'" class="unknown">(Unknown)</span>
                        <span v-if="status=='Dead'" class="dead">({{ status }})</span>
                    </p>
                    <p><b>Now in:</b> {{ cache.location.name }}</p>
                    <br>
                    <button class="close" @click="closeInfo()">Close</button>
                </div>
            </div>
        </div>
    </transition>
</template>

<script>
    import axios from 'axios';
    export default{
        name: 'CharactersComponent',
        props: ['name', 'image', 'gender', 'species', 'status', 'id'],
        data(){
            return {
                cachedInfo:false,
                cache: {
                    location:{
                        url: '',
                        name: ''
                    }
                },
                show: false
            }
        },
        methods: {
            closeInfo(){
                this.show=!this.show;
            },
            moreInfo(){
                if(this.cachedInfo){
                    console.log("CACHED")
                    console.log(this.cache)
                    this.show=!this.show;
                }else{
                    axios.get('https://rickandmortyapi.com/api/character/'+this.id).then((data)=>{
                        this.cachedInfo=true;
                        this.cache=data.data;
                        console.log("DOWNLOADED")
                        console.log(this.cache);
                        this.show=!this.show;
                    }).catch((err)=>{
                        console.log(err)
                    })
                }
            }
        },
    }
</script>

<style scoped>
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
    .close{
        width: 100%;
        padding: 40px 0px;
        height:35px;
        border: 1px solid #2e2e2e;
        background-color: #2e2e2e;
        color: #fff;
        border-radius: 5px;
        box-sizing: border-box;
    }

    hr {
        border-color: #ebebeb;
    }

    .card .content{
        padding: 20px 40px;
    }

    .card{
        background-color: #fff;
        width: 30%;
        border-radius: 8px;
    }

    

    @media screen and (max-width: 900px){
        .card{
            width: 60%;
        }
    }

    @media screen and (max-width: 520px){
        .card{
            width: 90%;
        }
    }

    .card img{
        width: 100%;
        border-top-left-radius: 8px;
        border-top-right-radius: 8px;
    }

    .characterInfo{
        backdrop-filter: blur(10px);
        background-color: rgba(0, 0, 0, 0.842);
        z-index: 1;
        position: fixed;
        top: 0;
        bottom: 0;
        right: 0;
        left: 0;
        display: flex;
        align-items: center;
        justify-content: center;
    }
    .character-card, .character-card *{
        display:block
    }

    .character-card{
        display:flex;
        flex-direction: column;
        align-items: center;
        border: solid 1px #ebebeb;
        background-color: #fff;
        border-radius: 8px;
        position: relative;
        transition: .4s;
        box-sizing:border-box;
    }

    .character-card:hover{
        transform: translateY(-5px)
    }

    .character-card .info{
        padding: 20px 30px;
    }

    .character-card img{
        width: 100%;
        object-fit: fill;
        border-top-left-radius: 4px;
        border-top-right-radius: 4px;
    }

    .unknown{
        color: gold ;
        }

    .dead{
        color: red;
    }

    .alive{
        color: green;
    }
</style>