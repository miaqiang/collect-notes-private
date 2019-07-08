### 强制英文换行
```
word-break: break-all;
word-wrap: break-word
```

### 显示一行，超过长度显示省略号

```
overflow: hidden;
text-overflow: ellipsis;
white-space: nowrap;
```

### 显示三角符号

方向向右

```
border-top: 8px solid transparent;
border-left: 10px solid rgb(255, 255, 255);
border-bottom: 8px solid transparent;
```

### 图片显示
```
background-size: cover;//把背景图像扩展至足够大，以使背景图像完全覆盖背景区域

background-size: contain;//把图像图像扩展至最大尺寸，以使其宽度和高度完全适应内容区域。

border-image: url(./src/imgs/changan/borderImg2.png) 25 fill / 1 / 0 stretch;

```