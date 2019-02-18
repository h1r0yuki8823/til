# Vue基本
## v-ifとv-showの違い 
どちらも式の結果に応じて表示・非表示を切り替える。しかし実現の仕方が異なる。v-ifはDOM要素を追加、削除している。vーshowはスタイルのdisplayプロパティの値を変更している<br>
DOMの操作の方がレンダリングのコストが高くなるのでv-showを使う方がいい。式の評価結果がほとんど変わらない場合はv-ifを使う。

## v-bind 
UIの見た目を条件によって変更する場合に使用する
```
v-bind: 属性名 = "データを展開した属性値"
```
属性名にはclass、styleが存在する
## v-bind:class 
値が真のプロパティ名をクラス属性として反映する
```
 <p v-bind:class="{shark:true, mecha:false}"></p>
```
## v-bind:style
属性値のオブジェクトのプロパティがスタイルのプロパティに対応して、インラインスタイルに反映される
```
<p v-bind:style="{color:'red;'}"></p>
```
## v-for
配列あるいはオブジェクトのデータを繰り返しレンダリングできる
```
v-for="要素 in 配列"
```
v-forではv-bind：KEY＝~で一意なキーを各要素に与える事ができる
```html
<!-- data:{arr['top','mid','bot']}を定義しておく -->
<ul>
  <li v-for="item in arr" v-bind:key="item">{{item}}</li>
</ul>
<!-- レンダリング後 -->
<ul>
  <li>top</li>
  <li>mid</li>
  <li>bot</li>
</ul>
```
## v-on
v-onはイベントが起きた時に属性値の式を実行する
```
v-on イベント名="式として実行したい属性値"
```
