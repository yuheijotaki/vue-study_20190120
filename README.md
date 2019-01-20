# Vue.js / JSON から情報を引っ張ってくる その1

Vue CLI を使って JSON から情報を引っ張る。  
とりあえず WordPress の `/wp-json/` から。

## Vue CLI の導入

[こちら](https://yuheijotaki.hatenablog.com/entry/2018/12/28/025438)とだいたい同じですが、SassとリセットCSSとaxiosを追加。

### Sass

scssを有効化

``` bash
npm install sass-loader node-sass --save-dev
```

- [VueCLIでHelloWorld \- Qiita](https://qiita.com/MariMurotani/items/5fbea5942d2edf149989)

### リセットCSS（normalize.css）

normalize.css を読み込む

``` bash
npm install -D normalize.css
```

App.vue の js に追加

```javascript
// normalize.css を読み込む
import "normalize.css";
```

- [Vueプロジェクトでnormalize\.cssを読み込む方法 \- Qiita](https://qiita.com/hogesuke_1/items/b12c65e8485289da4146)

### axios

```bash
npm install --save-dev axios
```

App.vue の js に追加

```javascript
// Ajax通信ライブラリ
import axios from "axios";
```

- [Vue\.js初心者向け：Vue\.jsとaxiosでJsonを取得してコンポーネントに反映するメモ \- Qiita](https://qiita.com/sygnas/items/7eac9491b37a1bcba0cb)
- [axios を利用した API の使用 — Vue\.js](https://jp.vuejs.org/v2/cookbook/using-axios-to-consume-apis.html)

## Vue CLI のコマンド

``` bash
# serve with hot reload at localhost:8080
# ローカルサーバー起動、コード監視
npm run dev

# build for production with minification
# ビルド（ `/dist/` へ書き出し）
npm run build
```

## WordPress の /wp-json/

知らなかったのですが、以前までパラメータ与えると投稿をフィルタして取得できたのですが、4.7から仕様が変わったようです。

> Wordpress4.7からfilterパラメーターは削除されているので、プラグインを利用してfilterパラメーターを利用できるようにする
> [WP REST API v2を利用し、カスタム投稿タイプの記事をカスタムタクソノミーでフィルタリングして取得する \- エンジニアうまの日記](http://umadash.hatenadiary.jp/entry/2019/01/09/093554)

とりあえず JSON であればなんでも良いので https://blog.yuheijotaki.com/wp-json/ から引っ張る

## App.vue

```html
<div id="app">
  <ul>
    <li>name: {{results.name}}</li>
    <li>home: {{results.home}}</li>
    <li>timezone_string: {{results.timezone_string}}</li>
  </ul>
</div>
```

```javascript
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
    // JSON取得
    axios.get(jsonUrl).then(response => {
      this.results = response.data;
    });
  }
};
```

結果

（画像）

## まとめ

[**GitHub**](https://github.com/yuheijotaki/vue-study_20190120)

- sass の導入で少しつまずく。CLIじゃないともう少し面倒な模様。
- JSONのURLが固定の場合は axios は必要ないらしいのですが、`axios.get()` 以外にJSON持ってくる方法がわからなかった。
- Instagram や Twitter APIから引っ張るつもりでしたが、Instagram => JSON の形式が難解、Twitter => APIの利用申請が難解、のために断念しました。
- Vue CLI で Router を入れてみて、ざっくりざっくりした概念は分かったような気がしました。
- 次回は投稿データをループして表示させるようにする。
