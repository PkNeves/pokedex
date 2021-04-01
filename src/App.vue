<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <h2>Pokedex</h2>
      <input class="input is-rounded" type="text" placeholder="Buscar pokemon pelo nome" v-model="busca">
      <button class="button is-fullwidth is-success" id="buscarBtn" @click="buscar">Buscar</button>
      <div v-for="(poke, index) in pokemonsFilter" :key="poke.name">
        <Pokemon :nome="poke.name" :url="poke.url" :num="index"/>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import Pokemon from './components/Pokemon'

export default {
  name: 'App',
  components: {
    Pokemon
  },
  computed: {
    resultadoBusca: function() {
      if (this.busca == '' || this.busca == ' ') return this.pokemons
      return this.pokemons.filter(pokemon => pokemon.name == this.busca)
    }
  },
  data() {
    return {
      pokemons: [],
      pokemonsFilter: [],
      busca: ''
    }
  },
  created: function() {
    axios.get("http://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then(res => {
      console.log('Pegou a lista de pokemons')
      this.pokemons = res.data.results
      this.pokemonsFilter = res.data.results
    })
  },
  methods: {
    buscar: function() {
      this.pokemonsFilter = this.pokemons
      if (this.busca != '' && this.busca != ' ') {
        this.pokemonsFilter =  this.pokemons.filter(pokemon => pokemon.name == this.busca)

      }
    }
  }
}
</script>

<style>

</style>
