# 向きとサイズを変更

先に，わかりやすさのため `styles.css` の設定を以下のように４行３列に変更する．

```diff
.container {
  display: grid;

- grid-template-rows: 100px 100px;
- grid-template-columns: 100px 100px 100px;
+ grid-template-rows: repeat(4, 100px);
+ grid-template-columns: repeat(3, 100px);
  gap: 10px;
}
```

## ▼ ボックスの表示の向きを変更

今はデフォルトで左から右に（行）配置されているが，これを上から下に（列）配置されるように変更してみる．その場合は `grid-auto-flow` を指定する．

**styles.css**

```diff
.container {
  display: grid;

  grid-template-rows: repeat(4, 100px);
  grid-template-columns: repeat(3, 100px);
+ grid-auto-flow: column;
  gap: 10px;
}
```

## ▼ 要素間の穴を埋める

要素を並べていくと，サイズの指定によっては穴が空いてしまう事がある．まずはそれを再現するため，item2, 3 のボックスサイズを２ブロック分（`span 2`）にする．

**styles.css**

```diff
.item2 {
  background: #3d92a4;
  color: #fff;
+
+ grid-row: span 2;
+ grid-column: span 2;
}

.item3 {
  background: #f1907e;
+
+ grid-row: span 2;
+ grid-column: span 2;
}
```

すると，item3 ボックスがはみ出すため改列（こんな言葉はなさそう）する．このとき，item3 ボックスは div タグなので，幅が画面いっぱいに広がってしまうので，まずは`grid-auto-columns` を使って，はみ出した幅を一律 100px に固定化する．

**styles.css**

```diff
.container {
  display: grid;

  grid-template-rows: repeat(4, 100px);
  grid-template-columns: repeat(3, 100px);
  grid-auto-flow: column;
+ grid-auto-flow: 100px;
  gap: 10px;
}
```

更に item1 ボックスの右に穴が空いてしまうのと，item5 ボックスが左に寄せられていないのでここを埋める．このときは，`grid-auto-flow` に `dense` を追加する．

**styles.css**

```diff
- grid-auto-flow: column;
+ grid-auto-flow: column dense;
```

余談だが，このときに `grid-auto-flow` を `row` にしたり，このプロパティそのものを外すとそれはそれで面白く勉強になる．
