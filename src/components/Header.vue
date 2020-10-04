<template>
  <div v-bind:class="{'startExploringWrapper': (sendState === '1')}" class="wrapper">
    <h1 class="heading">The IMGS</h1>
    <h2 v-if="sendState === '0'" class="subheading">Discover amazing
      photos of space objects from NASA</h2>
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
.wrapper {
  transition: top 1s ease-out;
  transition: position 1s ease-out;
  top: 20%;
}
.heading {
  font-size: 60px;
  letter-spacing: 5px;
}
.heading, .subheading {
  color: white;
  text-shadow: 0 0 10px rgb(200, 200, 200);
  text-align: center;
}
.subheading {
  font-weight: 500;
}
.startExploringWrapper {
  transition: top 1s ease-out;
  top: 10px;
  position: absolute;
}
</style>
