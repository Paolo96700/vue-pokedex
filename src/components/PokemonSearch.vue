<script>
export default {
    props:{
        pokemon: String,
    },
    data() {
        return {
            searchvalue: '',
        }
    },
    methods: {
        setPokemonUrl(url) {
            if(this.searchvalue !== '')
                this.$emit('setPokemonUrl', this.pokemon + this.searchvalue)
        }
    }
}
</script>

<template>
    <div class="my-5 relative">
        <form @submit.prevent="setPokemonUrl" class="flex  justify-center">
            <input  type="text" 
                    v-model="searchvalue"
                    class="rounded-md w-96 p-1 text-black font-bold text-base"
            >
        </form>
        <img src="./../../public/search.png" alt="" 
            @click="setPokemonUrl" 
            class="absolute right-1 top-1.5"
            style="height: 20px"
        >
    </div>
   
</template>

<style>

</style>