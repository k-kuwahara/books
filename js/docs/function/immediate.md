# 即時関数

## ▼説明
関数を定義したその場で実行する関数です。実行後は捨てられます。

```
// 要はこんな子です
(function() {
    //何かしらの処理
})()

// ()を中に入れる書き方もあります
(function() {
    // 何かしらの処理
}())
```

具体的な使い方は色々あるんですが、主には以下かなーと。

1. 名前を強制させる
2. プライベートな変数、オブジェクトを生成
3. ブラウザ判定

```JavaScript
// 1.名前を強制させる
// 例えばグローバルの（windowオブジェクトの）$が
// jQueryと他のライブラリでバッティングすることを避けられる
(function($) {
    // ここでの$はjQueryを指す
    $('#target').on('click', function() {
        // 何らかの処理
    })
})(jQuery)

// 2. プライベートな変数、オブジェクトを生成
// 外からは変数 hoge と count にはアクセスできない
(function() {
    var hoge  = 'hoge'
    var count = 0

    document.addEventListener('click', function() {
        console.info(++count);
    }, false)
})()

// 上記をjQueryを利用して書くとこうなる
$(function() {
    var hoge  = 'hoge'
    var count = 0

    $(document).on('click', function() {
        console.info(++count)
    })
})

// 3. ブラウザ判定
// デバイス判定にも利用可
var browser = (function() {
    // もちろんこの子は外からはアクセスできない
   var _ua = navigator.userAgent

   if (_ua.indexOf('Edge') > 0) return 'Edge'
   else if (_ua.indexOf('Chrome')  > 0) return 'Google Chrome'
   else if (_ua.indexOf('Safari')  > 0) return 'Safari'
   else if (_ua.indexOf('Firefox') > 0) return 'Firefox'
   else if (_ua.indexOf('.NET')    > 0) return 'Internet Explorer'
})()
```
