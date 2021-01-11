# 配置する領域を指定

より直感的に配置する領域を指定できるようにする．

先に，今回の学習のため `styles.css` の設定を以下のように４行５列に変更する．

```diff
.container {
  display: grid;

- grid-template-rows: 100px 100px;
- grid-template-columns: 100px 100px 100px;
+ grid-template-rows: repeat(4, 100px);
+ grid-template-columns: repeat(5, 100px);
  gap: 10px;
}
```

まずは各エリア領域を指定するため，`grid-template-areas` プロパティで指定する．

**styles.css**

```diff
.container {
  display: grid;

  grid-template-columns: repeat(5, 100px);
  grid-template-rows: repeat(4, 100px);
  gap: 10px;
+
+ grid-template-areas:
+   "r r r y y"
+   "r r r y y"
+   "c c g y y"
+   "c c b . b";
}
```

できましたら，それぞれの item を各領域に `grid-area` プロパティで紐付ける．

**styles.css**

```diff
.item1 {
  background: #2c3f55;
  color: #fff;
+ grid-area: r;
}

.item2 {
  background: #3d92a4;
  color: #fff;
+ grid-area: y;
}

.item3 {
  background: #f1907e;
+ grid-area: g;
}

.item4 {
  background: #9b5b19;
+ grid-area: c;
}

.item5 {
  background: #e5dcd9;
+ grid-area: b;
}
```

さらに，表示させたくない領域がある場合は，`grid-template-areas` の該当箇所を `.` で記述すると表示されなくなる．例えば以下．

**styles.css**

```diff
  grid-template-areas:
-   'r r r y y'
-   'r r r y y'
+   'r r . y y'
+   'r r . y y'
    'c c g y y'
    'c c b y y';
```

さらに，`.` を付ける位置によって四角形が崩れる場合はエラーとなり，全てのボックスが表示されないので注意．
