# wulier-arch

> 与其调用黑盒，不如自己写一遍。

零依赖神经网络框架 [**axon**](https://github.com/wulier-arch/axon) 的作者。

我做东西关注同一件事：**把底层原理摊开写清楚，并且证明它是对的。**

## 在做什么

### [axon](https://github.com/wulier-arch/axon) · 零依赖神经网络框架

自动微分、张量运算、卷积、层、优化器与训练循环，全部手写。同一份代码在浏览器和 Node.js 里都能跑。

| 依赖 | 导出 | 测试 | `matmul` 512×512 |
| :---: | :---: | :---: | :---: |
| **0** | 54 | 80 | 2.36 GFLOP/s |

核心主张是**梯度可验证**：每个算子都自带有限差分对照，梯度错了立刻暴露，而不是「跑起来没报错就算对」。这个机制抓到过三个静默 bug——前向传播完全正确，只有数值梯度能发现权重在错误地训练。

性能上坦白说比 TensorFlow.js 慢一个数量级，这是刻意的取舍：数据存在 `Float64Array` 里，但计算是标量 JS 循环，没有 WASM、没有 SIMD、没有算子融合。换来的是每一行都能读懂。**适合学习原理，不适合训 ResNet。**

[在线 Demo](https://wulier-arch.github.io/axon/demo/) · [站点](https://wulier-arch.github.io/axon/) · [npm](https://www.npmjs.com/package/axon-net)

### [interstellar-courier](https://github.com/wulier-arch/interstellar-courier) · 星际快递员

零依赖、零构建，打开浏览器就能玩的 Canvas 迷你太空躲避游戏。

[在线试玩](https://wulier-arch.github.io/interstellar-courier/)

## 技术栈

![JavaScript](https://img.shields.io/badge/JavaScript-f7df1e?logo=javascript&logoColor=black)
![Node.js](https://img.shields.io/badge/Node.js-5fa04e?logo=nodedotjs&logoColor=white)
![Canvas](https://img.shields.io/badge/Canvas-2f6feb)
![WebAudio](https://img.shields.io/badge/WebAudio-7c5cff)
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088ff?logo=githubactions&logoColor=white)

手写自动微分 · 手写卷积 · 零依赖工程习惯 · 用有限差分验证梯度

## 联系

[![Email](https://img.shields.io/badge/wulier%40foxmail.com-7c5cff?logo=maildotru&logoColor=white)](mailto:wulier@foxmail.com)

欢迎在任一仓库提 Issue 或 PR。**如果你给 axon 实现了新算子，请务必附上梯度校验用例**——这是那个项目唯一的质量底线。
