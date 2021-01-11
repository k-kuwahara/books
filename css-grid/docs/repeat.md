# 繰り返し生成

ボックスの個数が 100 個とか数が増えた場合，いちいち手で設定するのは面倒なので動的に何個配置するかを `repeat()` という関数を用いて以下のように指定できる．

**styles.css**

```diff
.container {
  display: grid;

  grid-template-rows: 100px 100px;
- grid-template-columns: 100px 100px 100px;
+ grid-template-columns: repeat(4, 100px);
  gap: 10px;
}
```

今回は４列で幅を 100px になるように指定している．

また，`100px` を `1fr` に設定すると画面幅に合うように横幅が伸びる．

**styles.css**

```diff
.container {
  display: grid;

  grid-template-rows: 100px 100px;
- grid-template-columns: repeat(4, 100px);
+ grid-template-columns: repeat(4, 1fr);
  gap: 10px;
}
```

さらに，画面幅に応じて横に並べるボックスの数を動的に変更させたい場合は `auto-fill` を指定する．ここでわかりやすさのため，ボックスを１つ追加しておく．

**index.html**

```diff
    <div class="box item4">item4</div>
    <div class="box item5">item5</div>
+   <div class="box item5">item6</div>
  </div>
```

**styles.css**

```diff
.container {
  display: grid;

  grid-template-rows: 100px 100px;
- grid-template-columns: repeat(4, 100px);
+ grid-template-columns: repeat(auto-fill, 100px);
  gap: 10px;
}
```
