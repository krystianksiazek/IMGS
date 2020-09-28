<template>
  <div class="main">
    <h1>The IMGS.</h1>
    <h2>Only best photos of space by NASA.</h2>
    <div class="query">
      <label for="search">Search the object </label>
      <input
        id="search"
        name="search"
        placeholder="Eg. Saturn"
        v-model="query"
        @input="search"
      />
      <p class="queryStats">{{amount}}</p>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';

const API = 'https://images-api.nasa.gov/search?q=';
export default {
  name: 'Home',
  data() {
    return {
      query: '',
      results: [],
      amount: 0,
    };
  },
  methods: {
    search: debounce(function search() {
      axios.get(`${API}${this.query}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
          this.amount = this.results.length;
        })
        .catch((error) => {
          console.log(error);
        });
    }, 1000),
  },
};

</script>

<style lang="scss">
  h1, h2 {
    color: white;
    text-shadow: 0 0 20px #FFFFFF;
  }
  .main {
    height: 85%;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 30px;
    margin: 0;
  }
  .query {
    display: flex;
    flex-direction: column;
    width: 250px;
    text-align: center;
    label {
      color: white;
    }
    input {
      border: none;
      height: 30px;
      border-bottom: 1px dashed white;
      color: white;
      background-color: rgba(0, 0, 0, 0);
      text-align: center;
    }
  }
  .queryStats {
    color: white;
  }
</style>
