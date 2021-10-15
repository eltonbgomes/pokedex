<template>  
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <hr>
      <h1 class="is-size-3">Pokedex</h1>
      <input type="text" placeholder="Buscar pokémon pelo nome" v-model="find" class="input is-info is-rounded">
      <button class="button is-info is-rounded" id="findButton" @click="findPokemon">Buscar</button>
      <div v-for="(poke) in filteredPokemons" :key="poke.url">
        <pokemon :name="poke.name" :url="poke.url"/>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/Pokemon.vue';

export default {
  name: 'App',
  data(){
    return{
      pokemons:[],
      filteredPokemons: [],
      find: ''
    }
  },
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
      this.pokemons = res.data.results;
      this.filteredPokemons = res.data.results;
    })
  },
  components:{
    Pokemon
  },
  methods:{
    findPokemon: function(){
      this.filteredPokemons =  this.pokemons;
      if(this.find == '' || this.find == ' '){
        this.filteredPokemons =  this.pokemons;
      }else{
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.find);
      }
    }
  },
  computed:{
    /* findPokemon: function(){
      if(this.find == '' || this.find == ' '){
        return this.pokemons;
      }else{
        return this.pokemons.filter(pokemon => pokemon.name == this.find);
      }
    } */
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#findButton{
  margin-top: 1%;
}
</style>
