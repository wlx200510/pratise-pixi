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

// 添加文字，显示 hello world
const text = new PIXI.Text("Hello World", {
  fontFamily: 'Arial',
  fontSize: 80,
  fill: "#cccccc",
  align: "center"
})

text.x = app.screen.width / 2;
text.y = app.screen.height / 2;

text.anchor.set(0.5, 0.5)
app.stage.addChild(text)

const bunny = PIXI.Sprite.from(require("./assets/logo.png"))
bunny.x = app.screen.width / 2
bunny.y = app.screen.height / 2
bunny.anchor.set(0.5)
bunny.scale.set(5)
// 文字作为遮罩
bunny.mask = text
app.stage.addChild(bunny)
// 图片也可以作为遮罩，只显示某个轮廓下的部分
const container = new PIXI.Container();

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
