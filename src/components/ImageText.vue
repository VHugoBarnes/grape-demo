<template>
  <div class="image-text-wrapper">
    <img
      :src="imageSrc"
      :alt="imageAlt"
      @click="onInputImage"
    >
    <p
      :contenteditable="true"
      @input="onInput"
      class="text"
    >{{ content }}
    </p>
  </div>
</template>

<script>
export default {
  name: 'ImageText',
  props: {
    content: {
      type: String,
      default: 'Texto',
    },
    imageSrc: {
      type: String,
      default: 'https://via.placeholder.com/150',
    },
    imageAlt: {
      type: String,
      default: 'Placeholder',
    },
  },
  methods: {
    onInput(event) {
      this.$emit('update:content', event.target.innerText);
    },
    onInputImage(event) {
      this.$emit('update:imageSrc', event.target.src);
    },
  },
};
</script>
