<template>

<div id="app">

  <div class ="column is-half is-offset-one-quarter">
    <img src="./assets/logo.png" width="100px">
    <h4>Victorhugofny</h4>
    <hr>
    <h4 class="is-size-3"> Pokedex </h4>
    <input type="text" class="input is-rounded" name="" id="buscaBtn" placeholder="Buscar pokemon pelo nome" v-model = 'busca'>
    <button class="button is-fullwidth is-success" @click="buscar">Buscar</button>

      <div v-for="(poke,index) in filterPokemons" :key="poke.url">
      <Pokemon :name = "poke.name" :url = "poke.url" :num = "index + 1"/>
      </div>
  </div>

</div>
</template>

<script>
import axios from "axios";
import Pokemon from "./components/Pokemon";

export default {
  name: 'App',
  data(){
    return{
      pokemons:[],
      filterPokemons: [],
      busca: ""
    }
  },
  created: function(){ //pegando a lista de pokemons
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(rest =>{
      this.pokemons = rest.data.results  
      this.filterPokemons = rest.data.results 
    })
  },
  components: {
    Pokemon
  },
  methods:{
    buscar: function(){
      this.filterPokemons = this.pokemons
      if(this.busca =="" || this.busca == ' '){
        this.filterPokemons = this.pokemons
      } else{
        this.filterPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca)
      }
    }
  },
  computed: {
    /*
    resultadoBusca: function(){
      if(this.busca =="" || this.busca == ' '){
        return this.pokemons;
      } else{
        return this.pokemons.filter(pokemon => pokemon.name == this.busca)
      }
    }
    */
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

#buscaBtn{
  margin-bottom: 3%;
}
</style>
