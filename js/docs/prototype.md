# prototype

JavaScript は__「`prototype` ベースのオブジェクト指向言語」__と言われる言語です。
どういうことかと言うと、JavaScriptには`クラス構文`が存在しません。（※`ES2015`からは実装されましたが、これはプロトタイプの糖衣構文になります）

しかし、JavaScript にはコンストラクタの働きをする組み込みオブジェクト（実態は関数）が存在し、この関数を `new` してインスタンスを生成することもできます。
この時重要になってくるのが、`prototype` というオブジェクトです。

では、詳しく見ていきましょう。