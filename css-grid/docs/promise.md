# Promise

### ▼説明

`プロミス(Promise)`とは、一言で言うと__処理の延期（deferred）や、非同期の処理を分かりやすく制御するオブジェクト__です。
分かりやすくというのは、いわゆる「可読性」のことを意味します。
まずは構文を見てみましょう。

```javascript
const promise = new Promise((resolve, reject) => {
	// resolve: 成功した時
	// reject : 失敗した時
})
```

1点注意しておかないといけないことがあります。処理の順番です。newされた時、引数の関数内の処理が先に実行され、
その後生成されたインスタンスが変数に格納されます。

また、生成されたインスタンスの`__proto__`オブジェクトを見てみると、以下のメソッド・プロパティがセットされています。

- constructor: function Promise()
- catch: function catch()
- then: function then()
- Symbol(Symbol.toStringTag): "Promise"

基本的には、この中の`then, catch`メソッドを使っていくことになります。
では具体的に例を見てみましょう。

```javascript

const promise = new Promise((resolve, reject) => {
   // 何かしらの処理
})

promise
   .then((val) => {
      // 正常時の処理
   })
   .catch((err) => {
      // エラー時の処理
   })
```

さらに、`Promise`コンストラクタのメソッドも見てみましょう。以下のメソッドの引数`tasks`は、プロミスの配列を表します。

- `Promise.all(tasks)`

tasks内のプロミスを並列に処理し、全てが成功となれば`then`を取得します。
この時の結果は全てのプロミスから得られた値の配列として渡されます。
tasks中にプロミスでないものが渡された時は、`Promise.resolve`で変換されます。
渡されたプロミスの内一つでも失敗となれば`catch`され、それ以外のプロミスは無視されます。


- `Promise.race(tasks)`

tasks内のプロミスの内、最初に完了(成功、失敗とちらでも可)したプロミスによって、成功（`then`）または失敗（`catch`）するプロミスを返します。


- `Promise.reject(reason)`

与えられた理由で失敗となる`Promise`オブジェクトを返します。


- `Promise.resolve(value)`

与えられた値で成功となる`Promise`オブジェクトを返します。
もし値が`thenable(thenメソッドを持っているオブジェクト)`ならば、返されるプロミスはその`thenable`に従い、その結果を採用します。
そうでなければ、返されるプロミスは与えられた値で成功（`then`）します。


これらも組み合わせることで、複雑な非同期処理を分かりやすく制御することが可能となります。
