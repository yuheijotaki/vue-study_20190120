<template>
  <div id="app">
    <ul>
      <li>name: {{results.name}}</li>
      <li>home: {{results.home}}</li>
      <li>timezone_string: {{results.timezone_string}}</li>
    </ul>
  </div>
</template>

<script>
// normalize.css を読み込む
import "normalize.css";
// Ajax通信ライブラリ
import axios from "axios";
// JSON の URL
const jsonUrl = "https://blog.yuheijotaki.com/wp-json/";

export default {
  name: "App",
  data() {
    return {
      results: []
    };
  },
  mounted() {
    axios.get(jsonUrl).then(response => {
      this.results = response.data;
    });
  }
};
</script>

<style lang="scss">
body {
  color: #222;
  background: #eee;
  font-family: "游ゴシック", YuGothic, "Hiragino Kaku Gothic ProN", Meiryo,
    sans-serif;
  -webkit-text-size-adjust: 100%;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-rendering: optimizeLegibility;
  font-feature-settings: "palt";
}
#app {
  background: #fff;
  max-width: 800px;
  margin: 40px auto;
  padding: 40px;
  box-sizing: border-box;
}
</style>
