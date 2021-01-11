# グリッドラインを使用

ソースコードをベースのもの（２行３列，余白付き，ボックス５個）を使用する．

## ▼ item1 ボックスを４番目の位置に配置

item1 ボックスを２行３列の左下に配置させたい．grid-row は２本目，grid-column は１本目なので，以下とする．

**styles.css**

```diff
.item1 {
  background: #2c3f55;
  color: #fff;

+ grid-row: 2;
+ grid-column: 1;
}
```

## ▼ item1 ボックスの横幅を伸ばす

では次に，item1 ボックスの横幅をボックス２つ分にまで伸ばしてみる．なお書き方はいくらかあるがどれでも同じ．

**styles.css**

```diff
.item1 {
  background: #2c3f55;
  color: #fff;

  grid-row: 2;
  /* 以下どの書き方でも同じ */
  grid-column: 1 / 3;
  grid-column: 1 / -2;
  grid-column: 1 / span 2;
}
```
