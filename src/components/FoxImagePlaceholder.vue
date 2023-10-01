<template>
  <div class="image-box" :class="{ bordering: !imageRef }">
      <img v-if="imageRef" :src="imageRef" class="image"/>
      <p v-else>Fox Image Placeholder</p>
  </div>
  <Buttons @click="getFoxImage" :disabled='isLoading' :class="{ disabled: isLoading }"/>
</template>


<script setup>
import { ref } from 'vue';
import { createToast } from 'mosha-vue-toastify';
import 'mosha-vue-toastify/dist/style.css'
import axios from 'axios';
import Buttons from './Buttons.vue';
import { wait } from "../utils/wait.js";

const timeout = 3000
const imageRef = ref(null)
const isLoading = ref(false)

const showNotify = (title, description, toastType = 'info') => {
  return createToast(
      { title, description },
      {
        showIcon: true,
        transition: 'slide',
        type: toastType,
        position: 'bottom-center',
        timeout: timeout,
        swipeClose: true,
      }
  );
}

async function getFoxImage() {
  showNotify('Generating Image...');

  isLoading.value = true;

  const image = await axios.get('https://randomfox.ca/floof/')
      .then(r => r.data.image)
      .catch(() => null);

  await wait(timeout);

  if (!image) {
    isLoading.value = false;
    return showNotify('Error generating image', 'Try again later', 'danger');
  }

  imageRef.value = image;
  showNotify('Successful image generation', '', 'success');
  isLoading.value = false;
}
</script>

<style lang="scss" scoped>
@import "../styles/mixins";

.image-box {
  @include flexbox($justify: center, $align: center);
  border-radius: 17px;
  height: 512px;

  p {
    font-size: 36px;
  }
}

.image {
  object-fit: cover;
  width: 100%;
  height: 100%;
  border-radius: 17px;
}

.bordering {
  border: 4px solid black;
}

.disabled {
  opacity: 0.5;
  cursor: default;

  &:hover {
    opacity: 0.5;
  }
}

@media (max-width: 450px) {
  .image-box {
    width: 380px;
    height: 512px;

    p {
      font-size: 24px;
    }
  }
}

</style>