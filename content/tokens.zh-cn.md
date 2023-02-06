+++
title = "代币"
description = "代币和交易对信息"
+++

## 基础知识

-   PlotBridge 简称为 PB 。
-   由 PB 发行的 BEP20 代币(如 WXCC/WXCH )简称为 WXX 。
-   区块连网络和 WXX 所对应的币简称为 XX 。

#### 问题

WXX 是在币安智能链（BSC）上由 PB 发行的代币，符合 BEP20 标准。

WXX 初始发行量为 0。

WXX 合同的源代码是公开的，可以在 BSC 区块浏览器网站上找到。

#### 地址绑定

PB 为 XX 维持着一个钱包。

XX 的储蓄地址在 PB 钱包中产生，并连同 WXX 合约存储在币安智能链中。

PB 保证在币安智能链中有足够的免费储蓄地址可进行存款地址绑定。

用户绑定储蓄地址时，会被分配到一个免费的存款地址，继而用户的 BEP20 地址与被分配到的存款地址二者间的联系就存储在币安智能链中了。

{{< mermaid >}}
graph LR;
PB(PlotBridge) --> PC[(WXCH 合约)]
{{< /mermaid >}}

通过用户输入才能获得 XX 的取款地址。当用户绑定取款地址后，BEP20 地址与取款地址二者间的联系就存储在币安智能链中了。

用户可以通过 WXX 合同将取款地址重新绑定到新的 XX 地址。

#### 铸造

PB 系统持续追踪 XX 钱包。当存款交易达到一定确认数（例如 10 个确认数）并且金额得到验证后，即可将其储存并放入铸造队列。

PB 系统持续跟踪铸造队列，根据铸造队列中的信息， 有序地铸造 WXX 代币。

{{< mermaid >}}
graph LR;
XD[XCH 存入] --> PB(PlotBridge) --> PM[WXCH 铸造]
{{< /mermaid >}}

#### 销毁

用户可以在 PB web App 内销毁 WXX 代币。

PB 系统持续追踪币安智能链。当检测到用户销毁的交易达到一定确认数后（例如 10 个确认数），它将被储存起来并被放入取款队列中。

PB 系统持续追踪提取款队列，并将 XX 代币发送回币安智能链中绑定的 XX 取款地址。

请注意，绑定取款地址后， PB 系统需要一定的时间更新 XX 取款地址。若用户想要确保取款到达新地址，请在重新绑定的一段时间（比如 10 分钟）后再进行 WXX 销毁。

{{< mermaid >}}
graph LR;
PBR[WXCH 销毁] --> PB(PlotBridge) --> XW[XCH 取款]
{{< /mermaid >}}

#### 安全原则

所有 XX 代币储蓄都被保存在 PB 系统的钱包中。

我们计划将其收集到一个单一的地址。此举也许有利于社区审计。

WXX 只在 XX 存款时铸造，取款后 XX 将被销毁。此举可有效防止 WXX 透支。

为提高安全性， App 网页服务器与 PB 系统完全隔离。二者之间仅通过 BSC 区块链进行通讯。

{{< mermaid >}}
graph LR;
App[PlotBridge App Web Server] <--> BSC([BSC Network]) <--> PB[PlotBridge App and Node]
{{< /mermaid >}}

## 现状

#### 代币发行

所有代币均在币安智能链（BSC）中发行。

| 名称                                 | 标识 | 代币标识                          | 合约地址                                   | 交易对                                                                                        |
| ------------------------------------ | :--- | --------------------------------- | ------------------------------------------ | --------------------------------------------------------------------------------------------- |
| [PBP](https://www.plotbridge.io)     | PBP  | ![PBP](/images/pbp.png)PBP        | 0x217634d01809d7B9C6348D70A95AE7f5E5179de3 | [BNB/PBP](https://pancakeswap.finance/info/pairs/0xb8d7e1982d01a613708b3235a5781a734f63d082)  |
| [Chia](https://www.chia.net)         | XCH  | ![奇亚](/images/wxch.png)WXCH     | 0xEc02B1b904a4e925F67fA8Bc6c5d428266F5C1a5 | [WXCH/PBP](https://pancakeswap.finance/info/pairs/0x10d2a3f0f7485fcee84407bbd4272918fe864a55) |
| [HDDcoin](https://www.hddcoin.org)   | HDD  | ![HDDcoin](/images/whdd.png) WHDD | 0xb558F597076babcC66250714F93A7b869Db26dB5 | [WHDD/PBP](https://pancakeswap.finance/info/pairs/0x005b461cD46E2A54e0FDF62b39f5aDf8E28dED7a) |
| [Chives](https://www.chivescoin.org) | XCC  | ![韭菜](/images/wxcc.png) WXCC    | 0x1aDCC92C322c21e387e6112bf162858AF208ff3a | [WXCC/PBP](https://pancakeswap.finance/info/pairs/0xA9d19fE91Bbb3D9F91cA313F71aA58101015014b) |
| [Flax](https://flaxnetwork.org)      | XFX  | ![Flax](/images/wxfx.png) WXFX    | 0x006294e75C3CE65910Cf6fa0EA57Dcf058dc30b0 | [WXFX/PBP](https://pancakeswap.finance/info/pairs/0x36d150548084371c8C294827433d13dC0788D3dE) |

将来我们会增加更多的代币。欢迎提出建议。
