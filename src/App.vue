<template>
  <div id="app">
    <TelegramEmbed link="telegram/83" />
  </div>
</template>

<script>
import TelegramEmbed from "./components/vue-telegram-embed";

export default {
  name: "App",
  components: {
    TelegramEmbed
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
