# Arrow Function

ES2015から、関数は以下の用に書くことができます。

```JavaScript
// 従来の書き方
function hoge() {}
var hoge = function() {}

// ES2015の書き方
let hoge = () => {}
const hoge = () => {}
```

しかし、誰しも一度はハマると思われる事があります。[アロー関数](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/arrow_functions)の内側のコンテキストです。

例えば以下のような`button`タグに`click`イベントが付与されているといます。

```html
<button id="btn_next" type="button">next</button>
```

このとき、このコールバック関数が以下のような従来の無名関数の場合、
関数内の`this`はこの関数のコンテキスト、今回は`button`タグになります。

```JavaScript
$('#btn_next').click(function() {
	console.info(this)   // => <button id="btn_next" type="button">next</button>
})
```

しかし以下のようにアロー関数の場合、関数内の`this`は、この関数が定義されたスコープのオブジェクト、今回は`window`オブジェクトになります。
`e.currentTarget`とすると、従来の無名関数と同じコンテキストになります。

```JavaScript
$('#btn_next').click( e => {
	console.info(this)   // => window
})
```

コールバック関数については従来の無名関数を使えば回避できますが、美しくない…