<template>
  <form v-on:submit.prevent="submitForm(searchQuery)">
    <input type="search" placeholder="Zoek je gif" v-model="searchQuery" />
  </form>
</template>

<script>
import { EventBus } from '../eventbus.js';

export default {
  name: 'searchform',

  data() {
    return {
      searchQuery: '',
    };
  },

  created() {
    this.searchQuery = 'Money rain';
    
    // Listen to events from Suggestions
    EventBus.$on('suggestion-clicked', (searchQuery) => {
      this.searchQuery = searchQuery;
    });
  },

  methods: {
    submitForm(searchQuery) {
      // Send the event on a channel (form-submit) with a payload (the searchQuery)
      EventBus.$emit('searchform-submit', searchQuery);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
</style>
