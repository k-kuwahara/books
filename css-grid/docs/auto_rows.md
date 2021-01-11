# はみ出した行の縦幅

[前回](./minmax_auto_fit.md) のコードをそのまま使う．

**styles.css**

```css
.container {
  display: grid;

  grid-template-rows: 100px 100px;
  grid-template-columns: repeat(auto-fit, 100px);
  gap: 10px;
}
```

３行になるまでボックスを増やしておく．

**index.html**

```diff
      <div class="box item4">item4</div>
      <div class="box item5">item5</div>
-     <div class="box item5">item6</div>
+     <div class="box item1">item1</div>
+     <div class="box item2">item2</div>
+     <div class="box item3">item3</div>
+     <div class="box item4">item4</div>
+     <div class="box item5">item5</div>
+     <div class="box item1">item1</div>
+     <div class="box item2">item2</div>
+     <div class="box item3">item3</div>
+     <div class="box item4">item4</div>
+     <div class="box item5">item5</div>
    </div>
  </body>
```

この状態で画面幅を小さくすると２行でも収まらず３行に改行されてしまうが，その際に３行目の縦幅を指定していないため，デフォルトサイズになってしまう．これを揃えるために `grid-auto-rows` を使用する．

**styles.css**

```diff
.container {
  display: grid;

  grid-template-rows: 100px 100px;
  grid-template-columns: repeat(auto-fit, 100px);
+ grid-auto-rows: 100px;
  gap: 10px;
}
```

ここの指定を `200px` とすると，はみ出した行（今回は３行目）のみが 200px となる．さらに，`grid-auto-rows` の指定のみにすれば全てのボックスの縦幅を揃えられるため，`grid-template-rows` の指定は削除する．

**styles.css**

```diff
.container {
  display: grid;

- grid-template-rows: 100px 100px;
  grid-template-columns: repeat(auto-fit, 100px);
  grid-auto-rows: 100px;
  gap: 10px;
}
```
