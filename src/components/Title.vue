<template>
  <h1
    :contenteditable="true"
    @click="onInput"
    class="title"
  >{{ content }}</h1>
</template>

<script>
export default {
  name: 'TitleComponent',
  props: {
    content: {
      type: String,
      default: 'Título',
    },
  },
  methods: {
    onInput(event) {
      this.$emit('update:content', event.target.innerText);
    },
  },
};
</script>

<style scoped>
.title {
  font-size: 2em;
  color: #303030;
  font-weight: 700;
}
</style>
