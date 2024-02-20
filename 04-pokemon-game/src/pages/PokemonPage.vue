<template>
  <div>
    <h1 v-if="!pokemon"> Espere por favor... </h1>

    <div v-else>
        <h1>Quién es este pokémon?</h1>

        <PokemonPicture 
            :pokemonId="pokemon.id" 
            :showPokemon="showPokemon"
        />

        <PokemonOptions 
            :pokemons="pokemonArr"
            @selection="checkAnswer( $event )"
        />

        <div v-if="showAnswer">
            <h2> {{message}} </h2>
            <button @click="newGame">
                Nuevo Juego
            </button>
        </div>
    </div>
  </div>
</template>

<script>
import PokemonPicture from '@/components/PokemonPicture.vue'
import PokemonOptions from '@/components/PokemonOptions.vue'
import getPokemonOptions from '@/helpers/getPokemonOptions'

// console.log( getPokemonOptions() )

export default {

    components: {
        PokemonPicture,
        PokemonOptions
    },
    data() {
        return {
            pokemonArr: [],
            pokemon: null,
            showPokemon: false,
            showAnswer: false,
            message: ''
        }
    },
    methods: {
        async mixPokemonArray() {
            this.pokemonArr = await getPokemonOptions()

            const rndInt = Math.floor( Math.random() * 4 )
            this.pokemon = this.pokemonArr[ rndInt ]
        },
        checkAnswer( selectedId ){
            // console.log('Este es el poquemon', selectedId)

            this.showAnswer = true
            if(selectedId === this.pokemon.id){
                this.showPokemon = true

                this.message = `Correcto!, ${this.pokemon.name}`
            }else{
                this.message = `Ooops!, Era ${this.pokemon.name}`
            }
        },
        newGame(){
            this.pokemonArr = [],
            this.pokemon = null,
            this.showPokemon = false,
            this.showAnswer = false,
            this.pokemon = null
            this.message = ''

            this.mixPokemonArray();
        }
    }, 
    mounted() {
        this.mixPokemonArray()
    }

}
</script>
