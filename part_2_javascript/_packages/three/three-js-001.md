title: three.js 学习(一)
date: 2015-12-16 09:49:34
tags: [three.js,webgl]
---

![handlebars.js](https://raw.githubusercontent.com/hexcola/blog/master/source/_images/web/threejs/01/01.png)
<!--more-->

> Still working on it.

# 什么是three.js
简单来说：
Three.js是一个可以让在浏览器中实现3D效果的WebGL更加简单易用的库。用纯粹的WebGL绘制一个简单的Cube可能需要上百行JavaScript代码及Shader，但通过Three.js就可以非常简单的实现。

# 浏览器兼容性检测
* [WebGL - 3D Canvas graphics](http://caniuse.com/#search=webgl)
* [Browser Check](http://www.x3dom.org/check/)

# 将three.js添加到项目中去
## CDN
```js
// From CDN
<script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r73/three.min.js" ></script>
```

## 下载文件
直接到three.js官网[下载文件](http://threejs.org/build/three.min.js), 添加到自己项目中去。

```js
// From local
<script src="js/three.min.js"></script>

```

# 创建场景
要使用Three.js显示任何对象，需要三样东西：
* 场景(scene)
* 相机(camera)
* 渲染器(render)

```js
var scene = new THREE.Scene();
var camera = new THREE.PerspectiveCamera( 75, window.innerWidth / window.innerHeight, 0.1, 1000 ); var renderer = new THREE.WebGLRenderer();
renderer.setSize( window.innerWidth, window.innerHeight );
document.body.appendChild( renderer.domElement );
```

# 添加Box对象
```js
var geometry = new THREE.BoxGeometry( 1, 1, 1 );
var material = new THREE.MeshBasicMaterial( { color: 0x00ff00 } );
var cube = new THREE.Mesh( geometry, material );
scene.add( cube );

camera.position.z = 5;

```

# 渲染场景
```js
function render() {
	requestAnimationFrame( render );
	renderer.render( scene, camera );
}
render();
```

# Cube动画
```js
function render() {
	requestAnimationFrame( render );
  cube.rotation.x += 0.1;
  cube.rotation.y += 0.1;
	renderer.render( scene, camera );
}
render();
```


查看完整代码：[GitHub]()

# 参考
* [Introduction](http://threejs.org/docs/index.html#Manual/Introduction/Creating_a_scene)
* [three.js wiki](https://github.com/mrdoob/three.js/wiki)
* [How to run things locally](https://github.com/mrdoob/three.js/wiki/How-to-run-things-locally)
* [The Beginner’s Guide to three.js](http://blog.teamtreehouse.com/the-beginners-guide-to-three-js)
* [20 Impressive Examples for Learning WebGL with Three.js](http://tutorialzine.com/2013/09/20-impressive-examples-for-learning-webgl-with-three-js/)
