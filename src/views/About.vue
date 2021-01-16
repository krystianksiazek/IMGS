<template>
  <div class="wrapper">
    <h1>
      IMGS
    </h1>
    <h2>
      NASA's space photos exploring app
    </h2>
    <h3>
      Designed and created by <a href="https://github.com/krystianksiazek">Krystian Książek</a>
    </h3>
    <h3>
      <a href="https://github.com/krystianksiazek/IMGS">Source</a>
    </h3>
  </div>
</template>

<script>
export default {
  name: 'About',
};
</script>

<style lang="scss" scoped>
  .wrapper {
    background: radial-gradient(rgba(0, 0, 0, 0.9), rgba(0,0,0,0.1));
    z-index: 1;
    text-shadow: 0 0 5px rgb(100, 100, 100);
    animation: fadeInAnimation ease 2s;
    animation-iteration-count: 1;
    animation-fill-mode: forwards;
  }
  @keyframes fadeInAnimation {
    0% {
      opacity: 0;
    }
    100% {
      opacity: 1;
    }
  }
  h1 {
    font-size: 60px;
    letter-spacing: 5px;
    font-weight: 500;
    text-align: center;
    border-bottom: 1px solid white;
    box-shadow: 0 10px 8px -5px rgba(255, 255, 255, 0.2);
    margin: 0 10px 0 10px;
    animation: puls 2s ease-out infinite;
    @media (max-width: 768px)
    {
      font-size: 50px;
    }
  }
  @keyframes puls {
    0%   { box-shadow: 0 0 0 rgba(255, 255, 255, 0.2); }
    50%  { box-shadow: 0 10px 8px -5px rgba(255, 255, 255, 0.2); }
    100% { box-shadow: 0 0 0 rgba(255, 255, 255, 0.2); }
  }
  h2, h3 {
    font-size: 30px;
    text-align: center;
    margin: 20px 10px 0 10px;
    font-weight: 200;
    @media (max-width: 768px)
    {
      font-size: 23px;
    }
  }
  h3 {
    font-size: 25px;
    text-align: center;
    margin: 20px 10px 0 10px;
    font-weight: 200;
    @media (max-width: 768px)
    {
      font-size: 18px;
    }
  }
  a {
    text-decoration: underline;
    color: white;
    font-weight: 500;
  }

</style>
