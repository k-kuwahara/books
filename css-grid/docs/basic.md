# 基本

## ▼ ２行３列のグリッドレイアウトを作成

グリッドレイアウトのキホンのキということで，２行３列のレイアウトを作成する．

**styles.css**

```diff
.container {
  display: grid;

+ grid-template-rows: 100px 100px;
+ grid-template-columns: 100px 100px 100px;
}
```

上記のように `columns, rows` で行と列の数を指定する．**次回以降のページも，ベースはこの指定とする．**

逆に３行２列にする場合は以下となる．

```diff
.container {
  display: grid;

- grid-template-rows: 100px 100px;
- grid-template-columns: 100px 100px 100px;
+ grid-template-rows: 100px 100px 100px;
+ grid-template-columns: 100px 100px;
}
```

## ▼ 余白を埋める

横幅が広い画面だと，右端に余白ができてしまう．ここを余白がある分だけ引き伸ばしたい場合は `fr` という単位で指定する．試しに一列目のボックスを伸ばしてみる．

**styles.css**

```diff
.container {
  display: grid;

+ grid-template-rows: 100px 100px;
+ grid-template-columns: 1fr　100px 100px;
}
```

また `fr` は複数個着けることができる．以下の場合は，２列目は 100px 固定で，１・３列目は 2:1 の割合で引き伸ばされる．

**styles.css**

```diff
.container {
  display: grid;

  grid-template-rows: 100px 100px;
- grid-template-columns: 1fr　100px 100px;
+ grid-template-columns: 2fr　100px 1fr;
}
```
