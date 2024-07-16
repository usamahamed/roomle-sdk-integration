<template>
  <SceneView :objectId="objectId" />
</template>

<script>
import SceneView from "./components/SceneView.vue";
import { ref } from "vue";

export default {
  name: "App",
  components: {
    SceneView,
  },
  setup() {
    const objectId = ref("");
    const urlParams = new URLSearchParams(window.location.search);
    const id = urlParams.get("id");
    // try to append ?id=roomle_content_demo:electronics003 to
    // the URL and see what's happening
    if (id) {
      objectId.value = id;
    }
    return {
      objectId,
    };
  },
};
</script>

<style>
body {
  margin: 0;
  padding: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  width: 100%;
  height: 100vh;
  background-color: lightgray;
}
</style>
