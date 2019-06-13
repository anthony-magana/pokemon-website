<template>
  <div class="card" style="width: 18rem;">
  <img :src="pokemon.sprites.front_default" class="card-img-top" alt="dragonite image">
  <div class="card-body">
    <h4 class="card-title">{{pokemon.name}}</h4>
    <p class="poke-height">Height: {{pokemon.height *3.9}} inch</p>
    <p class="poke-weight">Weight: {{pokemon.weight}} units</p>
    <a href="#" class="btn btn-primary">Learn more</a>
  </div>
</div>
</template>

<script>
    export default {
    name: 'card',
    data: function() {
        return {
            pokemon: ""
        }
    },
    props: {
        msg: String
    },
    mounted: function() {
        console.log("mounted function ran")

        const axios = require('axios')
        const vm = this;

        axios({
            method: 'get',
            url: 'https://pokeapi.co/api/v2/pokemon/dragonite',
            responseType: 'stream'
            })
            .then(function (response) {
                console.log(response.data);
                vm.pokemon = response.data
            });
        }
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

p {
    font-size: 14px;
}

a {
  color: #f8f8f8;
}


</style>
