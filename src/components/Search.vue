<template>
  <div class="searchWrapper">
    <div class="query">
      <label v-bind:class="{'exploringLabel': (sendState === '1')}" for="search">
          Type space related thing to start</label>
      <input
        v-bind:class="{'inputNegativeResults': (sendResults.length === 0) && (sendState === '1'),
        'inputPositiveResults': (sendResults.length > 0) && (sendState === '1'),
        'exploringInput': (sendState === '1')}"
        id="search"
        name="search"
        placeholder="Eg. Saturn"
        autocomplete="off"
        @input="wakeUp"
      />
    </div>
  </div>
</template>
<script>
export default {
  name: 'Search',
  props: {
    sendState: {
      type: String,
      required: true,
    },
    sendResults: {
      type: Array,
      required: true,
    },
  },
  methods: {
    wakeUp(sendQuery) {
      this.$emit('input', sendQuery.target.value);
    },
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
</style>
