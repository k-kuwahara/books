# Arrow Function

ES2015から、関数は以下の用に書くことができます。

```JavaScript
function hoge() {}
var hoge = function() {}

let hoge = () => {}
const hoge = () => {}
```

しかし、誰しも一度はハマると思われる事があります。[アロー関数](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/arrow_functions)の内側のコンテキストです。

例えば以下のような`button`タグがあったとして、

```html
<button id="btn_next" type="button">next</button>
```

以下のような従来の無名関数ですと、このコールバック関数内の`this`はこの関数のコンテキスト、今回は`button`タグになります。

```JavaScript
$('#btn_next').click(function() {})
```

しかしアロー関数ですと、以下のコールバック関数内の`this`は、この関数が定義されたスコープのオブジェクト、今回は`window`オブジェクトになります。
`e.currentTarget`とすると、従来の無名関数と同じコンテキストになります。

```JavaScript
$('#btn_next').click( e => {})
```

コールバック関数については従来の無名関数を使えば回避できますが、美しくない…