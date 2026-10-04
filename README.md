<a href="https://wulier-arch.github.io/axon/">
  <img src="https://wulier-arch.github.io/axon/og.png" alt="axon zero-dependency neural network framework" width="100%">
</a>

# wulier-arch

> 与其调用黑盒，不如自己写一遍。

零依赖神经网络框架 [**axon**](https://github.com/wulier-arch/axon) 的作者。

我做东西关注同一件事：**把底层原理摊开写清楚，并且证明它是对的。**

[![Live Demo](https://img.shields.io/badge/Live_Demo-7c5cff?style=for-the-badge&logo=googlechrome&logoColor=white)](https://wulier-arch.github.io/axon/)
[![Latest Release](https://img.shields.io/badge/Release-v0.3.0-4ad6c8?style=for-the-badge&logo=github&logoColor=white)](https://github.com/wulier-arch/axon/releases/tag/v0.3.0)
[![Star axon](https://img.shields.io/badge/Star_axon-ff6b6b?style=for-the-badge&logo=github&logoColor=white)](https://github.com/wulier-arch/axon)
[![npm](https://img.shields.io/badge/npm-axon--net-cb3837?style=for-the-badge&logo=npm&logoColor=white)](https://www.npmjs.com/package/axon-net)

## 在做什么

### [axon](https://github.com/wulier-arch/axon) · 零依赖神经网络框架

自动微分、张量运算、卷积、层、优化器与训练循环，全部手写。同一份代码在浏览器和 Node.js 里都能跑。

| 依赖 | 测试 | 最新版本 | `matmul` 512×512 |
| :---: | :---: | :---: | :---: |
| **0** | 95 | **v0.3.0** | 2.36 GFLOP/s |

核心主张是**梯度可验证**：每个算子都自带有限差分对照，梯度错了立刻暴露，而不是「跑起来没报错就算对」。这个机制抓到过三个静默 bug——前向传播完全正确，只有数值梯度能发现权重在错误地训练。

v0.3.0 补齐了 `LayerNorm`、`Embedding`、`MultiHeadAttention`、`TransformerBlock` 和 `GELU`。新增的梯度回归测试又抓到过一个只在 gamma 开启时出现的 LayerNorm 反向错误。

性能上坦白说比 TensorFlow.js 慢一个数量级，这是刻意的取舍：数据存在 `Float64Array` 里，但计算是标量 JS 循环，没有 WASM、没有 SIMD、没有算子融合。换来的是每一行都能读懂。**适合学习原理，不适合训 ResNet。**

[在线 Demo](https://wulier-arch.github.io/axon/demo/) · [项目主页](https://wulier-arch.github.io/axon/) · [v0.3.0 Release](https://github.com/wulier-arch/axon/releases/tag/v0.3.0) · [源码](https://github.com/wulier-arch/axon) · [npm](https://www.npmjs.com/package/axon-net)

### [rope-embedding](https://github.com/wulier-arch/rope-embedding) · 零依赖旋转位置编码

axon 有 `MultiHeadAttention` 和 `TransformerBlock`，但一直没有位置编码——这个补上缺的那块。RoPE 出自 [RoFormer](https://arxiv.org/abs/2104.09864)，现在是开源大模型的默认选择。

从数学定义手写，不引入任何张量库。内置性质自检：正交性、范数保持、相对位置不变性全部数值验证，误差触到双精度机器 epsilon。

| 依赖 | 测试 | 自检最大偏差 |
| :---: | :---: | :---: |
| **0** | 48 | 2.22e-16 |

两种配对约定（`half` / `interleaved`）都实现——**接错会静默出错**，因为两者都满足全部数学性质，只是旋转的维度对不同。

[源码](https://github.com/wulier-arch/rope-embedding)

### [awesome-shlab-opensource](https://github.com/wulier-arch/awesome-shlab-opensource) · 开源导航

上海人工智能实验室开源项目的分类索引。重点不在「有哪些项目」，而在**许可证风险标注**——同一个页面上的项目，权限差异极大。

| 标记 | 含义 |
| :---: | --- |
| 🟢 | Apache-2.0 / MIT，自由使用 |
| 🟡 | AGPL-3.0，衍生作品须同样开源 |
| 🟠 | 附加条款，如 MinerU 的商用阈值与在线署名义务 |
| 🔴 | 无许可证，默认保留所有权利，**不得转载** |
| ⛔ | 非商用许可，禁止商用与再分发 |

另附官方页面三处勘误：组织改名导致三个链接过期、把组织当成仓库、标称数量与实际不符。

[源码](https://github.com/wulier-arch/awesome-shlab-opensource)

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
