<template>
    <div class="col-3" v-if="pokemon.sprites && pokemon.sprites.front_default">
        <div class="card" style="">
            <img :src="pokemon.sprites.front_default" class="card-img-top" alt="pokemon image">
            <div class="card-body">
                <h4 class="card-title text-capitalize">{{pokemon.name}}</h4>
                <p class="poke-height">Height: {{parseFloat(Math.round(pokemon.height * 3.9)).toFixed(2)}} inch</p>
                <p class="poke-weight">Weight: {{pokemon.weight}} units</p>
                <a class="btn btn-primary" @click="movesShow()" >Learn more</a>
            </div>
        </div>
        <div class="moves" v-bind:style='{display: (show ? "block" : "none")}'>
                <div class="text-moves">
                    <p class="move-title">Move List</p>
                    <p>{{pokemon.moves[0].move.name}}</p>
                    <p>{{pokemon.moves[1].move.name}}</p>
                    <p>{{pokemon.moves[2].move.name}}</p>
                </div>
         </div>
    </div>
</template>

<script>
    export default {
        name: 'card',
        data: function() {
            return {
                pokemon: "",
                show: false,
            }
        },
        props: {
            url: String
        },
        mounted: function() {
            console.log("mounted function ran")

            const axios = require('axios')
            const vm = this;

            axios({
                method: 'get',
                url: vm.url,
                responseType: 'stream'
            })
            .then(function (response) {
                console.log(response.data);
                vm.pokemon = response.data
            });
        },
        methods: {
            movesShow: function(event){
                // checks value
                if(this.show){
                    this.show = false;
                }else{
                    this.show = true;
                }
            },
            
        },
        
    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

p {
    font-size: 14px;
}

img.card-img-top {
    height:286px;
    width: 286px;
}

.card {
    text-align: center;
    margin-bottom: 20px;
    width: 17rem;
}

.moves{
    margin: 0;
    padding-bottom: 125px;
    background-color: #f7f7f7;
    text-transform: uppercase;
    position: relative;
    height: 100%;
    max-height: 255px;
    width: 17rem;
    display: none;
    position: relative;
    line-height: 1;
    border: 1px solid black;
}

a.btn{
    cursor: pointer;
}
a:not([href]):not([tabindex]) {
    color: white;
}
div.card{
    margin-top: 20px;
}
.text-moves{
    display: inline-block;
    padding: 20px;
}
p.move-title{
    font-family: sans-serif;
    display: absolute;
    border-bottom: 1px solid black;
    font-size: 16px;
    font-weight: bold;
}
@media (max-width: 1200px) {
    div.card{
        width: 21vw;
        
    }
    .card-body{
        padding: 5px;
        width: 21vw;
    }
    img.card-img-top {
        height: 26vh;
        width: 21vw;
    }
    .moves{
        width: 21vw;
        font-size: 14px;
    }
    
}

@media (max-width: 770px) {
    div.card{
        width: 19vw;  
    }
    .card-body{
        width: 19vw;
    }
    img.card-img-top {
        height: 24vh;
        width: 19vw;
    }
    .moves{
        font-size: 12px;
        width: 19vw;
    }
    p{
        font-size: 12px;
    }
    .card-title{
        font-size: 20px;
    }
    .btn{
        padding: .285rem .55rem;
        font-size: 14px;
    }
}

</style>
