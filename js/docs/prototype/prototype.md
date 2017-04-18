# Prototype

## ▼説明

`prototype`は一つのオブジェクトです。関数を定義すると、必ずその関数の内部に一緒に定義されます。
ではこの`prototype`ってどんなオブジェクトか、を見ていきましょう。

まずは関数hogeを定義します。

```JavaScript
// 関数の定義
function hoge() {}

// 関数hogeの中身を確認
console.dir(hoge)
```

中身はこうなっているかと思います。

```JavaScript
function hoge()
  arguments: null
  caller: null
  length: 0
  name: "hoge"
  prototype: Object   // => 定義されている
  __proto__: ()
  [[FunctionLocation]]: VM23662:1
  [[Scopes]]: Scopes[1]
```

prototypeに似たオブジェクトとして`__proto__`というオブジェクトが存在します。（上記にもいますね）
JavaScriptではオブジェクトを作ると、__裏で勝手に__`__proto__`__というプロパティが作られます__。
もちろん関数はオブジェクトですので、関数にも作られます。

※`ES2015`のアロー関数では`prototype`は生成されません。

## ▼`__proto__`オブジェクト

ここで`__proto__`を展開してみましょう。
するとたくさんのプロパティが表示されると思いますが、この子は誰でしょうか？
答えから申し上げますと、こうです。

```JavaScript
hoge.__proto__ === Funciton.prototype  // => true
```

はい。つまり、`Fuction.prototype`だったわけです。

前述したように、コンストラクタの中で1つだけ特殊な子がいます。`Object`です。
全てのコンストラクタ・関数はオブジェクトですので、`Object.prototype`を継承しています。
（正確には__「参照できる」__ですが、わかりやすさのため）

具体的に見てみましょう。

```JavaScript
// 関数hogeの表示
console.info(hoge)  // => function hoge() {}

// 整数プロパティの追加
hoge.number = 123
console.info(hoge.number)  // => 123
console.info(hoge.number.toString()) // => "123"

// 値がどのプリミティブ型かを確認
console.info(typeof hoge.number)  // => number
console.info(typeof hoge.number.toString())  // => string
```

## ▼プロトタイプチェーン
上記で登場した`toString`という関数が、`Object.prototype`オブジェクトのメソッドになります。
すべてのオブジェクトは`Object.prototype`を継承していますので、`hoge`という関数も、そのプロパティも`toString`という関数を実行できることになります。
この`Object`オブジェクトの`prototype`にアクセスできるのは、`プロトタイプチェーン`なるものが定義されているからになります。

