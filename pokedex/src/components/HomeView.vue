<template>
    <section>
        <PokemonSearch></PokemonSearch>
        <PokemonCards></PokemonCards>
    </section>
 
</template>

<script>
import PokemonSearch from './PokemonSearch.vue';
import PokemonCards from './PokemonCards.vue';

export default{
    name: 'HomeView',

    components: {
        PokemonSearch,
        PokemonCards,
    }
}
</script>

<style>

section{
    background: rgb(250, 247, 247);
}  
</style>