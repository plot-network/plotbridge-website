+++
title = "代币"
description = "代币和交易对信息"
+++

## 运行机制

WXCH/WXCC 等是在币安智能链（BSC）上发行的代币，符合 BEP20 标准，初始发行量为 0。
以下内容将以 WXCH 代币为例进行介绍，PlotBridge 简称为 PB。

#### 地址绑定

XCH 存款地址通过 WXCH 智能合约预保存在 BSC 上。PB 系统会定期检查，确保有足够的 XCH 存款地址可用于绑定。绑定存款地址时，智能合约将分配一个可用的 XCH 地址与用户的 BEP20 地址进行绑定，此绑定关系保存在 BCS 链上。

{{< mermaid >}}
graph LR;
PB(PlotBridge) --> PC[(WXCH 合约)]
{{< /mermaid >}}

XCH 取款地址为用户 Chia 钱包的收款地址，由用户自己输入，再通过 WXCH 智能合约将其与用户的 BEP20 地址绑定，此绑定关系保存在 BSC 上。XCH 取款地址绑定后可更改。

#### 铸造

当 PB 系统的 XCH 节点检测到有效 XCH 存入，并达到一定确认数后，此存款动作将被 PB 识别，进入铸造队列。PB 系统根据铸造队列中的信息，有序地在 BSC 上铸造新的 WXCH 代币。

{{< mermaid >}}
graph LR;
XD[XCH 存入] --> PB(PlotBridge) --> PM[WXCH 铸造]
{{< /mermaid >}}

#### 销毁

PXCH 代币由用户在 PB 官方 App 中销毁。PB 系统监测 BSC 上信息变化，当发现用户销毁 WXCH 代币并达到一定确认数后，此销毁动作被 PB 系统记录，进入取款队列。该注意的是，XCH 取款地址更改后，系统需要一定时间更新此地址。为确保提币到新地址，请等待一定确认数后再进行 WXCH 销毁。

{{< mermaid >}}
graph LR;
PBR[WXCH 销毁] --> PB(PlotBridge) --> XW[XCH 取款]
{{< /mermaid >}}

#### 安全性

WXCH 仅当 XCH 存入时按量发行，取款时 WXCH 则被销毁，以此确保 WXCH 的数量不会超过 PB 系统钱包中的 XCH 数。

为了提高安全性，App 网页服务器与 PB 系统完全隔离，两者之间仅通过 BSC 区块链进行通讯。

{{< mermaid >}}
graph LR;
App[PlotBridge App Web Server] <--> BSC([BSC Network]) <--> PB[PlotBridge App and Node]
{{< /mermaid >}}

## 现状

###### 在 Binance 智能链（BSC）中发行的所有代币:

| 名称                                  | 标识 | 代币标识                       | 合约地址                                   | 交易对                                                                                       |
| ------------------------------------- | :--- | ------------------------------ | ------------------------------------------ | -------------------------------------------------------------------------------------------- |
| [PBP](https://www.plotbridge.io)      | PBP  | ![PBP](/images/pbp.png)PBP     | 0x217634d01809d7B9C6348D70A95AE7f5E5179de3 | [BNB/PBP](https://pancakeswap.finance/info/pool/0xb8d7e1982d01a613708b3235a5781a734f63d082)  |
| [Chia](https://www.chia.net)          | XCH  | ![奇亚](/images/wxch.png)WXCH  | 0xEc02B1b904a4e925F67fA8Bc6c5d428266F5C1a5 | [WXCH/PBP](https://pancakeswap.finance/info/pool/0x10d2a3f0f7485fcee84407bbd4272918fe864a55) |
| [Chives](https://www.chivescoin.org/) | XCC  | ![韭菜](/images/wxcc.png) WXCC | 0x1aDCC92C322c21e387e6112bf162858AF208ff3a | [WXCC/PBP](https://pancakeswap.finance/info/pool/0xa9d19fe91bbb3d9f91ca313f71aa58101015014b) |

在将来,我们会增加更多的代币,欢迎提出建议。
