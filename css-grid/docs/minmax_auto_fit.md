# サイズの範囲指定と余白の均等化

[前回](./repeat.md) のコードをそのまま使う．

**styles.css**

```css
.container {
  display: grid;

  grid-template-rows: 100px 100px;
  grid-template-columns: repeat(auto-fill, 100px);
  gap: 10px;
}
```

## ▼ 右端の余白をなくす

前回までで画面幅にはみ出した場合は自動的に改行するように設定したが，右端に微妙に余白が空いてしまっているので，その場合は各ボックスの横幅を `1fr` にして幅いっぱいに埋め，ぴったり収まる場合は `100px` とするように変更．

**styles.css**

```diff
.container {
  display: grid;

  grid-template-rows: 100px 100px;
- grid-template-columns: repeat(auto-fill, 100px);
+ grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));
  gap: 10px;
}
```

この状態で画面の幅を伸縮してみると，何をやっているか分かると思う．

ただし，この状態でも６個のボックスがすべて一行に表示されても画面幅を大きくすると右端にまだ余白ができてしまうので，これを埋めたい場合は `auto-fit` を指定する．

**styles.css**

```diff
.container {
  display: grid;

  grid-template-rows: 100px 100px;
- grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));
+ grid-template-columns: repeat(auto-fit, minmax(100px, 1fr));
  gap: 10px;
}
```

こうすることで余白がある場合は常にボックス幅が `1fr` で指定されることになる．
