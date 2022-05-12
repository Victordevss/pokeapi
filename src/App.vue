<template>
<div id="app">
  <div class="column is-half is-offset-one-quarter">
    <hr>
    <h4 class="is-size-4">Pokedex</h4>
    <input type="text" placeholder="Bucar pokemon pelo nome" v-model="busca"  class="input is-info">
    <br>
    <button class="button is-medium is-fullwidth is-success" id="mudar" @click="buscar">Buscar</button><br>
    
    <div v-for="(poke, index) in filteredpokemon" :key="poke.url">
      <Pokemon :name="poke.name" :url="poke.url" :num="index+1"/>
    </div>
  </div>
</div>
</template>

<script>

import axios from 'axios'
import Pokemon from './components/Pokemon.vue'
export default {
  name: 'App',
  data(){
    return {
      pokemons: [],
      filteredpokemon: "",
      busca: ""
    }
  },
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
      console.log('peguei')
      this.pokemons = res.data.results
      this.filteredpokemon = res.data.results
    })
  },
  components: {
    Pokemon
  },
  methods: {
    buscar: function(){
      this.filteredpokemon = this.pokemons
      if(this.busca == '' || this.busca == ' '){
        this.filteredpokemon == this.pokemons
      }else{
        this.filteredpokemon = this.pokemons.filter(pokemon => pokemon.name == this.busca)
      }
    }
  }
  /*
  computed:{
    resultadoBusca: function(){
      if(this.busca == '' || this.busca == ' '){
        return this.pokemons
      }else{
        return this.pokemons.filter(pokemon => pokemon.name == this.busca)
      }
    }
  }
  */
  
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webrit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#mudar{
  margin-top: 2%;
}

</style>


