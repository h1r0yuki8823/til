## Vuex
Vue用の状態管理を行うライブラリ<br>

```JS
//vuexを使用するには
import Vue from 'vue'
import Vuex from 'vuex'

//VueにVuexを登録
Vue.use(Vuex)

//ストアの作成
const store = new Vuex.store({/*...*/})
```

## Vuex:ストア
状態管理に関する機能を盛り込んでいる。Vuexは信頼できるただ一つの情報源であることを前提に実装されている。なのでアプリケーションには一つのストアのみが存在するようにする。
ストアは４つの構成要素概念が存在する。<br>
<li>アプリケーションのステート (state)
<li>ステートの一部や、ステートから計算された値を返すゲッター(getter)
<li>ステートを更新するミューテーション(mutation)
<li>外部APIとのやりとりを行うアクション(action)

```JS
//storeの作成
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

//ストアの作成
const store = new Vuex.Store({
  //ステート
  state:{
    count:0
  },
  //ミューテーション
  mutations:{
    increment(state, amount){
      state.count += amount
    }
  }
})

console.log(store.state.count) //0
//ミューテーションを実行し、ステートを更新
store.commit('increment',1)
console.log(store.state.count) //1
```

## ゲッター
ゲッターはステートから別の値を算出するために用いられる。算出ロジックをストア内に置くこともできる。
```JS
/* 基本文省略 */

const store = new Vuex.store({
  state:{
    count: 10
  },
  //ゲッターを定義
  getters:{
    //ステートから別の値を計算する
    squared:(state) => state.count * state.count,
    
    //他のゲッターの値を使うことも可能
    cubes: (state, getters) => state.count * getters.squared
  }
})

console.log(store.getters.cubes) //100
```

## ミューテーション
ステートを更新するために用いられる。Vuexの規約ではミューテーション以外がステートを更新するのを禁止している。
```JS
/* 基本文省略 */

const store = new Vuex.store({
  state:{
    count: 10
  },
  
  //ミューテーションを定義
  mutations:{
    //incrementミューテーションを定義
    increment(state){
      state.count = state.count + 1
    }
  }
})

console.log(store.state.count) //10
store.commit('increment') //incrementミューテーションを呼び出す
console.log(store.state.count) //11
```
store.commitの第二引数に何らかの値を与えると、それがハンドラーの第二引数に渡される。このことをペイロードと呼ぶ
```JS
/* 基本文省略 */

const store = new Vuex.store({
  state:{
    count: 10
  },
  
  mutations:{
    //ペイロード内の'ammount'を使ってステートを更新
    increment(state, payload){
      state.count = state.count + payload.amount
    }
  }
})

console.log(store.state.count) //10
store.commit('increment',{ammount:5})
console.log(store.state.count) //15
```
注意点としてミューテーションは同期的にしなければならない

## アクション
アクションは非同期処理や外部APIとの通信を行い最終的にミューテーションを呼び出すのに用いられる<br>
直接呼び出すことはできず、store.dispatchにアクション名を与えて呼び出す
```JS
/* 基本情報省略 */
const store = new Vuex.Store({
  state:{
    count: 10
  },
  
  mutations:{
    increment(state){
      state.count = state.count + 1
    }
  },
  
  //アクションを定義する
  actions:{
    incrementAction(ctx){
      //'increment'ミューテーションを実行する
      ctx.commit('increment')
    }
  }
})

console.log(store.state.count) //10
store.dispatch('incrementAction') //'incrementAction'アクションを呼び出す
console.log(store.state.count) //11
```
 
