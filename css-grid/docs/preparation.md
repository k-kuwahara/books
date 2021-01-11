# 準備

ここでは学ぶに当たってのベースとなる HTML, CSS ファイルを作成．基本的にはこの２つのファイルを操作するが，主に触るのは `styles.css` のみ．

**index.html**

```html
<!DOCTYPE html>
<html lang="ja">
  <head>
    <meta charset="utf-8" />
    <title>CSS Grid</title>
    <link rel="stylesheet" href="styles.css" />
  </head>
  <body>
    <div class="container">
      <div class="item1">item1</div>
      <div class="item2">item2</div>
      <div class="item3">item3</div>
      <div class="item4">item4</div>
      <div class="item5">item5</div>
    </div>
  </body>
</html>
```

**styles.css**

```css
body {
  margin: 0;
  padding: 0;
}

.container {
  display: grid;
}

.item1 {
  background: #2c3f55;
  color: #fff;
}

.item2 {
  background: #3d92a4;
}

.item3 {
  background: #f1907e;
}

.item4 {
  background: #9b5b19;
}

.item5 {
  background: #e5dcd9;
}
```
