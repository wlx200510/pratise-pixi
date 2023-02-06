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

const rectangle = new PIXI.Graphics() // 获取图形对象

rectangle.lineStyle(4, 0xff0000, 1) // 线宽 颜色 透明度
rectangle.beginFill(0x66ffff, 0.9) // 指定绘制颜色
rectangle.drawRect(0, 0, 300, 300) // 绘制矩形
rectangle.endFill() // 结束填充

// rectangle.scale.set(2, 2) // 放大缩小
rectangle.position.set(400, 400) // 移动位置
// 图形的锚点 旋转基点
rectangle.pivot.set(150, 150)
// 图形的旋转
rectangle.rotation = 0.7

const circle = new PIXI.Graphics()
circle.lineStyle(6, 0xff0000, 0.5) // 线宽 颜色 透明度
circle.beginFill(0x66ccff, 0.9)
circle.drawCircle(100, 100, 64)
circle.endFill()

const roundRect = new PIXI.Graphics()
roundRect.beginFill(0xcc0000, 0.8)
roundRect.drawRoundedRect(0, 0, 100, 200, 10) // 最后参数是圆角半径
roundRect.endFill()
roundRect.position.set(600, 100)

// 绘制多边形
const polygon = new PIXI.Graphics()
polygon.beginFill(0x66cc00, 0.9)
polygon.drawPolygon([0, 0, 100, 0, 100, 100, 0, 100])
polygon.endFill();
polygon.position.set(600, 400)

// 绘制圆弧，用arc(0, 0, 32, 0, MATH.PI, false) 结束角度 逆时针

//绘制线段，可以设置lineStyle后，用 moveTo起手，各种lineTo绘制出折线

app.stage.addChild(rectangle)
app.stage.addChild(circle)
app.stage.addChild(roundRect)
app.stage.addChild(polygon)
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
