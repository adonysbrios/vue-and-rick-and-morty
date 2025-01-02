<template>
  <NavBar/>
  <SearchComponent :change="changeSearch" :next="next" :prev="prev" :fetchC="fetchCharacters"/>
  <div class="content">
    <div class="characterList"> 
      <CharactersComponent v-for="character in characters" :id="character.id" :key="character.id" :gender="character.gender" :species="character.species" :status="character.status" :name="character.name" :image="character.image"/>
    </div>
  </div>
  <footer>
    <p>Made by Adonys Barzaga Rios. (Education Purposes)</p>
    <a href="mailto:adonysbarzagarios@gmail.com">Contact me</a>
    <br/>
    <a href="https://github.com/adonysbrios/vue-and-rick-and-morty"> GitHub repository </a>
  </footer>
</template>

<script>
import axios from 'axios';
import CharactersComponent from './components/CharactersComponent.vue';
import NavBar from './components/NavBar.vue';
import SearchComponent from './components/SearchComponent.vue';

export default {
  name: 'App',
  components: {
    CharactersComponent,
    NavBar,
    SearchComponent
  },
  data(){
    return{
      characters:{},
      search: '',
      next: null,
      prev: null
    }
  },
  methods: {
    fetchCharacters(url){
      axios.get(url)
        .then((el)=>{ 
          if(el.data.results){
            this.characters=el.data.results;
            this.next=el.data.info.next;
            this.prev=el.data.info.prev;
          }else{
            this.characters=el.data;
          }
      })
        .catch((error)=>console.log(error))
    },
    changeSearch(val){
      if(val==''){
          this.fetchCharacters('https://rickandmortyapi.com/api/character/1,2,3,4,5,6,7,8,9,10,11,12')
          this.next=null;
          this.prev=null;
      }else{
        this.fetchCharacters('https://rickandmortyapi.com/api/character/?name='+val)
      }
    }
  },
  mounted(){
    this.fetchCharacters('https://rickandmortyapi.com/api/character/1,2,3,4,5,6,7,8,9,10,11,12');
  }
}
</script>

<style>
body *{
  margin: 0;
  padding: 0;
}

* {
  color:#414141;
  font-family: 'Segoe UI';
}
</style>

<style scoped>


#app {
  font-family: 'Segoe UI';
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.content{
  justify-content: center;
  width: 70%;
  margin: 0 auto;
  display: flex
}

.characterList{
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  gap: 30px;
}

@media screen and (max-width: 850px) {
  .characterList{
    grid-template-columns: 1fr 1fr
  }
}

@media screen and (max-width: 500px) {
  .characterList{
    grid-template-columns: 1fr
  }
  .content{
    width: 90%;
  }
}

.content *{
  margin: 0;
  padding: 0;
}

h1{
  color: #2e2e2e;
  font-size: 25px;
}

p{
  color: #414141;
  font-size: 15px;
}

footer{
  width: 70%;
  margin: 0 auto;
  margin-top: 50px;
  padding:16px 15%;
  border-top: solid 1px #ebebeb;
  text-align: center;
}

footer *{
  font-size: .7rem;
}

footer p{
  color: #727272;
}
</style>
