<template>
  <div class="wrapper">
    <h1 class="heading">The IMGS</h1>
    <h2 class="subheading">NASA's space image search engine.</h2>
  </div>
</template>
<script>
export default {
  name: 'Header',
};
</script>
<style lang="scss" scoped>
.wrapper {
  display: flex;
  flex-direction: column;
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
</style>
