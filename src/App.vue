<script lang="ts">
import HelloWorld from "@/components/HelloWorld.vue";
import { defineComponent, onMounted } from "vue";
export default defineComponent({
  components: {
    HelloWorld,
  },
  setup() {
    const uniSdk = uni;
    const msg = "孙组件测试";
    return {
      uniSdk,
      msg,
    };
  },
  mounted() {
    this.emitData("子组件初始化传讯");
    document.addEventListener("UniAppJSBridgeReady", () => {
      this.emitData("子组件等待UniAppJSBridgeReady后传讯");
    });
    setTimeout(() => {
      this.emitData("子组件等待3秒后传讯");
    }, 3000);
  },
  methods: {
    emitData(text: string) {
      console.log(text);
      const info = {
        name: text,
      };
      this.uniSdk.postMessage({
        data: {
          info,
        },
      });
    },
  },
});
</script>

<template>
  <div id="app">
    <button @click="emitData('子组件点击传讯')">子传父</button>
    <HelloWorld :msg="msg" @emitChildren="emitData" />
  </div>
</template>

<style scoped></style>
