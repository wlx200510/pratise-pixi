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

function addImageToStage(img, x, y, scale = 1, rotate = Math.PI) {
  // 创建一个精灵（可以旋转 移动等）
  const sprite = new PIXI.Sprite(img)
  sprite.anchor.set(0.5, 0.5);
  sprite.x = x
  sprite.y = y
  // 设置透明度
  sprite.alpha = 0.6
  sprite.scale.set(scale)
  sprite.interactive = true
  sprite.on("pointerenter", () => {
    sprite.alpha = 1
  })
  sprite.on("pointerout", () => {
    sprite.alpha = 0.6
  })
  // 创建模糊滤镜
  const blurFilter = new PIXI.BlurFilter()
  //  将模糊滤镜添加到精灵上
  blurFilter.blur = 10
  // const outlineFilter = new PIXI.OutlineFilter(5, 0xffff00)
  sprite.filters = [blurFilter]
  app.stage.addChild(sprite)
}
const texture = PIXI.Texture.from(require("./assets/logo.png"))

addImageToStage(texture, app.screen.width / 2, app.screen.height / 2)
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
