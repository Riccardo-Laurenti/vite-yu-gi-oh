<script>
import AppPokemonsCard from './AppPokemonsCard.vue';
import { store } from '../data/store';
export default {
    computed: {
        pokemonsdre() {
            return store.pokemons.list;
        },
    },
    components: { AppPokemonsCard },
};
</script>

<template>
    <div class="container">
        <div class="pokemon-list">
            <div class="row row-cols-2 row-cols-md-3 row-cols-lg-5 gy-5">
                <div class="col" v-for="pokemon in pokemonsdre">
                    <AppPokemonsCard :key="pokemon.id" :id="pokemon.number" :img="pokemon.imageUrl" :name="pokemon.name"
                        :type="pokemon.type1.toLowerCase()" />
                </div>
            </div>
        </div>
    </div>
</template>

<style lang="scss" scoped>
@import 'bootstrap/dist/css/bootstrap.css';


#app {
    background-color: red;
}
.my-bi {
  font-size: 20;
}
.pokemon-list {
    background-color: #93ceff;
    padding: 20px;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    overflow-y: auto;
    align-items: center;
}

.c-pokemon {
    border-radius: 0px;
}
</style>