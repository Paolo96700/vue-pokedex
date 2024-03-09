<script>
import axios from 'axios';
export default {
    props: {
        imagePokemon: String,
        pokemon: String,
    },
    data() {
        return {
            pokemonList: [],
            pokemonsImages: [],
            nextUrl:'',
            currentUrl: '',
        }
    },
    methods: {
        getPokemon(url){
            axios
                .get(url)
                .then(response => {
                    this.pokemonList = [...this.pokemonList, ...response.data.results];
                    if (response.data.next) {
                        // Se c'è un URL successivo, carica i Pokémon da quell'URL
                        this.getPokemon(response.data.next);
                    } else {
                    // Imposta this.nextUrl su null o una stringa vuota per evitare ricariche infinite
                        this.nextUrl = null;
                    }
                    this.pokemonList.forEach(pokemon => {
                        // Ottenere l'ID del Pokémon dall'URL
                        const pokemonId = pokemon.url.split('/').filter(part => !!part).pop();
                        
                        // Costruire l'URL completo dell'immagine
                        pokemon.image = `${this.imagePokemon}${pokemonId}.png`;
                    });  
                })
                .catch(error => {
                    console.error('Error Pokemon list:', error); 
                });
        },
        scrollTrigger() {
            const observer = new IntersectionObserver((entries) => {
                if (entries[0].isIntersecting && this.nextUrl) { 
                    this.getPokemon(this.nextUrl); 
                }
            });

            observer.observe(this.$refs.infinitescrolltrigger); 
        },
        next(){
            this.currentUrl = this.nextUrl;  
        },
        handlePokemonClick(url){
            this.$emit('setPokemonUrl', url)
        } 
    },
    created() {
        this.currentUrl = this.pokemon;
        this.getPokemon(this.currentUrl)
    },
    mounted() {
        this.scrollTrigger();
    },
       
}

</script>

<template>
 
     
    <div class="flex flex-wrap justify-center items-center gap-1">
        <div v-for="pokemon in pokemonList" :key="pokemon.id" @click="handlePokemonClick(pokemon.url)" class="card flex flex-col justify-center items-center bg-gray-700 rounded-md p-2" style="width: 120px;  cursor: pointer;">
            <img :src="pokemon.image" alt="">
            <p class="text-white text-center text-xs font-bold">{{ pokemon.name }}</p>
        </div>
        <div v-if="pokemonList.length === 0" ref="infinitescrolltrigger" class="scroll-trigger flex justify-center items-center size-8 mx-4 my-2" style="width: 120px; height: 140px;">
            <img src="./../../public/icons8-filatore.gif" alt="" class="rounded-full">
        </div>
    </div>
        


</template>

<style scoped>
@media  (max-width: 425px) {
    .container{
        
    }
    .card{
        width: 90px!important;
    }
   
}
</style>