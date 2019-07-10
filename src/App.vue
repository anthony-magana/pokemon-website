<template>
  <div id="app">
    <div class="container">
      <h1 class="text-center display-3 my-4 text-capitalize">{{activeType}} Type Pokemon</h1>
      <span v-for="type in types" :key="type.name" class="btn btn-primary m-1 text-capitalize" v-on:click="somethingHappened(type.name)">
        {{type.name}}
      </span>
      <div class="row">
        <card :url="item.pokemon.url" v-for="item in pokemonOfCurrentType" :key="item.pokemon.name"> </card>
      </div>
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import card from './components/card.vue'

  export default {
    name: 'app',
    components: {
      HelloWorld,
      card
    },
    data: function(){
      return {
        pokemonOfCurrentType: "",
        types:"",
        activeType: "dragon"
      }
    },
    methods: {
      somethingHappened: function(name) {
        //console.log("something happened ")
        this.activeType = name;
        this.retrievePokemonOfSpecifiedType(this.activeType);
      },
      retrievePokemonOfSpecifiedType: function(type){
        const axios = require('axios')
        const vm = this;

        axios({
        method: 'get',
        url: 'https://pokeapi.co/api/v2/type/' + this.activeType
        })
        .then(function (response) {
          console.log(response.data.pokemon);
          vm.pokemonOfCurrentType = response.data.pokemon
        });
      }
    },

    mounted: function() {
      console.log("mounted function ran")

      const axios = require('axios')
      const vm = this;

      this.retrievePokemonOfSpecifiedType(this.activeType);

      axios({
        method: 'get',
        url: 'https://pokeapi.co/api/v2/type'
      })
      .then(function (response) {
        //console.log(response.data.results);
        vm.types = response.data.results
      });
    }
        
  }
</script>

<style>
@media (max-width: 770px){
  .display-3{
    font-size: 3.3rem;
  }
}
</style>
