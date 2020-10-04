<template>
  <div v-bind:class="{'startExploring': (state === 1)}" class="mainWrapper">
    <Header :sendState="state" />
    <div class="query">
      <label v-if="state === '0'" for="search">Type space-related thing to start</label>
      <input
        id="search"
        name="search"
        placeholder="Eg. Saturn"
        autocomplete="off"
        v-model="query"
        @input="search"
      />
      <p class="queryStats">Amount of results: {{amount}}</p>
    </div>
  </div>
</template>

<script>
import Header from '@/components/Header.vue';
import axios from 'axios';
import debounce from 'lodash.debounce';

const API = 'https://images-api.nasa.gov/search?q=';
export default {
  name: 'Main',
  components: {
    Header,
  },
  data() {
    return {
      query: '',
      results: [],
      amount: 0,
      isLoading: false,
      state: '0',
    };
  },
  methods: {
    search:
    debounce(function search() {
      this.isLoading = true;
      if (document.getElementById('search').value === '') {
        this.amount = 0;
        this.results = [];
        this.state = '0';
        this.isLoading = false;
      } else {
        axios.get(`${API}${this.query}&media_type=image`)
          .then((response) => {
            this.isLoading = false;
            this.state = '1';
            this.results = response.data.collection.items;
            if (this.results.length >= 100) {
              this.amount = `>${this.results.length}`;
            } else if (this.results.length === 0) {
              this.state = '0';
              this.isLoading = false;
            } else {
              this.amount = this.results.length;
            }
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
  .mainWrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 30px;
    margin: 0;
  }
  .query {
    text-shadow: 0 0 10px rgb(200, 200, 200);
    margin-top: 60px;
    display: flex;
    flex-direction: column;
    width: 250px;
    text-align: center;
    label {
      font-weight: 300;
      font-size: 16px;
      color: white;
      margin-bottom: 10px;
    }
    input {
      font-weight: 800;
      font-size: 15px;
      border: none;
      height: 30px;
      border-bottom: 1px dashed white;
      color: white;
      background-color: rgba(0, 0, 0, 0);
      text-align: center;
      transition: box-shadow .5s ease-out;
    }
    input:focus {
      outline: none;
      box-shadow: 0 10px 8px -4px rgba(255, 255, 255, 0.2);
      @media (max-width: 768px)
      {
        box-shadow: 0 15px 8px -4px rgba(255, 255, 255, 0.2);
      }
    }
  }
  .queryStats {
    color: white;
  }
</style>
