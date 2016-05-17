# Album
[![Developing](https://img.shields.io/badge/Album-developing-yellow.svg)](https://github.com/772807886/Album)
[![GitHub license](https://img.shields.io/badge/license-AGPL-blue.svg)](https://raw.githubusercontent.com/772807886/Album/master/LICENSE)
[![GitHub stars](https://img.shields.io/github/stars/772807886/Album.svg)](https://github.com/772807886/Album/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/772807886/Album.svg)](https://github.com/772807886/Album/network)
[![GitHub issues](https://img.shields.io/github/issues/772807886/Album.svg)](https://github.com/772807886/Album/issues)

[![Chrome](https://img.shields.io/badge/Chrome-52.0%20Tested-F19A11.svg)](https://github.com/772807886/Album)
[![Firefox](https://img.shields.io/badge/Firefox-47.0%20Tested-1A6EAF.svg)](https://github.com/772807886/Album)

一个使用JS编写的相册库，使用了ES2015+CSS3

##Usage 使用方法
1. 包含album.min.css（或是未压缩版：album.css）和album.js。
```
<link rel="stylesheet" href="./css/album.min.css"/>
<script src="./js/album.js"></script>
```
2. 定义一个div容器，并指定id、宽度和高度。
```
<div id="album" style="width: 100%; height: 100%;"></div>
```
3. 使用div容器的id构造Album对象。
```
let obj = Album("album");
```
4. 调用初始化函数初始化类库，并传入初始化参数。
```
obj.setImage("", {
    layout: obj.LAYOUT.PUZZLE,
    resizeUpdate: 100
});
```
* 第一个参数为一个字符串或是字符串数组，传入一个或多个图片的地址。
* 第二个参数为一个对象，用于配置类库。

|配置项|说明|可选项|含义|默认值|
|:---:|:---:|:---:|:---:|:---:|
|layout|布局类型|Album.LAYOUT.PUZZLE<br />Album.LAYOUT.WATERFALL<br />Album.LAYOUT.BARREL|拼图布局<br />瀑布布局<br />木桶布局|Album.LAYOUT.WATERFALL|
|fullScreen|点击图片全屏|Album.FULL_SCREEN.NONE<br />Album.FULL_SCREEN.PAGE<br />Album.FULL_SCREEN.WINDOW|禁止全屏<br />页面全屏<br />全屏|Album.FULL_SCREEN.NONE|
|gutter|图片间距|{x: number, y: number}|x：横向间距<br />y：纵向间距|{x: 0, y: 0}|
|barrelHeight|木桶布局高度范围|{min: number, max: number}|min：最小高度<br />max：最大高度||
|resizeUpdate|容器大小改变监听<br />当容器大小改变时重新计算布局|Number|<=0为不监视|不监视|
|imageLoadCallback|所有图片加载完成回调函数|Function|当队列中的图片加载完成后自动调用的函数|undefined|

5. 调用```obj.addImage([]);```追加图片，函数返回追加的图片对象，可对追加的图片设置其他属性。
例如：
```
//添加1张图片
obj.addImage("./img/example.jpg").setAttribute("title", "example.jpg");
//添加多张图片
obj.addImage(["./img/example1.jpg", "./img/example2.jpg"]).forEach(function(image) {
    image.setAttribute("title", image.src);
});
```
##关于图片顺序
***注：添加多张图片时，将会把所有土建加入缓冲队列进行加载，加载完成后才会被放入布局队列中进行布局。因此，图片的顺序以加载完成时的顺序为准。***
***如需控制图片顺序，可以使用addImage函数的第二个参数回调，传入一个函数，在图片成功加载时会回调该函数。***

##PUZZLE 拼图布局
拼图布局支持1~6张图片，超过6张将只显示前6张。
