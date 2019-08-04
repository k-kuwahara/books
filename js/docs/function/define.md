# Function

## ▼説明

JavaScriptでは、__[関数](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Functions) __ は __1つのオブジェクト__ になります。
オブジェクトですので __変数に格納__ できますし、 __プロパティを関数に追加する__ こともできますし、__別の関数の引数に渡す__ ことも、__`return` で返すこと__もできます。

### ▼関数の定義

```JavaScript
// 関数の定義
function hoge() {}

// プロパティの追加
hoge.foo = 123

// プロパティにアクセス
console.info(hoge.foo) // => 123

// 即時関数を用いて関数を定義
const hoge = (() => {
   return () => {
      return 'fuga'
   }
})()
// ※上記の関数は以下のように省略できる
const hoge = (() => () => 'fuga')()

hoge() // => "fuga"
```

JavaScriptにおいて、関数の定義には三通りあります。

```JavaScript
// 定義1: function で定義
function hoge() {}

// 定義2: 変数リファレンスで定義
const hoge = () => {}

// 定義3: Function オブジェクトのインスタンスとして定義
const hoge = new Function()
```

* すべて `hoge` という変数に無名関数をセット
* すべて `hoge()` で実行可
* 定義1のみ呼び出しが先でも動作する（後述）
* 定義3のみコンストラクタの `name` が `anonymous`

また面白いことに、関数は別の名前で定義することができます。以下のコードを見て下さい。

```JavaScript
// hogeで定義
let hoge = () => {}
console.info(hoge.name)   // => "hoge"

// fugaで定義
hoge = function fuga() {}
console.info(hoge.name)   // => "fuga"
```

### ▼関数のスコープ
さらに面白いことに、関数の定義は呼び出しより後に置くことができます。

```JavaScript
// 以下は動作する
console.log(square(5))
function square(n) {
   return n * n
}
```

関数のスコープは自身が定義された関数内、トップレベル（グローバル）で定義されたのであればプログラム全体になります。
ただし、上記の書き方は`function hoge(){}`を用いて定義した場合のみ動作しますので、以下の場合はエラーとなります。

```JavaScript
// 以下はエラーとなる
console.log(square(5))
const square = (n) => n * n
```

このように、JavaScriptの関数はオブジェクトですので、かなり自由に扱えます。逆にそれが難しくさせているのかもしれないですね…
