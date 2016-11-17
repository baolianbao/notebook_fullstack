title: Phaser.js基础 
date: 2016-01-05 21:34:06
tags: 
---

## 框架结构

## 常用

加载图片
1.普通图片
```js
game.load.image(key, url, overwrite = false);
```

示例
```js
game.load.image('sky', 'assets/sky.png');
```

1.图片组(sprite sheet)
```js
game.load.spritesheet(key, url, frameWidth, frameHeight, frameMax=-1, margin = 0 )
```
 
示例
```js
game.load.spritesheet('dude', 'assets/dude.png', 32, 48);
```
 


## 创建精灵(Sprite)

API
```js
game.add.sprite(x, y, key, frame, group)
```

示例
```js
game.add.sprite(0, 0, 'star');
```

## 资料
* [List of Phaser Tutorials](http://www.lessmilk.com/phaser-tutorial/)
* [Phaser：开源HTML5 2D游戏引擎](http://www.vqianduan.com/828.html)
