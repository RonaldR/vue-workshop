<template>
  <div id="app">
    <div class="suggestions">
        <a href="#" class="btn btn--blue-ghost" v-on:click="submitForm('Money rain')">Money rain</a>
        <a href="#" class="btn btn--blue-ghost" v-on:click="submitForm('Vue')">Vue</a>
        <a href="#" class="btn btn--blue-ghost" v-on:click="submitForm('Javascript')">Javascript</a>
        <a href="#" class="btn btn--blue-ghost" v-on:click="submitForm('Wow')">Wow</a>
        <a href="#" class="btn btn--blue-ghost" v-on:click="submitForm('anwb')">anwb</a>
    </div>
    
    <form @submit.prevent="submitForm(searchQuery)">
        <input type="search" placeholder="Zoek je gif" v-model="searchQuery" />
    </form>
    
    <div class="container" v-if="results">
        <div class="item image" v-for="result in results" :key="result.id">
            <img v-if="result.images.downsized_medium" v-bind:src="result.images.downsized_medium.url" data-action="zoom" />
                <span class="info">
                <span class="title">{{ result.title }}</span>
            </span>
        </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Zooming from 'zooming';

export default {
  name: 'app',

  data() {
    return {
      searchQuery: '',
      results: []
    }
  },
  
  created: function() {
    this.submitForm('Money rain');
  },
  
  methods: {
    submitForm(searchQuery) {
      const apiURL = `https://api.giphy.com/v1/gifs/search?api_key=cEDADbeB31OKJkua38c8r8BmaFuiHkph&q=${searchQuery}&limit=18&offset=0&rating=R&lang=en`;

      this.results = [];
      this.searchQuery = searchQuery;

      axios.get(apiURL).then((response) => {
        console.log(response);
        
        this.results = response.data.data;
        this.isLoading = false;
      }).then(() => {
        new Zooming();
      });
    },
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

  input[type="search"] {
    border-radius: 2px;
    box-shadow: 0 2px 2px 0 rgba(0,0,0,0.16), 0 0 0 1px rgba(0,0,0,0.08);
    border: 0;
    height: 44px;
    padding: 0 20px;
    font-size: 16px;
    min-width: 300px;
    outline: 0;
  }


  .image {
    position: relative;
  }

  .image img {
    display: flex;
    height: 100%;
    width: 100%;
    object-fit: cover;
    border-radius: 5px;
  }

  .info {
    padding: 15px;
    position: absolute;
    bottom: 0;
    right: 0;
    max-width: 80%;
    font-size: 14px;
    text-align: right;
    color: #fff;
    text-shadow: 1px 0px 1px #252525;
  }

  .maker {
    display: block;
    font-weight: bold;
  }

  img[data-action="zoom"] {
    cursor: pointer;
    cursor: -webkit-zoom-in;
    cursor: -moz-zoom-in;
  }

  .zoom-img,
  .zoom-img-wrap {
    position: relative;
    z-index: 666;
    transition: all 300ms;
  }

  img.zoom-img {
    cursor: pointer;
    cursor: -webkit-zoom-out;
    cursor: -moz-zoom-out;
  }

  .zoom-overlay {
    z-index: 420;
    background: #fff;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    pointer-events: none;
    filter: 'alpha(opacity=0)';
    opacity: 0;
    transition: opacity 300ms;
  }

  .zoom-overlay-open .zoom-overlay {
    filter: 'alpha(opacity=100)';
    opacity: 1;
  }

  .zoom-overlay-open,
  .zoom-overlay-transitioning {
    cursor: default;
  }

  .suggestions {
    margin-bottom: 20px;
  }
  
  .btn {
    position: relative;
    border-radius: 6px;
    transition: background .2s linear;
    color: rgba(0, 140, 231, 1);
    outline: 0;
    text-decoration: none;
    margin: 10px 10px 10px 0;
    padding: 10px 20px;
    display: inline-block;
    box-shadow: inset 0 0 0 2px rgba(0, 140, 231, 1);
  }

  .btn::before {
    content: '';
    position: absolute;
    z-index: -1;
    border-radius: 6px;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 140, 231, 1);
    opacity: .2;
    transform: scale(0);
    transition-property: transform;
    transition-duration: .14s;
    transition-timing-function: ease;
  }

  .btn:hover {
    background-color: rgba(0, 140, 231, 1);
    color: #fff;
    cursor: pointer;
  }

  .btn:hover::before {
    opacity: 1;
    transform: scale(1);
  }
</style>
