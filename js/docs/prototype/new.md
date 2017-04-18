# new

## ▼説明

`prototype`の前に、JavaScriptにおける`new`の使い方に触れます。
前述の通り、JavaScriptにはクラス構文が存在しません（しかし、`class`は予約後です）が、 `new`してインスタンスを生成することができます。
実際にやってみましょう。

```JavaScript
// コンストラクタの定義
function Animal(name, age) {
	this.name = name
	this.age  = age
}

// インスタンスを生成
let cat = new Animal('kitty', 3)
console.info(cat.name) // => kitty
console.info(cat.age)  // => 3
```

上記のように、コンストラクタの名前は__頭大文字の名詞__にすることが習慣となっています。
ここで作成した`cat`というインスタンスには、現在は何もメソッドがありませので、追加してみましょう。

```JavaScript
cat.hello = function() {
	console.info('hello')
}
cat.hello() // => 'hello'
```

後はこのcatを拡張するなり何なりすれば、他のオブジェクト指向言語と同様に開発ができますが、この拡張方法には__問題があります__。

ここで新たに`dog`インスタンスを生成しましょう。

```JavaScript
var dog = new Animal('pluto', 5)
console.info(dog.name) // => pluto
console.info(dog.age)  // => 5
```

`dog`インスタンスには、先程`cat`インスタンスに追加した`hello`メソッドが存在しません。つまり、他のインスタンスを生成する度に、
そのインスタンスに別途`hello`メソッドを追加する必要があります。これは不便ですね。

では`dog`インスタンスにて`hello()`を実行できるようにするにはどうすれば良いかというと、__`Animal`コンストラクタにhelloメソッドを追加__します。

```JavaScript
Animal.prototype.hello = function() {
	console.info(this.name)
}

cat.hello() // => kitty
dog.hello() // => pluto
```

コンストラクタの`prototype`に追加すると、既に`new`して生成したインスタンスでも、この先に生成するインスタンスでも実行できるようになります。
また上記を実行するとわかりますが、`cat`インスタンスに直接`hello`メソッドが定義されている場合は、
__コンストラクタのメソッドよりインスタンスのメソッドが優先__ されますのでご注意ください。
