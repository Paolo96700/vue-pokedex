
<script>
import axios from 'axios';
export default {
    props: {
        pokemonUrl: String,
    },
    data() {
        return {
            show: false,
            pokemon: {},
            showFrontImage: true,
            showErrorMessage: false,
        }
    },
    methods: {
        getPokemonDetails(){
        axios
            .get(this.pokemonUrl)
            .then(response => {
                this.pokemon = response.data;
                // Imposta l'URL dell'immagine del Pokémon
                this.image_front = this.pokemon.sprites.front_default;
                this.image_back = this.pokemon.sprites.back_default;
                this.show = true; 
            })
            .catch(error => {
                console.log(error) 
                this.showErrorMessage = true; 
            }); 
        },
        toggleImage() { 
            this.showFrontImage = !this.showFrontImage;
        },
        closeDetail() {
            this.$emit('closeDetail');
            this.show = false; 
            this.pokemon = {};
        },
    },
    created(){
        setTimeout(() => {
            this.getPokemonDetails();
            this.interval = setInterval(() => {
                this.toggleImage();
            }, 1000);
        }, 500);
    }
      
}
</script>

<template>
    <div 
        class="flex flex-col justify-center items-center px-24 py-3 text-black font-bold" 
        style="position: fixed; top: 0; left: 0; width:100%; height: 100%; background: rgba(0, 0, 0, 0.7);"
    >
        <div
            v-if="show" 
            class="flex flex-col justify-center items-center relative  bg-slate-200 rounded-lg" 
            style="width:100%; max-width: 510px;"
        >
            <div v-if="pokemon" class="w-96 flex flex-col"> 
                <div class="w-96 flex justify-center py-4">
                    <div 
                        class="bg-gray-800 flex justify-center rounded-full p-8 w-52" 
                        style="height: 200px; box-shadow: 0 15px 30px rgba(0, 0, 0, 0.5), 
                                                          0 10px 10px rgba(0, 0, 0, 0.5);">
                        <img v-if="showFrontImage" :src="image_front" alt="">
                        <img v-else :src="image_back" alt="">
                    </div>
                </div>
                
                <div 
                    class="flex justify-center text-3xl border-b-2 border-slate-400 mx-2 pb-2" 
                    style="text-transform: capitalize;"
                >
                    {{ pokemon.name }}
                </div>
                <div class="pt-8">
                    <div  class="pt-2 flex justify-between border-b-2 border-slate-400 mx-8 text-base">
                        <div class="">Height</div>
                        <div class="flex flex-col items-end text-base">
                            <div>{{ pokemon.height }} m</div>
                        </div>   
                    </div> 

                    <div  class="pt-2 flex justify-between border-b-2 border-slate-400 mx-8 text-base">
                        <div class="">Weight</div>
                        <div class="flex flex-col items-end text-base">
                            <div>{{ pokemon.weight }} Kg</div>
                        </div>   
                    </div>
                    <div class="pt-4 mx-8">
                        <div class="border-b-2 border-slate-400">Pokemon Types</div>
                      
                        <div class="flex py-3">
                            <div 
                                v-for="pokemon_type in pokemon.types" 
                                :key="pokemon_type.id" 
                                class="mr-3 px-3 py-1 rounded-full text-white bg-black text-sm"
                                style="text-transform: capitalize;"
                            >
                                <div>{{ pokemon_type.type.name }}</div>
                            </div> 
                        </div>
                        <div class="border-b-2 border-slate-400">Abilities</div>
                        
                        <div class="flex py-3">
                            <div 
                                v-for="ability in pokemon.abilities" 
                                :key="ability.id" 
                                class="mr-3 px-3 py-1 rounded-full text-white bg-slate-500 text-sm"
                                style="text-transform: capitalize;"
                            >
                                <div>{{ ability.ability.name }}</div>
                            </div>
                        </div> 
                    </div>
                     
                    <div class="pt-4 px-8 pb-8">
                        <div class="border-b-2 border-slate-400">Pokemon Stats</div>
                        <div v-for="stat in pokemon.stats" :key="stat.id" class="flex justify-between text-base">
                            <div>{{ stat.stat.name }}</div>
                            <div>{{ stat.base_stat }}</div>
                        </div> 
                    </div> 
                </div>
                
            </div>
            
            <button class="m-8 px-6 py-2 bg-slate-800 text-white rounded-md" @click="closeDetail">Close</button>  
        </div>
        <div v-else-if="showErrorMessage" class="flex flex-col justify-center items-center px-24 py-3 text-white font-bold" 
                style="position: fixed; top: 0; left: 0; width:100%; height: 100%; background: rgba(0, 0, 0, 0.7);">
                <h2  class="font-bold">The Pokemon was not found</h2>
                <button class="m-8 px-6 py-2 bg-slate-800 text-white rounded-md" @click="closeDetail">Close</button> 
            </div>
        <img v-else src="./../../public/icons8-filatore.gif" alt="" class="rounded-full">
    </div>
</template>

<style>

</style>