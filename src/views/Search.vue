<template>
  <div class="search">
    <Header />
    <div class="query">
      <label for="search">Search the object</label>
      <input
        id="search"
        name="search"
        placeholder="Eg. Saturn"
        v-model="query"
        @input="search"
      />
      <p class="queryStats">Amount of results: {{amount}}</p>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Header from '@/components/Header.vue';

const API = 'https://images-api.nasa.gov/search?q=';
export default {
  name: 'Search',
  data() {
    return {
      query: '',
      results: [],
      amount: 0,
    };
  },
  components: { Header },
  methods: {
    search: debounce(function search() {
      if (document.getElementById('search').value === '') {
        this.amount = 0;
        this.results = [];
      } else {
        axios.get(`${API}${this.query}&media_type=image`)
          .then((response) => {
            this.results = response.data.collection.items;
            if (this.results.length >= 100) {
              this.amount = `>${this.results.length}`;
            } else this.amount = this.results.length;
          })
          .catch((error) => {
            console.log(error);
          });
      }
    }, 1000),
  },
};

</script>

<style lang="scss" scoped>
  .search {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 30px;
    margin: 0;
  }
  .query {
    text-shadow: 0 0 20px #FFFFFF;
    margin-top: 150px;
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
