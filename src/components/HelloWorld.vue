<script lang="ts">
import { defineComponent } from "vue";
export default defineComponent({
  name: "HelloWorld",
  props: {
    msg: String,
  },
  setup() {
    const uniSdk = uni;

    return {
      uniSdk,
    };
  },
  mounted() {
    this.onBtnClick("孙组件初始化传讯");
    document.addEventListener("UniAppJSBridgeReady", () => {
      this.onBtnClick("孙组件等待UniAppJSBridgeReady后传讯");
    });
    setTimeout(() => {
      this.onBtnClick("孙组件等待3秒后传讯");
    }, 3000);
  },
  methods: {
    onEmitClick() {
      this.$emit("emitChildren", "孙组件提级传讯测试");
    },
    onBtnClick(text: string) {
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
  <div class="greetings">
    <h1 class="green">{{ msg }}</h1>
    <button @click="onBtnClick('孙组件点击传讯')">孙组件传讯测试</button>
    <button @click="onEmitClick()">孙组件提级传讯测试</button>
  </div>
</template>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}

.greetings {
  background: #f1f1f1;
}

.greetings h1,
.greetings h3 {
  text-align: center;
}

@media (min-width: 1024px) {
  .greetings h1,
  .greetings h3 {
    display: block;
    text-align: left;
  }
}
</style>
