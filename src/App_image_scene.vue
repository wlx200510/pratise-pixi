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
// 添加场景1的资源, 按照场景来加载和调用
PIXI.Assets.addBundle("scene1", {
  header: require("./assets/header.jpg"),
  award: require("./assets/award.png"),
  one: require("./assets/one.jpg")
})

const texturesPromise = PIXI.Assets.loadBundle("scene1", (progress) => {
  // 可以打印出进度，做进度条效果
  console.log(progress)
})

const container = new PIXI.Container();

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
  addImageToStage(textures.one, 100, 100)
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
