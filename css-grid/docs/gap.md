# 余白

各ボックス間に余白を付けたい場合は，以下のように `gap` プロパティをつける．もちろんこれは `fr` でも適用される．

**styles.css**

```diff
.container {
  display: grid;

  grid-template-columns: 100px 100px;
  grid-template-rows: 100px 100px 100px;
+ gap: 10px;
}
```

上下左右で違う余白にしたい場合は以下のようにプロパティの値を増やす．

**styles.css**

```diff
.container {
  display: grid;

  grid-template-columns: 100px 100px;
  grid-template-rows: 100px 100px 100px;
- gap: 10px;
+ gap: 10px 20px;
}
```
