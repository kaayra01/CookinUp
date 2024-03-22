<template>
  <Banner />
  <Content />
  <Footer />
</template>

<script lang="ts">
import Banner from "./components/Banner.vue";
import Content from "./components/Content.vue";
import Footer from "./components/Footer.vue";

export default {
  name: "App",

  components: {
    Banner,
    Content,
    Footer,
  },
};
</script>

<style scoped></style>
