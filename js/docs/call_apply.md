# call, apply method

### ▼説明

`call, apply`メソッドは、知ってると役に立つ素晴らしい奴らです。

どんな奴らかというと、あるオブジェクトが、本来使えないはずのメソッドを実行できるようになります。
（イメージは、戦士が覚えてもいない黒魔法を使う感じです）

```JavaScript
const main_obj = {
   name: 'main !!',
   echo: function() {
      console.info(this.name)
   }
}

const sub_obj = {
   name: 'sub !!'
}

main_obj.echo()  // => 'main !!'
sub_obj.echo()  // => エラー
main_obj.echo.call(sub_obj) // => 'sub !!'
```

上記のコードでは、`sub_obj`は`echo`というメソッドが定義されていないため使えないですが、
callメソッドを使うことで`main_obj`の`echo`メソッドを実行できるようになります。

※callメソッドによる実行時のコンテキスト（this）は、callのカッコ内のオブジェクトになることに注意しましょう。


### ▼callとapplyの違い

最後に、`call, apply`の違いはというと、以下です。

- call => 引数を一つずつカンマ区切りで指定
- apply => 引数をオブジェクトや配列にまとめて指定