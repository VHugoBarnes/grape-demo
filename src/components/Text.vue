<template>
  <p
    :contenteditable="true"
    @input="onInput"
    class="text"
  >{{ content }}</p>
</template>

<script>
export default {
  name: 'TextComponent',
  props: {
    content: {
      type: String,
      default: 'Texto',
    },
  },
  methods: {
    onInput(event) {
      this.$emit('update:content', event.target.innerText);
    },
  },
};
</script>
