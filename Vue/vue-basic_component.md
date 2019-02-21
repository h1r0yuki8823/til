## コンポーネントシステム
Vue.jsに置けるコンポーネントシステムは再利用可能なVueインスタンスのこと<br>
```JS
//定義の仕方
Vue.component(tagName,options)

//使用例
Vue.Component('list-items',{
  template:'<li>foo</li>'
})
```
optionに使用できるオプションの代表例<br>
<li>data UIの状態・データ
<li>filters  データを文字列を整形する
<li>methods  イベントが発生した時の振る舞い
<li>computed  データから派生して算出する値
<li>template コンポーネントのテンプレート
<li>props 親から子へのデータの受け渡し

## コンポーネント間の通信
Vue.jsは親コンポーネントからのみ、子コンポーネントへデータを渡す事がこのとなっている。子コンポーネントから親のデータは参照できない。<br>
親から子へはpropsというオプションを使用して通信を行えるようにしている。子から親へはイベントを使用して通信を行える<br>

```JS
Vue.component(コンポーネント名,{
  props:{
    親から受け取る属性名:{
      type:StringやObjectなどのデータ型,
      default: デフォルト値,
      required:必須華道家の真偽値,
      validator:バリデーション用の関数
    }
  }
})
```

## おまけ
JSのLT大会に参加してきた
