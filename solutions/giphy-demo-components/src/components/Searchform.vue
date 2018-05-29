<template>
  <form @submit.prevent="submitForm()">
    <input type="search" placeholder="Zoek je gif" v-model="searchQuery" />
  </form>
</template>

<script>
export default {
  name: 'searchform',

  props: {
        searchQuery: {
            type: String,
            required: true
        }
  },

  methods: {
    submitForm() {
        // Call submitform in parent component
        this.$parent.submitForm(this.searchQuery);
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
