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
    <div class="form">
      <div class="control">
        <!-- <input class="input" type="text" placeholder="お名前" v-model="formData.name"> -->
      </div>
      <!-- <button class="button is-info is-fullwidth" @click="onSubmit()">送信する</button>
      <button class="button is-light is-fullwidth" @click="handleCancel()">キャンセル</button> -->
    </div>
    <div id="example-1">
      <button v-on:click="counter += 1">Add 1</button>
      <p>The button above has been clicked {{ counter }} times.</p>
    </div>
    <button v-on:click="greet">クリック</button>
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
      error: "",
      counter: 0
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
        console.log("hello inspector");
      })
      .catch((e) => {
        this.message = "LIFF init failed.";
        this.error = `${e}`;
      });
  },
  methods: {
    greet(event) {
      // メソッド内の `this` は、 Vue インスタンスを参照します
      alert('Hello!')
      console.log("Hello");
      // `event` は、ネイティブ DOM イベントです
      // if (event) {
      //   alert(event.target.tagName)
      // }
    }
    // openLoading(text) {
    //   if (!text) {
    //     this.loading = 'Loading'
    //   } else {
    //     this.loading = text
    //   }
    // },
    // closeLoading() {
    //   this.loading = null
    // },
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
  margin-top: 60px;
}
</style>
