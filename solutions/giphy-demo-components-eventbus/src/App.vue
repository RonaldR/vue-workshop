<template>
  <div id="app">
    <suggestions></suggestions>
    
    <searchform></searchform>
    
    <spinner v-if="isLoading"></spinner>
    
    <div class="container" v-if="results">
      <item v-for="result in results" v-bind:result="result" :key="result.id"></item>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Zooming from 'zooming';
import { EventBus } from './eventbus.js';
import item from './components/Item';
import spinner from './components/Spinner';
import searchform from './components/Searchform';
import suggestions from './components/Suggestions';

export default {
  name: 'app',

  components: {
    item,
    suggestions,
    spinner,
    searchform
  },

  data() {
    return {
      searchQuery: '',
      results: [],
      isLoading: false,
    }
  },
  
  created: function() {
    this.submitForm('Money rain');
    
    // Listen to Suggestions
    EventBus.$on('suggestion-clicked', (searchQuery) => {
      this.submitForm(searchQuery);
    });
    
    // Listen to Searchform
    EventBus.$on('searchform-submit', (searchQuery) => {
      this.submitForm(searchQuery);
    });
  },
  
  methods: {
    submitForm(searchQuery) {
      const apiURL = `https://api.giphy.com/v1/gifs/search?api_key=cEDADbeB31OKJkua38c8r8BmaFuiHkph&q=${searchQuery}&limit=18&offset=0&rating=R&lang=en`;

      this.results = [];
      this.searchQuery = searchQuery;
      this.isLoading = true;

      axios.get(apiURL).then((response) => {
        console.log(response);
        
        this.results = response.data.data;
        this.isLoading = false;
      }).then(() => {
        new Zooming();
      });
    }
  },
}
</script>

<style>
  body {
    position: relative;
    background: rgba(0, 140, 231, 1);
    margin: 0 0 -100px;
    height: 100%;
    overflow-x: hidden;
  }

  body::before,
  body::after {
    content: '';
    position: absolute;
    display: block;
    background: rgba(255, 255, 255, 1);
    width: 120%;
    height: 280px;
    transform: rotate(-6deg) translateY(-220px);
    z-index: -1;
  }

  body::after {
    transform: rotate(-6deg) translateX(-50px) translateY(-450px);
    height: 400px;
  }

  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    margin: 20px auto 0;
    width: 90%;
    max-width: 1400px;
    min-height: 800px;
  }

  .loading {
    margin: 200px 0 0;
  }

  .container {
    display: grid;
    grid: 1fr 1fr 1fr / 1fr 1fr 1fr;
    grid-column-gap: 50px;
    grid-row-gap: 50px;
    margin: 50px 0;
  }
</style>
