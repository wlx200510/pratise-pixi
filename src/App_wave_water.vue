<template>
  <div></div>
</template>

<script setup>
// 导入pixi
import { ShockwaveFilter } from 'pixi-filters'

const app = new PIXI.Application({
  width: window.innerWidth,
  height: window.innerHeight,
  backgroundColor: 0x1099bb,
  resolution: window.devicePixelRatio || 1,
  antialias: true
})

// 将应用画布添加到DOM中
document.body.appendChild(app.view)

const texture = PIXI.Texture.from(require("./assets/a.jpg"))
const sprite = new PIXI.Sprite(texture)
sprite.width = app.screen.width
sprite.height = app.screen.height
// 创建容器
const container = new PIXI.Container()
container.addChild(sprite)
app.stage.addChild(container)

// 添加文字
const text = new PIXI.Text("Hello Car With PIXI", {
  fontFamily: "Arial",
  fontSize: Math.floor(app.screen.width * 0.1),
  fill: 0xffffff,
  align: 'center',
  dropShadow: true,
  dropShadowColor: "#000000",
  dropShadowBlur: 4,
  dropShadowAngle: Math.PI / 2,
  dropShadowDistance: 2
})
text.x = app.screen.width / 2
text.y = app.screen.height / 2
text.anchor.set(0.5)
container.addChild(text)

// 添加置换滤镜
const displacementSprite = PIXI.Sprite.from(require("./assets/displacement.jpg"))
// 越放大越不明显
displacementSprite.scale.set(0.5)
// 图像水平竖直重复填充
displacementSprite.texture.baseTexture.wrapMode = PIXI.WRAP_MODES.REPEAT
const displacementFilter = new PIXI.DisplacementFilter(displacementSprite)
// 要填充到容器上，从而文字和图片都会有效果
container.addChild(displacementSprite)

// 添加震波滤镜
const shockwaveFilter = new ShockwaveFilter([
  0.5 * app.screen.width,
  0.5 * app.screen.height
], {
  radius: 100, // 半径
  wavelength: 50, //波长
  amplitude: 10,
  speed: 200, // 扩散速度
}, 0)

container.filters = [displacementFilter, shockwaveFilter]
// 让变形动起来
app.ticker.add((delta) => {
  displacementSprite.x += 1
  displacementSprite.y += 1
  createWave(shockwaveFilter, 1)
})
// 核心函数，好好研究下
function createWave(waveFilter, resetTime) {
  waveFilter.time += 0.01;
  if (waveFilter.time > resetTime) {
    waveFilter.time = 0;
    waveFilter.center = [
      Math.random() * app.screen.width,
      Math.random() * app.screen.height,
    ];
  }
}
// 问题：如何实现点击出现波纹，目前是中心出现了波纹
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
