<template>
  <div class="modalWrapper">
    <div class="titleAndClose">
      <span class="title">
        Księżyc
      </span>
    </div>
    <div class="content">
      <div class="photo">
      </div>
      <div class="aboutPhoto">
        <h1>Księżyc</h1>
        <p class="description">
          Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor
          incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam,
          quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.
          Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu
          fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident,
          sunt in culpa qui officia deserunt mollit anim id est laborum.
        </p>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'Modal',
};
</script>
<style lang="scss" scoped>
  .modalWrapper {
    width: 80%;
    position: absolute;
    background-color: grey;
    // border: 1px solid rgba(255, 255, 255, 0.5);
    border-radius: 2px;
    @media (max-width: 1000px)
    {
      width: 100% !important;
      height: 100% !important;
    }
  }
  .titleAndClose {
    display: block;
    background-color: black;
    text-align: center;
    height: 20px;
  }
  .content {
    display: flex;
    height: 70vh;
    @media (max-width: 1000px)
    {
      flex-direction: column;
      height: calc(100% - 20px);
    }
  }
  .aboutPhoto {
    text-align: center;
    width: 50%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    padding-left: 20px;
    @media (max-width: 1000px)
    {
      width: 100%;
      height: 50%;
      padding-left: 0;
    }
  }
  .photo {
    width: 50%;
    height: 100%;
    background-image: url('https://cdn2.techmaniak.pl/wp-content/uploads/mobimaniak/2016/02/8cG66eARi-large.jpg');
    background-repeat: no-repeat;
    background-size: contain;
    background-position: 50%;
    @media (max-width: 1000px)
    {
      width: 100%;
      height: 50%;
    }
  }
</style>
