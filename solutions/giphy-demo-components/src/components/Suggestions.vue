<template>
  <div class="suggestions">
    <a href="#" class="btn btn--blue-ghost" v-on:click="onSuggestionClick('Money rain')">Money rain</a>
    <a href="#" class="btn btn--blue-ghost" v-on:click="onSuggestionClick('Vue')">Vue</a>
    <a href="#" class="btn btn--blue-ghost" v-on:click="onSuggestionClick('Javascript')">Javascript</a>
    <a href="#" class="btn btn--blue-ghost" v-on:click="onSuggestionClick('Party')">Party</a>
    <a href="#" class="btn btn--blue-ghost" v-on:click="onSuggestionClick('anwb')">Anwb</a>
  </div>
</template>

<script>
export default {
  name: 'Suggestions',
  
  methods: {
    onSuggestionClick(searchQuery) {
      // call parent submitforn on suggestion click
     this.$parent.submitForm(searchQuery);
    },
  }
}
</script>

<style scoped>
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