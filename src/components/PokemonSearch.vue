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
        setPokemonUrl() {
            if(this.searchvalue !== '')
                this.$emit('setPokemonUrl', this.pokemon + this.searchvalue)
        }
    }
}
</script>

<template>
    <div class="my-5 relative flex justify-center items-center"
        style="width: 100%;"
    >
        <form @submit.prevent="setPokemonUrl" class="flex justify-center items-center"
        >
            <input  type="text" 
                    v-model="searchvalue"
                    class="rounded-l-md p-1 text-black font-bold text-base"
                    style="width: 300px;"
            >
        </form>
        <img src="./../../public/search.png" alt="" 
            @click="setPokemonUrl" 
            class="bg bg-slate-700 p-1 rounded-r-md"
            style="height: 33px"
        >
    </div>
   
</template>

<style>

</style>