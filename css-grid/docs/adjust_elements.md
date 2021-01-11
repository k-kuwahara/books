# 要素を揃えるプロパティ

`flexbox` と同様に以下のプロパティが指定できる（意味合いも同じ）．

- 外側

  - `justify-content`
  - `align-content`

- 中身

  - `justify-items`
  - `align-items`

- 個別の中身
  - `justify-self`
  - `align-self`

わかりやすさのため，コードを以下のように変更する．

**styles.css**

```diff
.container {
  display: grid;

- grid-template-rows: 100px 100px;
- grid-template-columns: 100px 100px 100px;
+ grid-template-rows: repeat(2, 100px);
+ grid-template-columns: repeat(3, 100px);
  gap: 10px;

+ width: 400px;
+ height: 300px;
+ background: #efefef;
}

- .box {
-   display: flex;
-   align-items: center;
-   justify-content: center;
- }
```

## ▼ 全体を上下中央揃えにする

**styles.css**

```diff
  width: 400px;
  height: 300px;
  background: #efefef;

+ justify-content: center;
+ align-content: center;
}
```

## ▼ 要素を上下中央揃えにする

**styles.css**

```diff
  width: 400px;
  height: 300px;
  background: #efefef;

  justify-content: center;
  align-content: center;

+ justify-items: center;
+ align-items: center;
}
```

これだとサイズが自動で最小化してしまうので，サイズを指定する．

**styles.css**

```diff
+ .box {
+   width: 50px;
+   height: 50px;
+ }
```

## ▼ item2 ボックスのみ start 指定

**styles.css**

```diff
.item2 {
  background: #3d92a4;
  color: #fff;

+ justify-self: start;
+ align-self: start;
}
```
