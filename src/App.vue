<template>
  <div>
    <h1>create-liff-app</h1>
    <p v-if="message">{{ message }}</p>
    <p v-if="error">
      <code>{{ error }}</code>
    </p>
    <a href="https://developers.line.biz/ja/docs/liff/" target="_blank" rel="noreferrer">
      LIFF Documentation
    </a>
    <p>hallo inspector</p>
  </div>
</template>

<script>
import liff from "@line/liff";
import LIFFInspectorPlugin from "@line/liff-inspector";


export default {
  data() {
    return {
      message: "",
      error: ""
    };
  },
  mounted() {
    liff.use(new LIFFInspectorPlugin())
    // liff.use(new LIFFInspectorPlugin({ origin: 'wss://darling-starburst-32a83d.netlify.app' }))

    liff
      .init({
        liffId: import.meta.env.VITE_LIFF_ID
      })
      .then(() => {
        this.message = "LIFF init succeeded.";
        console.log("hallo inspector");
      })
      .catch((e) => {
        this.message = "LIFF init failed.";
        this.error = `${e}`;
      });
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
