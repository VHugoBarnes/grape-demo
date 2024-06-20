<template>
  <h1
    :contenteditable="true"
    @input="onInput"
    class="title"
  >
    {{ content }}
  </h1>
</template>

<script>
export default {
  name: 'TitleComponent',
  props: {
    content: {
      type: String,
      default: 'KEKO KAKA',
    },
    onUpdateContent: {
      type: Function,
      required: true,
    },
  },
  methods: {
    onInput(event) {
      this.onUpdateContent(event.target.innerText);

      // console.log("onInput", event.target.innerText)
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
