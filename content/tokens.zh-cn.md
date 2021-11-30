+++
title = "代币"
description = "代币和交易对信息"
+++

## 运行机制

PXCH/PXCC 等是在币安智能链（BSC）上发行的代币，符合 BEP20 标准，初始发行量为 0。
以下内容将以 PXCH 代币为例进行介绍，PlotBridge 简称为 PB。

#### 地址绑定

XCH 存款地址通过 PXCH 智能合约预保存在 BSC 上。PB 系统会定期检查，确保有足够的 XCH 存款地址可用于绑定。绑定存款地址时，智能合约将分配一个可用的 XCH 地址与用户的 BEP20 地址进行绑定，此绑定关系保存在 BCS 链上。

{{< mermaid >}}
graph LR;
PB(PlotBridge) --> PC[(PXCH 合约)]
{{</mermaid>}}

XCH 取款地址为用户 Chia 钱包的收款地址，由用户自己输入，再通过 PXCH 智能合约将其与用户的 BEP20 地址绑定，此绑定关系保存在 BSC 上。XCH 取款地址绑定后可更改。

#### 铸造

当 PB 系统的 XCH 节点检测到有效 XCH 存入，并达到一定确认数后，此存款动作将被 PB 识别，进入铸造队列。PB 系统根据铸造队列中的信息，有序地在 BSC 上铸造新的 PXCH 代币。

{{< mermaid >}}
graph LR;
XD[XCH 存入] --> PB(PlotBridge) --> PM[PXCH 铸造]
{{</mermaid>}}

#### 销毁

PXCH 代币由用户在 PB 官方 App 中销毁。PB 系统监测 BSC 上信息变化，当发现用户销毁 PXCH 代币并达到一定确认数后，此销毁动作被 PB 系统记录，进入取款队列。该注意的是，XCH 取款地址更改后，系统需要一定时间更新此地址。为确保提币到新地址，请等待一定确认数后再进行 PXCH 销毁。

{{< mermaid >}}
graph LR;
PBR[PXCH 销毁] --> PB(PlotBridge) --> XW[XCH 取款]
{{</mermaid>}}

#### 安全性

PXCH 仅当 XCH 存入时按量发行，取款时 PXCH 则被销毁，以此确保 PXCH 的数量不会超过 PB 系统钱包中的 XCH 数。

为了提高安全性，App 网页服务器与 PB 系统完全隔离，两者之间仅通过 BSC 区块链进行通讯。

{{< mermaid >}}
graph LR;
App[PlotBridge App Web Server] <--> BSC([BSC Network]) <--> PB[PlotBridge App and Node]
{{</mermaid>}}

## 现状

###### 在 Binance 智能链（BSC）中发行的所有代币:

| 名称   | 标识 | 代币标识                              | 合约地址                                   | 交易对                                                                                        |
| ------ | :--- | ------------------------------------- | ------------------------------------------ | --------------------------------------------------------------------------------------------- |
| Chia   | XCH  | ![奇亚](/images/chia-logo.png)PXCH    | 0x8fCD852147d1BbA1C4f4dFf07880cCB25DD36DD7 | [PXCH/BUSD](https://pancakeswap.finance/info/pool/0xffdfb45e3d743ec10eb793fdcee3055ea82c270c) |
| Chives | XCC  | ![韭菜](/images/chives-logo.png) PXCC | 0x24D7ec172b331c7636a5Ca604de890996e5e2028 | [PXCC/BUSD](https://pancakeswap.finance/info/pool/0x62608fa59fcd378cd71ce277a50f24df333b4633) |

在将来,我们会增加更多的代币,欢迎提出建议。
