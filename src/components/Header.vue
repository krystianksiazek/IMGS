<template>
  <div class="wrapper">
    <h1 v-bind:class="{'exploringSubheading': (sendState === '1')}" class="heading">
      The IMGS
    </h1>
    <h1 v-bind:class="{'exploringSubheading': (sendState === '0')}" class="exploringHeading">
      IMGS
    </h1>
    <h2 v-bind:class="{'exploringSubheading': (sendState === '1')}" class="subheading">
      Discover amazing space related photos from NASA
    </h2>
  </div>
</template>
<script>
export default {
  name: 'Header',
  props: [
    'sendState',
  ],
};
</script>
<style lang="scss" scoped>
.exploringHeading {
  top: 40px;
  left: 50%;
  transform: translate(-50%, -50%);
  position: absolute;
  transition: opacity 200ms, visibility 200ms;
  transition-delay: 0.5s;
}
.heading {
  font-size: 60px;
  letter-spacing: 5px;
  opacity: 1;
  transition: opacity 200ms, visibility 200ms;
  font-weight: 500;
}
.heading, .subheading {
  color: white;
  text-shadow: 0 0 5px rgb(100, 100, 100);
  text-align: center;
}
.subheading {
  font-size: 30px;
  visibility: visible;
  opacity: 1;
  transition: opacity 200ms, visibility 200ms;
  font-weight: 200;
}
.exploringSubheading {
  visibility: hidden;
  opacity: 0;
  transition: opacity 200ms, visibility 200ms;
}
</style>
