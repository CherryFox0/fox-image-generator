<template>
    <button class="styled-button">Get Fox Image</button>
</template>

<script setup>

</script>

<style lang="scss" scoped>
@import "../styles/mixins";

.styled-button {
  @include styled-button;
  background: #ffa550;
  border: none;
  margin-top: 20px;
  height: 50px;
  width: 300px;

  &:hover {
    opacity: 0.8;
  }

  &:active {
    transform: scale(0.9);
  }
}

</style>