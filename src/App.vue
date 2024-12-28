<template>
  <div id="app">
    <msgPage></msgPage>
    <div id="self_word-line">添加至词库</div>
  </div>
</template>

<script>
import msgPage from "./pages/msgPage.vue";

export default {
  name: "App",
  components: {
    msgPage,
  },
};
</script>

<style>
#app {
}
</style>
