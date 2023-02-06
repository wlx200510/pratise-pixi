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
// 多图片资源的管理
// 异步添加资源，并批量添加 
PIXI.Assets.add("vue", require("./assets/logo.png"))
PIXI.Assets.add("header", require("./assets/header.jpg"))
PIXI.Assets.add("award", require("./assets/award.png"))

const container = new PIXI.Container();
const texturesPromise = PIXI.Assets.load(["vue", "header", "award"], (progress) => progress)

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
  container.addChild(sprite)
}

texturesPromise.then((textures) => {
  addImageToStage(textures.vue, 100, 100)
  addImageToStage(textures.header, app.screen.width / 2, app.screen.height / 2, 0.1)
  addImageToStage(textures.award, 800, 100)
})

app.stage.addChild(container)
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
