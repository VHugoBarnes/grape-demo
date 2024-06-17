<template>
  <div id="app">
    <!-- <div class="panel__top">
      <div class="panel__devices"></div>
      <div class="panel__basic-actions"></div>
    </div> -->
    <div id="blocks"></div>
    <GrapeEditor />
  </div>
</template>

<script>
import GrapeEditor from './Editor.vue';

export default {
  name: 'App',
  components: {
    GrapeEditor,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
