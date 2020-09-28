<template>
  <div class="app">
    <div class="nav">
      <router-link to="/">IMGS</router-link>
      |
      <router-link to="/about">about</router-link>
    </div>
    <router-view />
  </div>
</template>

<style lang="scss">
  html, body {
    height: 100%;
    margin: 0;
    color: white;
  }
  .app {
    height: 100%;
  }
  body {
    background-image: url("assets/background.jpg");
    background-repeat: no-repeat;
    background-size: cover;
    background-position: center;
    font-family: "Lucida Console", Courier, monospace;
    background-color: black;
  }
</style>
