<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <h4 class="is-size-3">Consumindo API - da Pokémon</h4>
      <p></p>
      <input type="text" class="input is-rounded" placeholder="Buscar pokemon pelo nome" v-model="busca">
      <button class="button is-fullwidth is-black" id="buscaBtn" @click="buscar">Buscar</button>

        <div v-for="(poke,index) in filterPokemos" :key="poke.url">
        <Pokemon :name= "poke.name" :url = "poke.url" :num="index + 1"/>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/Pokemon'

export default {
  name: 'App',
  data(){
    return {
      busca: '',
      pokemons: [],
      filterPokemos: []
    }
  },
  created: function(){
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res=>{
      console.log("Pegou a lista de pokemons");
      this.pokemons = res.data.results;
      this.filterPokemos = res.data.results;
      console.log(this.pokemons);


    })
  },
  components: {
    Pokemon
  },
  methods: {
    buscar: function(){
      if(this.busca == '' || this.busca == ' '){
        this.filterPokemos = this.pokemons
      }
      else{
        this.filterPokemos = this.pokemons.filter(pokemon => pokemon.name == this.busca)
      }
    }
  }
  // computed: {
  //   resultadoBusca: function(){
  //     if(this.busca == '' || this.busca == ' '){
  //       return this.pokemons
  //     }else{
  //       return this.pokemons.filter(pokemon => pokemon.name == this.busca)
  //     }
  //   }
  // }

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
#buscaBtn {
  margin-top: 2%;
}
</style>
