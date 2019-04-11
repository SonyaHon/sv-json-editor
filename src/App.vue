<template>
  <div id="app">
    <div class="card">
      <sv-json-editor v-model="json" name="root"></sv-json-editor>
    </div>
  </div>
</template>

<script>
import SvJsonEditor from "./components/sv-json-editor.vue";

export default {
  name: "app",
  components: {
    SvJsonEditor
  },
  data() {
    return {
      json: {
        kek: 34,
        lel: true,
        nonsence: "ahahahahha",
        rofl: {
          momma: "string",
          infos: [1, 2, 3]
        },
        arr: [1, 2, 3, { x: 22 }],
        some: {
          x: 10,
          y: [1, 2, 3, 4, 5, 6]
        }
      }
    };
  }
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100%;
  height: 100%;
}
body,
html {
  width: 100%;
  height: 100%;
  margin: 0;
  padding: 0;
}

.card {
  width: 500px;
  height: 600px;
  border-radius: 3px;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 5px;
  box-shadow: 0 0 2px #b0b0b0;
}
</style>
