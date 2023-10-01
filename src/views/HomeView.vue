<template>
  <main>
    <h1>Fox Image</h1>
    <Placeholder/>
  </main>
</template>

<script setup>
import Placeholder from '../components/FoxImagePlaceholder.vue'
</script>

<style lang="scss" scoped>
@import "../styles/mixins.scss";

main {
  @include flexbox($justify: center, $align: center);
  height: 100vh;
  font-family: "Inter", sans-serif;
  flex-direction: column;
}

h1 {
  color: #fff;
  margin: 20px;
}

</style>
