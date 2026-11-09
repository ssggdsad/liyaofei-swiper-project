# Swiper 学习笔记（不是聊天记录）

真实用户提示词与 Codex 回复请看 [prompt.md](prompt.md)，网页入口为 [prompts.html](prompts.html)。本文件是实现说明，不把下面的内容称为用户的真实提问或已经完成的答辩。

## Cube 配置

```js
new Swiper('#wySw4', {
  loop: true,
  effect: 'cube',
  speed: 800,
  autoplay: { delay: 3200, disableOnInteraction: false },
  pagination: { el: '#wyPag4', clickable: true }
});
```

综合页任务四默认 slide；Cube 配置在独立页面验证。这是老师两处要求分别对应的演示。

## creative 配置与含义

```js
creativeEffect: {
  limitProgress: 2,
  perspective: true,
  prev: { shadow: true, translate: ['-24%', 0, -180], scale: 0.82, rotate: [0, 0, -20] },
  next: { shadow: true, translate: ['110%', 0, 0], scale: 1.12, rotate: [0, 0, 20] }
}
```

prev 控制前一张，next 控制后一张，变换随进度插值。translate 的 X/Y 百分比相对 slide 宽/高，Z 数字按像素；rotate 第三项为 Z 轴角度。将其改为 20 表示绕 Z 轴旋转 20 度。

## 键盘和等待时间

keyboard.enabled 开启左右方向键，onlyInViewport 限制可见时响应。autoplay.delay 为换页等待时间，speed 为过渡时间；把 3200 改为 5000 表示等待 5 秒，speed 800 不变。手动操作后继续播放由 disableOnInteraction:false 控制。

## 邮轮素材

1600×900 的横版 AI 生成示意图（16:9），页面已标注非官方实拍。生成素材属于前一阶段产物；本轮没有重新生成图片。

## 学生自己需要完成的事项

针对 Cube 配置的两轮技术提示词应由学生实际提出并保留回答；不以 AI 内部练习代替。现场解释参数、修改 delay 和答辩需学生本人完成。
