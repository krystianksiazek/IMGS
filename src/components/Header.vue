<template>
  <div class="wrapper">
    <h1>The IMGS.</h1>
    <h2>NASA's space image search engine.</h2>
  </div>
</template>
<script>
export default {
  name: 'Header',
};
</script>
<style lang="scss" scoped>
.wrapper {
  margin-top: 200px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
h1, h2 {
  color: white;
  text-shadow: 0 0 20px #FFFFFF;
}
</style>
