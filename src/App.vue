<template>
  <div class="app">
    <router-link class="imgs" to="/">HOME</router-link>
    <router-link class="about" to="/about">ABOUT</router-link>
    <canvas id="stars" />
    <router-view />
  </div>
</template>

<script>
export default {
  name: 'App',
  mounted() {
    /* eslint-disable */
    const field = document.getElementById('stars');
    const ctx = field.getContext('2d');
    const stars = {};
    let starIndex = 0;
    let numStars = 0;
    let acceleration = 1;
    let starsToDraw = (field.width * field.height) / 100;

    function Star() {
      this.X = field.width / 2;
      this.Y = field.height / 2;
      this.SX = Math.random() * 10 - 5;
      this.SY = Math.random() * 10 - 5;
      let start = 20;
      if (field.width > field.height) start = field.width;
      else start = field.height;
      this.X += this.SX * start / 30;
      this.Y += this.SY * start / 30;
      this.radius = Math.random();
      this.age = 0;
      this.dies = 100;
      starIndex++;
      stars[starIndex] = this;
      this.id = starIndex;
      this.color = '#ffffff';
    }
    Star.prototype.Draw = function () {
      this.X += this.SX;
      this.Y += this.SY;
      this.SX += this.SX / (500 / acceleration);
      this.SY += this.SY / (500 / acceleration);
      this.age++;
      if (this.age >= 10) {
        this.radius += 0.001;
      }
      if (this.X + this.radius < 0 | this.X > field.width
        | this.Y + this.radius < 0 | this.Y > field.height) {
        delete stars[this.id];
        numStars--;
      }
      ctx.beginPath();
      ctx.arc(this.X, this.Y, this.radius, 0, 2*Math.PI);
      ctx.fillStyle = this.color;
      ctx.fill();
    };
    field.width = window.innerWidth;
    field.height = window.innerHeight;
    function draw() {
      if (field.width != window.innerWidth) field.width = window.innerWidth;
      if (field.height != window.innerHeight) field.height = window.innerHeight;
      ctx.fillStyle = 'rgba(0, 0, 0, 0.8)';
      ctx.fillRect(0, 0, field.width, field.height);
      for (let i = numStars; i < starsToDraw; i++) {
        new Star();
        numStars++;
      }
      for (const star in stars) {
        stars[star].Draw();
      }
      window.requestAnimationFrame(draw);
    }
    window.requestAnimationFrame(draw);
  },
};
</script>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css2?family=Work+Sans:wght@300;500;700&display=swap');
  #field {
    position: fixed;
    z-index: 1;
  }
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
    // background-image: url("assets/background(compressed).jpg");
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
    background-image: radial-gradient(rgba(0, 0, 0, 0.4),
    rgba(0, 0, 0, 0.2),
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
    z-index: 2;
    position: absolute;
    top: 10px;
    left: 10px;
  }
  .about {
    z-index: 2;
    position: absolute;
    top: 10px;
    right: 10px;
  }
</style>
