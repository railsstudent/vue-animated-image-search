<template>
  <div>
    <form id="search-form">
      <input type="text" class="input is-medium"
        placeholder="What images would you like to see on Pixabay?" v-model="query">
      <button type="submit" class="button is-link is-medium" @click.prevent="search">Search</button>
    </form>
    <div class="hero-body">
      <div class="image-container">
        <div v-for="result in results" class="image-card">
          <img :src="result.largeImageURL" alt="pixable image" class="image-data">
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import axios from 'axios';

const apiUrl = 'https://pixabay.com/api'
const apiKey =  '8653965-67fc8570b61c58e735d9adade'

export default {
  name: 'SearchImageComponent',
  data() {
    return {
      query: "",
      results: []
    }
  },
  methods: {
    search() {
      const requestUrl = `${apiUrl}/?key=${apiKey}&q=${this.query}s&image_type=photo&per_page=15&safesearch=true`;

      axios.get(requestUrl)
        .then(response => {
          const { hits, totalHits } = response.data;
          this.results = (totalHits > 0) ? hits : [];
          console.log(totalHits, this.results);
        })
        .catch (err => {
          console.error(err);
        })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
  #search-form  {
    padding-left: 20%;
    padding-right: 20%;
    background: #363636;
    min-height: 80px;

    height: 100vh;
    display: flex;
    align-items: center;

    input {
      margin-right: 5px;
    }
  }

  .image {
    &-container {
      display: flex;
      flex-flow: row wrap;
    }

    &-card {
      flex: 0 0 33.33%;
    }

    &-data {
      width: 100%;
      height: auto;
    }
  }
</style>
