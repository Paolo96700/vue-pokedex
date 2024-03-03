<script>
  import PokemonSearch from './../components/PokemonSearch.vue';
  import PokemonList from './../components/PokemonList.vue';
  import PokemonDetails from './../components/PokemonDetails.vue';
  export default{
    data() {
      return {
        imageUrl: 'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/',
        apiUrl: 'https://pokeapi.co/api/v2/pokemon/',
        pokemonUrl: '',
        showDetail: false
      }
    }, 
    components: {
        PokemonSearch,
        PokemonList,
        PokemonDetails,
    },
    methods: {
      handleSetPokemonUrl(url){
        this.pokemonUrl = url;
        this.showDetail = true;
      },
      closeDetail(){
        console.log('Chiusura dettagli Pokémon');
        this.pokemonUrl = '';
        this.showDetail = false;
      },
    }
  }
</script>

<template>
  <div class="container m-auto flex flex-col justify-center items-center p-3 bg-slate-800 text-xl text-white">
      <h1 class="text-4xl font-bold font-serif">Pokedex</h1>
      <PokemonList 
        :imagePokemon="imageUrl" 
        :pokemon="apiUrl"
        @setPokemonUrl="handleSetPokemonUrl"
      />
      <PokemonDetails 
        v-if="showDetail"
        :pokemonUrl="pokemonUrl" 
        @closeDetail="closeDetail"
      />
  </div>
</template>

<style lang="scss" scoped>
    
</style>
