<template>
  <div class="container">
    <div ref="scene" class="scene"></div>
  </div>
</template>

<script>
import RoomleSdk from "@roomle/web-sdk";
import { onMounted, ref } from "vue";

export default {
  name: "HelloWorld",
  props: {
    objectId: String,
  },
  setup(props) {
    window.__RML__ENV__ = {
      assetPath: "/roomle/",
    };
    const scene = ref(null);
    let rubensConfiguratorApi = null;
    let rubensConfigurator = null;
    onMounted(async () => {
      RoomleSdk.setGlobalInitData({
        customApiUrl: "https://api.roomle.com/v2",
        ls: "shelf",
      });
      rubensConfigurator = await RoomleSdk.getConfigurator();
      rubensConfigurator.boot();
      rubensConfiguratorApi = await rubensConfigurator.getApi();
      await rubensConfiguratorApi.init(scene.value);
      const initialId = props.objectId || "usm:frame";
      await rubensConfiguratorApi.loadConfigurableItemById(initialId);
    });

    return { scene };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
  width: 70%;
  height: 100%;
}
.scene {
  width: 100%;
  height: 100%;
}
</style>
