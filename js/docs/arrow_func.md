# Arrow Function

多分一度はハマると思う[アロー関数](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/arrow_functions)のスコープについて。

```JavaScript
$('#btn_next').click(function() {
    // 従来の無名関数だと、このコールバック関数内のthisはこの関数のコンテキスト
    // ex) <button id="btn_next" type="button">next</button>
})

$('#btn_next').click( e => {
    // アロー関数だと、このコールバック関数内のthisはこの関数が定義されたスコープのオブジェクト
    // ちなみにこの例だとwindowオブジェクト
    // e.currentTarget とすると、従来の無名関数と同じコンテキストになる
})
```

