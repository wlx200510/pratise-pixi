<template>
  <div></div>
</template>

<script setup>
// 导入pixi

const app = new PIXI.Application({
  width: window.innerWidth,
  height: window.innerHeight,
  backgroundColor: 0x1099bb,
  resolution: window.devicePixelRatio || 1,
})

// 将应用画布添加到DOM中
document.body.appendChild(app.view)

// 绘制一张图片

// 通过纹理引入图片
const texture = PIXI.Texture.from(require("./assets/logo.png"))
// 创建一个精灵（可以旋转 移动等）
const sprite = new PIXI.Sprite(texture)

sprite.anchor.set(0.5, 0.5);
sprite.x = app.screen.width / 2
sprite.y = app.screen.height / 2

// 操纵精灵旋转180度
sprite.rotation = Math.PI
// 设置透明度
sprite.alpha = 0.6
app.stage.addChild(sprite)

// ticker实现动画
app.ticker.add((delta) => {
  // delta:两帧之间的间隔, 可以认为是均匀的
  sprite.rotation += 0.01 * delta
})

// 如何实现交互
// 为精灵添加点击事件
sprite.interactive = true
sprite.on("click", () => {
  sprite.rotation = 0
})
sprite.on("pointerenter", () => {
  sprite.alpha = 1
})
sprite.on("pointerout", () => {
  sprite.alpha = 0.6
})
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
canvas {
  width: 100vw;
  height: 100vh;
  position: fixed;
  left: 0;
  top: 0;
}
</style>
