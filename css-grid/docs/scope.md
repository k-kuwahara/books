# Scope

### ▼説明

JavaScriptのスコープは、`グローバルスコープ`と`ブロックスコープ`の２つに分けられます。
以下のコードを見てください。

```JavaScript
// グローバルの変数
let hoge = 'hoge',
    fuga = 'fuga'

// ブロックスコープ用の関数
const show_hoge = () => {
   let hoge = 999
   console.info(hoge)   // ここにはthisは不要
}

console.info(hoge)  // => 'hoge'
show_hoge() // => 999

// グローバル変数の変更
const change_hoge = () => {
   hoge = 111
   console.info(hoge)   // ここもthisは不要
}

console.info(hoge)  // => 'hoge'
change_hoge()   // => 111
console.info(hoge)  // => 111 書き換わる！


// ブロックスコープ用のオブジェクト
const obj = {
   foo: 'foo',
   fuga: 123,
   show_inner_fuga: function() {
       console.info(this.fuga)  // ここにはthisが必要
   },
   show_outer_fuga: function() {
      console.info(fuga)
   }
}


console.info(fuga)  // => 'fuga'
console.info(obj.fuga)  // => 123

console.info(foo) // => エラー
obj.show_inner_fuga() // => 123
obj.show_outer_fuga() // => 'fuga'
```

変数の頭に`let, const（ES5なら var）`を付けないと、JavaScriptはその変数をグローバルの変数とみなしますので、注意して下さい。