# 第一个游戏

本小节，我们动手来实现我们的第一个游戏，这个游戏也是Phaser官方提供的入门案例。

我们可以从[这里](https://www.phaser-china.com/inter/download/downloadFile.php?file=example)下载完整案例的素材及源码。接下来，我们还是展示一下实际项目过程中的步骤。

* 第一步，创建一个项目目录。

* 第二步，在项目目录中创建一个assets文件夹，用于存放资源。将案例中的资源拷贝过来。

* 第三步，在项目目录中创建一个index.html文件。

* 第四步，编写index.html的代码。

* 第五步，在项目目录下运行http-server，然后在浏览器打开 http://127.0.0.1:8080 ，查看我们的项目运行效果。

## 源码解析

了解了创建项目的步骤之后，最重要的就是第四步的代码是怎么编写的了，下面我们来详细解析一下，整个文件的代码如下：

```
<!DOCTYPE html>
<head>
    <meta charset="UTF-8" />
    <title>exam8</title>
    <script src="../phaser.min.js"></script>
</head>
<body>
 
<script>
 
var game = new Phaser.Game(800, 600, Phaser.AUTO, '', { preload: preload, create: create, update: update });
 
function preload() {
    game.load.image('sky', 'assets/sky.png');
    game.load.image('ground', 'assets/platform.png');
    game.load.image('star', 'assets/star.png');
    game.load.spritesheet('dude', 'assets/dude.png', 32, 48);
}
 
var platforms;
var player;
var cursors;
var stars;
var score = 0;
var scoreText;

function create() {
    game.physics.startSystem(Phaser.Physics.ARCADE);
    game.add.sprite(0, 0, 'sky');
    platforms = game.add.group();
    platforms.enableBody = true;
    var ground = platforms.create(0, game.world.height - 64, 'ground');
    ground.scale.setTo(2, 2);
    ground.body.immovable = true;
    var ledge = platforms.create(400, 400, 'ground');
    ledge.body.immovable = true;
    ledge = platforms.create(-150, 250, 'ground');
    ledge.body.immovable = true;
   
    player = game.add.sprite(32, game.world.height - 150, 'dude');
    game.physics.arcade.enable(player);
    player.body.bounce.y = 0.2;
    player.body.gravity.y = 300;
    player.body.collideWorldBounds = true;
    player.animations.add('left', [0, 1, 2, 3], 10, true);
    player.animations.add('right', [5, 6, 7, 8], 10, true);
   
    cursors = game.input.keyboard.createCursorKeys();
   
    stars = game.add.group();
    stars.enableBody = true;
    for (var i = 0; i < 12; i++) {
        var star = stars.create(i * 70, 0, 'star');
        star.body.gravity.y = 300;
        star.body.bounce.y = 0.7 + Math.random() * 0.2;
    }
   
    scoreText = game.add.text(16, 16, 'score: 0', { fontSize: '32px', fill: '#000' });
}
 
function update() {
    game.physics.arcade.collide(player, platforms);
   
    game.physics.arcade.collide(stars, platforms);
    game.physics.arcade.overlap(player, stars, collectStar, null, this);
   
    player.body.velocity.x = 0;
    if (cursors.left.isDown) {
        player.body.velocity.x = -150;
        player.animations.play('left');
    } else if (cursors.right.isDown) {
        player.body.velocity.x = 150;
        player.animations.play('right');
    } else {
        player.animations.stop();
        player.frame = 4;
    }
    
    if (cursors.up.isDown && player.body.touching.down) {
        player.body.velocity.y = -350;
    }
}
 
function collectStar (player, star) {
    star.kill();
   
    score += 10;
    scoreText.text = 'Score: ' + score;
}
 
</script>
 
</body>

```

接下来我们对其中的重点部分进行讲解：

* ``` <script src="../phaser.min.js"></script> ``` ，这一行引入phaser库。

* ``` var game = new Phaser.Game ``` ，这一行创建了一个Game对象，指定了游戏区域宽高，渲染模式，并且指定了初始场景。

* preload 函数中进行了资源的加载，create 函数进行了场景的初始化，update 函数是游戏循环。注意，preload、create、update 都是由框架调用，我们不需要手动调用它，只需要定义就行。

* ``` game.physics.startSystem(Phaser.Physics.ARCADE); ``` ，这一行打开了ARCADE物理系统。

* update 中通过 ``` game.physics.arcade.collide ``` 和 ``` game.physics.arcade.overlap ``` 进行了碰撞检测。

其余的代码基本就是一看就懂的，这就是Phaser的强大之处，用它写出来的代码，就像白话文一样好懂。

更加详细的教程，一步一步教你这个项目的代码是怎么写出来的，请看[这里](https://www.phaser-china.com/tutorial-detail-1.html)。

***

这是我们的第一个游戏，不管你是否能够弄懂代码的含义，都希望你能够按照上面的1到5步，把项目搭建出来，运行起来。完成这个工作，我们向Phaser游戏开发者又迈进了一步。

