<template>
  <div class="app">
      <router-link class="imgs" to="/">HOME</router-link>
      <router-link class="about" to="/about">ABOUT</router-link>
    <router-view />
  </div>
</template>

<script>
export default {
  name: 'App',
};
</script>

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
    background-attachment: fixed;
    font-family: 'Work Sans', sans-serif;
    background-color: black;
    user-select: none;
    -webkit-user-select: none;
    -khtml-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    scrollbar-color: #888 #3e3e3e;
  }
  body {

    background-image: radial-gradient(rgba(0, 0, 0, 0.2),
    rgba(0, 0, 0, 0.1),
    rgba(0, 0, 0, 0));
  }
  .imgs, .about {
    width: 60px;
    color: white;
    font-size: 15px;
    text-align: center;
    text-decoration: none;
    border: 1px solid rgba(255, 255, 255, 0.5);
    border-radius: 2px;
  }
  .imgs {
    position: absolute;
    top: 10px;
    left: 10px;
  }
  .about {
    position: absolute;
    top: 10px;
    right: 10px;
  }
</style>
