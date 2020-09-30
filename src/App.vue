<template>
  <div class="app">
      <router-link class="imgs" to="/">IMGS</router-link>
      <router-link class="about" to="/about">about</router-link>
    <router-view />
  </div>
</template>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css2?family=Work+Sans:wght@300;500;700&display=swap');
  html, body {
    height: 100%;
    margin: 0;
    color: white;
  }
  .app {
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  html {
    background-image: url("assets/background.jpg");
    background-repeat: no-repeat;
    background-size: cover;
    background-position: center;
    font-family: 'Work Sans', sans-serif;
    background-color: black;

  }
  body {

    background-image: radial-gradient(rgba(0, 0, 0, 0.4),
    rgba(0, 0, 0, 0.2),
    rgba(0, 0, 0, 0));
  }
  .imgs {
    position: absolute;
    top: 5px;
    left: 10px;
  }
  .about {
    position: absolute;
    top: 5px;
    right: 10px;
  }
</style>
