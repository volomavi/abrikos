<template>
  <div>
    <the-header title="Fun with Curie!"></the-header>
    <the-resources></the-resources>
  </div>
  <div class="container"></div>
</template>

<script>
import TheHeader from "./components/layouts/TheHeader.vue";
import TheResources from "./components/learning-resources/TheResources.vue";
export default {
  components: {
    TheHeader,
    TheResources,
  },
};

</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap");

* {
  box-sizing: border-box;
}

html {
  font-family: "Roboto", Helvetica, Arial, sans-serif, sans-serif;
}

body {
  margin: 0;
}

h2 {
  display: flex;
  justify-content: center;
  color: #004c3f;
}
</style>
