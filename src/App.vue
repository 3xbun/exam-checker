<script setup>
import Header from "./components/Header.vue";
import Calculator from "./components/Calculator.vue";
import Footer from "./components/Footer.vue";
</script>

<template>
  <Header />
  <div class="container">
    <Calculator />
  </div>
  <Footer />
</template>

<style>
@import url("https://fonts.googleapis.com/css2?family=Prompt:wght@300&display=swap");

* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
  font-family: "Prompt", sans-serif;
}

.container {
  width: 85vw;
  margin: auto;
  padding: 1em;
  margin-top: 2em;
  border-radius: 1em;
  max-width: 800px;
  box-shadow: 0 3px 6px rgba(0, 0, 0, 0.16), 0 3px 6px rgba(0, 0, 0, 0.23);
}

h1 {
  text-align: center;
  font-size: 3em;
}
</style>
