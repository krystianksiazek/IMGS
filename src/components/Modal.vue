<template>
  <div class="dimmer">
    <div class="modalWrapper">
      <div class="titleAndClose">
        <span class="title">
          {{ title }} (ID: {{ id }})
        </span>
        <a class="close" @click="$emit('close-modal')" />
      </div>
      <div class="content">
        <div class="photo" @click="myhref(fullSize)"
         v-bind:style="{ backgroundImage: 'url(' + photo + ')' }">
        </div>
        <div class="aboutPhoto">
          <h1>{{ title }}</h1>
          <p class="description">
            {{ description }}
            <br><br>
            <span v-if="location != null">Location: {{ location }}</span>
            <br>
            <span v-if="date != null">Date: {{ date }}</span>
          </p>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'Modal',
  props: {
    item: {
      type: Object,
      required: true,
    },
    modalState: {
      type: Boolean,
      required: true,
    },
  },
  data() {
    return {
      id: null,
      location: null,
      date: null,
      photo: null,
      title: null,
      description: null,
      fullSize: null,
    };
  },
  mounted() {
    this.id = this.item.data[0].nasa_id;
    this.location = this.item.data[0].location;
    this.date = this.item.data[0].date_created;
    this.photo = this.item.links[0].href;
    this.title = this.item.data[0].title;
    this.description = this.item.data[0].description;
    this.fullSize = this.item.href;
  },
  methods: {
    myhref(href) {
      // window.open(links, '_blank');
      console.log(href);
      // window.location.href = href;
    },
  },
};
</script>
<style lang="scss" scoped>
  .dimmer {
    display: flex;
    align-items: center;
    justify-content: center;
    position: fixed;
    top: 0;
    left: 0;
    height: 100%;
    width: 100%;
    z-index: 2;
    background-color: rgba(0,0,0,0.6);
  }
  .modalWrapper {
    width: 80%;
    position: absolute;
    background-color: rgb(70, 70, 70);
    // border: 1px solid rgba(255, 255, 255, 0.5);
    border-radius: 2px;
    z-index: 3;
    @media (max-width: 1000px)
    {
      width: 100% !important;
      height: 100% !important;
    }
  }
  .titleAndClose {
    overflow: hidden;
    display: flex;
    background-color: black;
    height: 30px;
    align-items: center;
    justify-content: center;
  }
  .content {
    display: flex;
    height: 70vh;
    @media (max-width: 1000px)
    {
      flex-direction: column;
      height: calc(100% - 30px);
    }
  }
  .aboutPhoto {
    text-shadow: 0 0 10px #555;
    text-align: center;
    width: 50%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    @media (max-width: 1000px)
    {
      width: 100%;
      height: 50%;
    }
  }
  .photo {
    cursor: pointer;
    width: 50%;
    height: 100%;
    background-image: "";
    background-repeat: no-repeat;
    background-size: contain;
    background-position: 50%;
    @media (max-width: 1000px)
    {
      width: 100%;
      height: 50%;
    }
  }
  .description {
    overflow: auto;
    margin: 0 20px 0 20px;
  }
  .close {
    cursor: pointer;
    position: absolute;
    right: 0;
    top: 0;
    width: 30px;
    height: 30px;
    opacity: 0.5;
  }
  .close:hover {
    opacity: 1;
  }
  .close:before, .close:after {
    position: absolute;
    left: 13px;
    content: ' ';
    height: 30px;
    width: 2px;
    background-color: rgba(255, 255, 255);
  }
  .close:before {
    transform: rotate(45deg);
  }
  .close:after {
    transform: rotate(-45deg);
  }

</style>
