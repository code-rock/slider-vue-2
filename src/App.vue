<template>
  <div id="app">
    <header>
      <MyButton v-on:click="fetchImages"> Загрузить </MyButton>

      <p class="counter">В слайдере {{ max }} изображений</p>
    </header>

    <main>
      <h2 v-if="isImagesLoading">Идет загрузка...</h2>
      <MySlider v-else-if="images.length" :images="images" />
      <h2 v-else>Ничего не найдено...</h2>
    </main>
  </div>
</template>

<script>
import MyButton from "@/components/MyButton.vue";
import MySlider from "@/components/MySlider.vue";
import axios from "axios";

export default {
  components: {
    MySlider,
    MyButton,
  },
  data() {
    return {
      id: 0,
      images: [],
      max: 0,
      isImagesLoading: false,
    };
  },
  methods: {
    async fetchImages() {
      try {
        this.isImagesLoading = true;
        const response = await axios.get(
          "https://jsonplaceholder.typicode.com/albums/1/photos?_limit=10"
        );
        this.images = response.data;
        this.max = response.data.length;
        localStorage.setItem("images", JSON.stringify(response.data));
      } catch (e) {
        console.warn(e);
      } finally {
        this.isImagesLoading = false;
      }
    },
  },
  mounted() {
    try {
      this.isImagesLoading = true;
      const loaded = JSON.parse(localStorage.getItem("images"));
      this.images = loaded;
      this.max = loaded.length;
    } catch (e) {
      console.warn(e);
    } finally {
      this.isImagesLoading = false;
    }
  },
};
</script>

<style scoped>
  header {
    line-height: 1.5;
    display: flex;
    align-items: center;
    margin-bottom: 20px;
  }

  .counter {
      margin-left: 20px;
  }

  @media (min-width: 1024px) {
    header {
      display: flex;
      place-items: center;
      padding-right: calc(var(--section-gap) / 2);
    }
  }
</style>
