<script lang="ts">
import { defineComponent } from "vue";
export default defineComponent({
  setup() {
    const emitData = () => {
      const uniSdk = uni;
      const info = {
        name: "wft",
        age: 18,
      };
      console.log(uniSdk, info);
      uniSdk.postMessage({
        data: {
          info,
        },
      });
    };
    return {
      emitData,
    };
  },
});
</script>

<template>
  <div id="app">
    <button @click="emitData">子传父</button>
  </div>
</template>

<style scoped></style>
