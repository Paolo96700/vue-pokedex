<script>
import Nav from './header/Nav.vue'
import Pokedex from './main/Pokedex.vue'
export default {
  data() {
    return {
    }
  },
  components: {
      Pokedex, Nav,
    }
}
</script>

<template>
  <header>
    <Nav />
  </header>

  <main>
    <Pokedex 
    />
  </main>
</template>

<style scoped>
 
</style>