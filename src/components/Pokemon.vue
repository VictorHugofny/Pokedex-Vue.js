<template>
<div id = "pokemon">

  <div class="card">
  <div class="card-image">
    <figure>
      <img :src="currentImg" alt="Placeholder image">
    </figure>
  </div>
  <div class="card-content">
    <div class="media">
      
      <div class="media-content">
        <p class="title is-4">{{num}} - {{name | upper}}</p>
        <p class="subtitle is-6">{{pokemon.type}}</p>
      </div>
    </div>

    <div class="content">
     
    </div>
  </div>
</div>
</div>
</template>

<script>
import axios from "axios"
export default {
    created: function(){ //pegando a lista de pokemons
    axios.get(this.url).then(res =>{
      this.pokemon.type = res.data.types[0].type.name
      this.pokemon.spritefront = res.data.sprites.front_default;
      this.pokemon.spriteback = res.data.sprites.back_default;
      this.currentImg = this.pokemon.spritefront
      this.console.log(this.pokemon)

    }
    )},

    data(){
        return{
            isFront: true,
            currentImg: '',
            pokemon: {
                type:"",
                spritefront:"",
                spriteback:""
            }
        }
    },
    props:{
        num: Number,
        name: String,
        url: String
    },
    filters: {
        upper: function(value){ 
            let newName = value[0].toUpperCase() + value.slice(1);
            return newName
        }
    }
}
</script>

<style>
#pokemon{
    margin-top: 2%
}
</style>