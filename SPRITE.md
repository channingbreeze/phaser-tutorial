# 精灵详解

这小节详细介绍精灵，精灵可以说是整个Phaser引擎的重中之重，也是所有游戏引擎的重中之重。所以这一小节的内容大家一定要掌握。

## 基础部分

### sprite和image的区别

* 加载都是通过game.load.image

* 使用sprite是通过game.add.sprite，而使用image是通过game.add.image

* sprite可以有物理属性，image没有

案例：

[创建精灵](https://www.phaser-china.com/example-detail-484.html)

[创建图片](https://www.phaser-china.com/example-detail-485.html)

### 锚点

* 默认在左上角

* 可以通过sprite.anchor来设置，注意，sprite.anchor是一个point，要设置sprite.anchor.x 或者 sprite.anchor.y，还可以通过sprite.anchor.setTo方法来设置

* 精灵中心点，旋转中心点

[锚点案例](https://www.phaser-china.com/example-detail-487.html)

### 缩放

* 通过sprite.scale来设置，同样，sprite.scale也是一个point

* 可以实现翻转，sprite.scale.x = -1，就是水平翻转，sprite.scale.y = -1，就是垂直翻转

[缩放案例](https://www.phaser-china.com/example-detail-505.html)

### 彩显

* 通过sprite.tint来设置，可以改变精灵的颜色

[彩显案例](https://www.phaser-china.com/example-detail-509.html)

### 旋转

* 可以通过sprite.angle或者sprite.rotation来设置。

* angle和rotation的例子，注意，rotation是以弧度为单位，angle是以角度为单位。

[rotation案例](https://www.phaser-china.com/example-detail-487.html)

[angle案例](https://www.phaser-china.com/example-detail-508.html)

* sprite.pivot，可以定义旋转中心的偏移量，同样sprite.pivot是一个point

[pivot案例](https://www.phaser-china.com/example-detail-501.html)

### 销毁

* 通过sprite.destroy()销毁精灵，会把精灵从内存中清除

* sprite.kill()并不是销毁精灵，它是将精灵置为死亡状态，界面上不显示，但是内存中还有。可以通过sprite.reset()将精灵复活。

[销毁案例](https://www.phaser-china.com/example-detail-490.html)

## 高级部分

### bitmapData纹理

* 不需要图片资源，可以通过canvas的api来绘制

[bitmapData纹理案例](https://www.phaser-china.com/example-detail-507.html)

### 裁剪

* 通过sprite.crop(cropRect)

[裁剪案例](https://www.phaser-china.com/example-detail-491.html)

### 遮罩

* 通过sprite.mask来实现

* 可以用来做圆形头像

[遮罩案例](https://www.phaser-china.com/example-detail-496.html)

### 重叠检测

```
function checkOverlap(spriteA, spriteB) {
    // 获取边界
    var boundsA = spriteA.getBounds();
    var boundsB = spriteB.getBounds();
    // 检测是否相交
    return Phaser.Rectangle.intersects(boundsA, boundsB);
}

```

[重叠检测案例](https://www.phaser-china.com/example-detail-500.html)

### 子精灵

* 通过sprite.addChild(child)来添加子精灵，child只要是一个DisplayObject（可显示对象）就可以

* 子精灵的位置是相对父精灵计算的

[子精灵案例](https://www.phaser-china.com/example-detail-488.html)

拓展：[Sprite和Group用作容器的异同](http://club.phaser-china.com/topic/59b0b4f8484a53dd723f4267)

### 继承精灵

* 可以用来做一些具有特定功能的精灵类

```
// 这是一个自定义的游戏对象
MonsterBunny = function (game, x, y, rotateSpeed) {
    // 继承Phaser.Sprite
    Phaser.Sprite.call(this, game, x, y, 'bunny');
    this.rotateSpeed = rotateSpeed;
};

// 继承Phaser.Sprite的原型
MonsterBunny.prototype = Object.create(Phaser.Sprite.prototype);
MonsterBunny.prototype.constructor = MonsterBunny;

/**
 * 这个update被自动被World.update调用
 */
MonsterBunny.prototype.update = function() {
    this.angle += this.rotateSpeed;
};

// 使用
var wabbit = new MonsterBunny(game, 200, 300, 1);

```

[继承精灵案例](https://www.phaser-china.com/example-detail-492.html)

### 绳子(拓展)

* 通过game.add.rope来实现

* 我们可以给绳子创建节点

[绳子案例](https://www.phaser-china.com/example-detail-502.html)

***

精灵就为大家介绍到这里，本小节的内容和案例，大家一定要理解透彻，部分功能最好能够记住，这样能够为后面编写游戏提高不少效率。















