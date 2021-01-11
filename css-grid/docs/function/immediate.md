# 即時関数

## ▼説明
関数を定義したその場で実行する関数です。実行後は捨てられます。

```js
// 要はこんな子です
(() => {
    // 何かしらの処理
})()

// function で定義する場合は、()を中に入れる書き方もあります
// ※ES6 のアロー関数ではエラーになります
(function() {
    // 何かしらの処理
}())
```

具体的な使い方は色々あるんですが、主には以下かなーと。

### 名前を強制させる

```js
// 例えばグローバルの（windowオブジェクトの）$が
// jQueryと他のライブラリでバッティングすることを避けられる
(($) => {
    // ここでの$はjQueryを指す
    $('#target').on('click', () => {
        // 何らかの処理
    })
})(jQuery)
```

### プライベートな変数、オブジェクトを生成

```js
// 外からは変数 _hoge と _count にはアクセスできない
(() => {
    const _hoge  = 'hoge'
    let _count = 0

    document.addEventListener('click', () => {
        console.info(++_count);
    }, false)
})()

// 上記をjQueryを利用して書くとこうなる
$(() => {
    const _hoge  = 'hoge'
    let _count = 0

    $(document).on('click', () => {
        console.info(++_count)
    })
})
```

### インスタンスを生成

```js
// パターン1
// いわゆるシングルトンパターン
const app = (() => {
   const _hoge,
         _fuga

   const foo = () => {
      // 〜
   }
   const bar = () => {
      // 〜
   }
   $('#hoge').click(() => {
      alert('hoge')
   })

   return {
      hoge: this._hoge
      fuga: this._fuga
      aaa: (val) => {
         // 〜
      },
      bbb: (val) => {
         // 〜
      }
   }
})()

// パターン2
const classHoge = (() => {
   const classHoge = (a, b) => {
      this.hoge = a
      this.fuga = b
      this.init()
   }
   classHoge.prototype = {
      init: () => {
         this.buttonBack(),
         this.buttonNext()
      },
      buttonBack: () => {
         $('#btn-back').on('click', () => {
            alert('back')
         })
      },
      buttonNext: function() {
         $('#btn-next').on('click', () => {
            alert('next')
         })
      }
   }
   return classHoge
})()
// htmlのscriptタグで
const hoge = new classHoge('hoge', 123)
```

### ブラウザ判定

```js
// デバイス判定にも利用可
const browser = (() => {
    // もちろんこの子は外からはアクセスできない
   const _ua = navigator.userAgent

   if (_ua.indexOf('Edge') > 0) return 'Edge'
   else if (_ua.indexOf('Chrome')  > 0) return 'Google Chrome'
   else if (_ua.indexOf('Safari')  > 0) return 'Safari'
   else if (_ua.indexOf('Firefox') > 0) return 'Firefox'
   else if (_ua.indexOf('.NET')    > 0) return 'Internet Explorer'
})()
```
