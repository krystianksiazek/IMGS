<template>
  <div class="mainWrapper">
    <Modal v-if="modalOpen" :item="modalData" :modalState="modalOpen"
    @close-modal="modalOpen = false; showScroll()" />
    <Header :sendState="state" />
    <Search :sendState="state" :sendResults="results" v-model='query' @input='search'/>
    <p v-bind:class="{'exploringQueryStats': (state === '1')}" class="queryStats">Amount of results:
      <span v-if="results.length >= 100">></span>{{results.length}}
    </p>
    <div class = "results" v-if="state === '1'">
      <div class="imageBody"
      v-for="results in results" :key="results.data[0].nasa_id"
      v-bind:style="{ 'background-image': 'url(' + results.links[0].href + ')' }"
      @click="handleModalOpen(results)">
      <span class="imageTitle">↓ {{results.data[0].title}} ↓</span>
      </div>
    </div>
    <div v-on:click="scrollToTop" id='topBtn'>TOP</div>
  </div>
</template>

<script>
import Header from '@/components/Header.vue';
import Modal from '@/components/Modal.vue';
import Search from '@/components/Search.vue';
import axios from 'axios';
import debounce from 'lodash.debounce';

const API = 'https://images-api.nasa.gov/search?q=';
export default {
  name: 'Main',
  components: {
    Header,
    Modal,
    Search,
  },
  data() {
    return {
      modalOpen: false,
      modalData: null,
      query: '',
      results: [],
      loading: false,
      state: '0',
    };
  },
  created() {
    window.addEventListener('scroll', this.scrollListener);
  },
  methods: {
    // wakeUp:
    //   function wakeUp() {
    //     this.state = '1';
    //   },
    handleModalOpen(item) {
      this.modalOpen = true;
      this.modalData = item;
      document.body.style.overflow = 'hidden';
    },
    showScroll() {
      document.body.style.overflow = 'auto';
    },
    scrollToTop:
    function top() {
      const topPoint = document.documentElement.scrollTop || document.body.scrollTop;
      if (topPoint > 0) {
        window.requestAnimationFrame(top);
        window.scrollTo(0, topPoint - topPoint / 10);
      }
    },
    scrollListener:
    function scrollFunction() {
      if (this.state === '1') {
        if (document.body.scrollTop > 20 || document.documentElement.scrollTop > 20) {
          document.querySelector('#topBtn').style.display = 'block';
        } else {
          document.querySelector('#topBtn').style.display = 'none';
        }
      }
    },
    search:
    debounce(function search() {
      this.loading = true;
      if (document.getElementById('search').value === ''
      || (document.getElementById('search').value).startsWith(' ')) {
        this.results = [];
        this.state = '0';
        this.loading = false;
      } else {
        axios.get(`${API}${this.query}&media_type=image`)
          .then((response) => {
            this.loading = false;
            this.state = '1';
            this.results = response.data.collection.items;
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
  .inputNegativeResults {
    border-bottom: 2px solid rgb(136, 0, 5) !important;
  }
  .inputNegativeResults:focus {
    box-shadow: 0 10px 8px -4px rgba(194, 0, 7, 0.2) !important;
    @media (max-width: 768px)
    {
      box-shadow: 0 15px 8px -4px rgba(194, 0, 7, 0.2) !important;
    }
  }
  .inputPositiveResults {
    border-bottom: 2px solid rgb(0, 136, 5) !important;
  }
  .inputPositiveResults:focus {
    box-shadow: 0 10px 8px -4px rgba(0, 194, 7, 0.2) !important;
    @media (max-width: 768px)
    {
      box-shadow: 0 15px 8px -4px rgba(0, 194, 7, 0.2) !important;
    }
  }
  .exploringInput {
    top: 100px;
    left: 50%;
    transform: translate(-50%, -50%);
    position: absolute;
    width: 250px;
  }
  .mainWrapper {
    text-shadow: 0 0 5px rgb(100, 100, 100);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 30px;
    margin: 0;
    animation: fadeInAnimation ease 2s;
    animation-iteration-count: 1;
    animation-fill-mode: forwards;
  }
  .query {
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
      visibility: visible;
      opacity: 1;
      transition: opacity 200ms, visibility 200ms;
    }
    .exploringLabel {
      visibility: hidden;
      opacity: 0;
      transition: opacity 200ms, visibility 200ms;
    }
    input {
      font-weight: 800;
      font-size: 18px;
      border: none;
      height: 30px;
      border-bottom: 2px solid white;
      color: white;
      background-color: rgba(0, 0, 0, 0);
      text-align: center;
      transition: box-shadow .5s ease-out;
      padding: 0px;
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
    visibility: hidden;
    opacity: 0;
  }
  .exploringQueryStats {
    color: white;
    visibility: visible;
    opacity: 1;
    top: 130px;
    left: 50%;
    transform: translate(-50%, -50%);
    position: absolute;
    transition: opacity 600ms, visibility 600ms;
    transition-delay: 0.5s;
  }
  .results {
    margin-bottom: 20px;
    cursor: pointer;
    text-align: center;
    top: 200px;
    position: absolute;
    display: grid;
    max-width: min-content;
    grid-template-columns: repeat(4, 1fr);
    background-color: rgba(0, 0, 0, 0.8);
    box-shadow: 0 0 30px 20px rgba(0, 0, 0, 0.9);
    @media (max-width: 1700px)
    {
      grid-template-columns: repeat(3, 1fr);
    }
    @media (max-width: 1300px)
    {
      grid-template-columns: repeat(2, 1fr);
    }
    @media (max-width: 900px)
    {
      grid-template-columns: 1fr;
    }
  }
  .imageBody {
    height: 400px;
    width: 400px;
    background-size: cover;
    background-position: 50%;
    background-repeat: no-repeat;
    @media (max-width: 900px)
    {
      height: 340px;
      width: 340px;
    }
  }
  .imageBody:last-child {
    align-self: center;
  }
  .imageTitle {
    background-color: black;
    padding: 5px;
    line-height: 15px;
    display: block;
    text-shadow: none;
  }
  #topBtn {
    cursor: pointer;
    padding: 5px;
    color: white;
    font-size: 20px;
    text-align: center;
    text-decoration: none;
    background-color: black;
    border: 1px solid rgba(255, 255, 255, 0.5);
    text-shadow: none;
    display: none;
    position: fixed;
    bottom: 10px;
    right: auto;
    border-radius: 4px;
    max-width: min-content;
  }

  @keyframes fadeInAnimation {
    0% {
      opacity: 0;
    }
    100% {
      opacity: 1;
    }
  }
</style>
