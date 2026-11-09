# Swiper 项目 AI 关键对话记录

本文件保留每轮提示词与 AI 答复要点。答辩参考是 AI 草稿，不声称学生本人已经复述或现场操作。

## 任务一：提示词工程师

### 第一轮提示词

我在用老师提供的 Swiper 11.0.3。请给我一段 `new Swiper('#wySw4', {...})` 配置，让它循环播放、3.2 秒自动翻页，并显示可以点击的圆点分页器（`#wyPag4`）。给出最小代码及简单解释即可。

### 第一轮 AI 回答

```js
new Swiper('#wySw4', {
  loop: true,
  autoplay: { delay: 3200 },
  pagination: { el: '#wyPag4', clickable: true },
  cubeEffect: { shadow: true, slideShadows: true, shadowOffset: 20, shadowScale: 0.94 }
});
```

第一轮提示词没有明确指定 `effect: 'cube'`，也没有要求手动操作后自动播放不停，因此这段简短答案没覆盖完整清单。

### 第二轮提示词

你上次的配置漏了两个条件：初始效果必须是 cube；用户手动操作后自动播放不能停止。请重写 `new Swiper('#wySw4', {...})`：loop true；effect cube；autoplay.delay 3200 且 disableOnInteraction false；pagination.el #wyPag4 且 clickable true；speed 800。请给代码并逐项解释。

### 第二轮 AI 回答

```js
new Swiper('#wySw4', {
  loop: true,
  effect: 'cube',
  speed: 800,
  autoplay: { delay: 3200, disableOnInteraction: false },
  pagination: { el: '#wyPag4', clickable: true }
});
```

Cube 配置在 `prompt-cube-preview.html` 独立验证；综合作业页按任务四要求默认 slide。

### 第二轮技术追问与 Codex 答复

- `prev` 是活动 slide 前面的卡片变换，`next` 是下一张进入时的变换。
- `translate: [x,y,z]` 控制横、纵、深度位移；百分比相对被变换的 slide 尺寸。X 正值向右、负值向左。
- `rotate: [x,y,z]` 分别绕三轴旋转，单位为度；第三个数字改成 `20` 就是绕 Z 轴转 20 度。
- `keyboard.enabled` 开启方向键；`onlyInViewport` 限制轮播在可视区域内响应。
- `autoplay.delay` 改为 5000 后每张停留 5 秒；`speed: 800` 的切换动画时间不变。

答复由 Codex 生成。自动化检查验证了页面配置，不代表学生本人已经练习或完成答辩。

## 任务二：creative 电影墙

**提示词：** 阅读资料包中的 Swiper 11.0.3 `swiper/demo/257-effect-creative.html`，为演示四添加 creative 效果：上一张缩小左移并后退，下一张放大并从右侧进入；解释 prev、next、translate、rotate、百分比基准和如何现场修改到 Z 轴 20 度。

**答复与实现：**

```js
creativeEffect: {
  limitProgress: 2,
  perspective: true,
  prev: { shadow: true, translate: ['-24%', 0, -180], rotate: [0, 0, -20], scale: 0.82 },
  next: { shadow: true, translate: ['110%', 0, 0], rotate: [0, 0, 20], scale: 1.12 }
}
```

- `prev` 设置活动页前方 slide 的退场变换；`next` 设置后一张 slide 的进场变换。
- `translate` 是 X/Y/Z 位移；百分比相对当前 slide 的尺寸。X 负值向左、正值向右。
- `rotate` 三个值是绕 X/Y/Z 轴的角度，单位为度；第三个值改为 20 即绕 Z 轴转 20°。
- `scale` 小于 1 缩小，大于 1 放大。

## 任务三：图片与键盘控制

**图片提示词：**

> A 16:9 landscape editorial concept illustration of Adora Magic City, a Chinese-built large cruise ship. Full white ship with tiered passenger decks, dark window bands and orange lifeboats, sailing on calm blue ocean at golden sunrise. Three-quarter side view, realistic maritime scale, no text, logo or watermark. Educational AI illustration, not an official photograph.

图片输出裁切、缩放为 1600×900；页面明确标注 AI 示意图，不冒充官方实拍。首次图像服务请求没有可用通道，切换到已配置的备用图像服务后生成成功。

**键盘代码：**

```js
keyboard: { enabled: true, onlyInViewport: true }
```

- `enabled` 开启方向键控制。
- `onlyInViewport` 使轮播进入可视区域时才响应；此能力只给演示四启用，避免多个轮播一起响应。
- 把 `autoplay.delay` 改为 `5000`，每张等待时间变成约 5 秒；`speed: 800` 的切换动画不变。

## 答辩自查

- 先用自己的话说出第一轮遗漏的要求，再说第二轮如何补全。
- 现场拖动轮播、点击 creative 和 cube、按左右键。
- 将 delay 改为 5000 并解释停留时间变化；自动化浏览器截图不等于本人练习。

## 本次实际的第二轮 AI 答复

配置假设页面已加载 Swiper 11.0.3 bundle。Cube 版本为：

```js
new Swiper('#wySw4', {
  loop: true,
  effect: 'cube',
  speed: 800,
  autoplay: { delay: 3200, disableOnInteraction: false },
  pagination: { el: '#wyPag4', clickable: true }
});
```

Creative 是另一种效果，需设置 `effect: 'creative'` 并提供 `creativeEffect`。`prev`、`next` 分别设置当前 slide 前后方向 slide 的变换。`translate: [x,y,z]` 是横向、纵向、深度位移；CSS 百分比 X/Y 分量相对 slide 自身宽高，数值 Z 位移按像素。`rotate: [x,y,z]` 的第三项控制绕 Z 轴角度，设成 `20` 即旋转 20°；`scale` 小于 1 缩小，大于 1 放大。

`keyboard.enabled` 开启方向键；`onlyInViewport` 限制轮播在视口内响应。delay 从 3200 改 5000 后每张等待五秒，speed 800 的动画时长不变。`disableOnInteraction: false` 让手动操作后自动播放继续。

以上答复由本次真实的第二轮子智能体调用生成；尚未由学生本人复述。效果另由 34 项自动化检查覆盖。
