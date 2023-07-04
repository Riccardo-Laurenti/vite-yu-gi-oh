<script>
import axios from 'axios';
import { store } from '../data/store';
export default {
    data() {
        return {
            store,
            selectedType: '',
            searchedTerm: '',
            originalList: [],
        };
    },
    props: {
        types: {
            type: Array,
            required: true,
        },
    },
    watch: {
        selectedType: {
            immediate: true,
            handler(newType) {
                this.fetchPokemonsByType(newType);
            },
        },
    },
    computed: {
        typeOptions() {
            return ['', ...this.types];
        },
    },
    methods: {
        fetchPokemonsByType(type) {
            const url = `https://41tyokboji.execute-api.eu-central-1.amazonaws.com/dev/api/v1/pokemons?type=${type}`;
            axios
                .get(url)
                .then(res => {
                    this.store.pokemons.list = res.data.docs;
                    this.originalList = res.data.docs;
                })
                .catch(e => {
                    console.error(e);
                });
        },
        searchPokemons() {
            if (this.searchedTerm) {
                const term = this.searchedTerm.toLowerCase();
                const filteredPokemons = this.originalList.filter((pokemon) =>
                    pokemon.name.toLowerCase().includes(term)
                );
                this.store.pokemons.list = filteredPokemons;
            } else {
                this.store.pokemons.list = this.originalList;
            }
        },
    },
};
</script>

<template>
    <header class="container text-center my-4">
        <div class="search-button">
            <!-- Input search -->
            <div class="input-group text-danger">
                <input type="text" class="form-control" v-model="searchedTerm" @input="searchPokemons"
                    placeholder="Search your pokemon">
            </div>
            <!-- Input select -->
            <select class="form-select" v-model="selectedType">
                <option value="">All Pokemon</option>
                <option v-for="type in types" :key="type" :value="type">{{ type }}</option>
            </select>
        </div>
    </header>
</template>

<style scoped>

.search-button {
    display: flex;
    justify-content: center;
    align-items: center;
}
.input-group {
    width: 500px;
    margin-right: 20px;
}
.form-select {
    width: 500px;
}
</style>