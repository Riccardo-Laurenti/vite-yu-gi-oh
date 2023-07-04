<script>
import axios from 'axios';
const endpoint = 'https://41tyokboji.execute-api.eu-central-1.amazonaws.com/dev/api/v1/pokemons'
import { store } from './data/store.js';
import AppMain from './components/AppMain.vue';
import AppHeader from './components/AppHeader.vue';
import AppLoader from './components/AppLoader.vue';
import AppArrows from './components/AppArrows.vue';
export const fetchPokemons = (page = '') => {
  store.isLoading = true;
  const url = page ? endpoint + `?page=${page}` : endpoint;
  axios
    .get(url)
    .then(async res => {
      store.pokemons.list = res.data.docs;
      store.pokemons.pages.prev = res.data.prevPage;
      store.pokemons.pages.next = res.data.nextPage;
      store.pokemons.pages.current = res.data.page;
    })
    .catch(e => {
      console.error(e);
    })
    .then(() => {
      store.isLoading = false;
    });
};
export default {
  data() {
    return {
      store,
      types: [
              'Bug', 
              'Dark', 
              'Dragon', 
              'Electric', 
              'Fairy', 
              'Fighting', 
              'Fire', 
              'Flying', 
              'Ghost', 
              'Grass', 
              'Ground', 
              'Ice', 
              'Normal', 
              'Poison', 
              'Psychic', 
              'Rock', 
              'Steel', 
              'Water'
            ],
    };
  },
  components: { AppArrows, AppMain, AppHeader, AppLoader },
  created() {
    fetchPokemons();
    this.fetchTypes();
  },
  methods: {
    fetchTypes() {
      const typesUrl = 'https://41tyokboji.execute-api.eu-central-1.amazonaws.com/dev/api/v1/pokemons/types1';
      axios
        .get(typesUrl)
        .then(res => {
          this.types = res.data;
        })
        .catch(e => {
          console.error(e);
        });
    },
  },
};
</script >
<template>
  <div class="container-background">
    <AppHeader :types="types" />
    <AppMain />
    <AppLoader />
  </div>
</template>

<style lang="scss" scoped>
@import '../src/assets/scss/style.scss';
</style>