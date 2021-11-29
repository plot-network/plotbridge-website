+++
title = "代币"
description = "代币和交易对信息"
+++
## 运行机制
PXCH/PXCC等是在币安智能链（BSC）上发行的代币，符合BEP20标准，初始发行量为0。
以下内容将以PXCH代币为例进行介绍，PlotBridge简称为PB。

#### 地址绑定
XCH存款地址通过PXCH智能合约预保存在BSC上。PB系统会定期检查，确保有足够的XCH存款地址可用于绑定。绑定存款地址时，智能合约将分配一个可用的XCH地址与用户的BEP20地址进行绑定，此绑定关系保存在BCS链上。

{{< mermaid >}}
graph LR;
PB(PlotBridge) --> PC[(PXCH合约)]
{{</mermaid>}}

XCH取款地址为用户Chia钱包的收款地址，由用户自己输入，再通过PXCH智能合约将其与用户的BEP20地址绑定，此绑定关系保存在BSC上。XCH取款地址绑定后可更改。

#### 铸造
当PB系统的XCH节点检测到有效XCH存入，并达到一定确认数后，此存款动作将被PB识别，进入铸造队列。PB系统根据铸造队列中的信息，有序地在BSC上铸造新的PXCH代币。

{{< mermaid >}}
graph LR;
XD[XCH Deposit] --> PB(PlotBridge) --> PM[PXCH Mint]
{{</mermaid>}}

#### 销毁
PXCH代币由用户在PB官方App中销毁。PB系统监测BSC上信息变化，当发现用户销毁PXCH代币并达到一定确认数后，此销毁动作被PB系统记录，进入取款队列。该注意的是，XCH取款地址更改后，系统需要一定时间更新此地址。为确保提币到新地址，请等待一定确认数后再进行PXCH销毁。

{{< mermaid >}}
graph LR;
PBR[PXCH Burn] --> PB(PlotBridge) --> XW[XCH Withdraw]
{{</mermaid>}}

#### 安全性
PXCH仅当XCH存入时按量发行，取款时PXCH则被销毁，以此确保PXCH的数量不会超过PB系统钱包中的XCH数。

为了提高安全性，App网页服务器与PB系统完全隔离，两者之间仅通过BSC区块链进行通讯。

{{< mermaid >}}
graph LR;
App[PlotBridge App Web Server] <--> BSC([BSC Network]) <--> PB[PlotBridge App and Node]
{{</mermaid>}}

## 现状

###### 在 Binance 智能链（BSC）中发行的所有代币:

| 名称 | 标识 | 代币标识 | 合约地址                                                                                      | 交易对                                                                                        |
| ------ | :--- | ------------------------------------ | ------------------------------------------ | --------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| Chia   | XCH  | ![奇亚](/images/chia-logo.png)PXCH   | 0x8fCD852147d1BbA1C4f4dFf07880cCB25DD36DD7 | [PXCH/BUSD](https://pancakeswap.finance/info/pool/0xffdfb45e3d743ec10eb793fdcee3055ea82c270c) |
| Chives | XCC  | ![韭菜](/images/chives-logo.png)PXCC | 0x24D7ec172b331c7636a5Ca604de890996e5e2028 | [PXCC/BUSD](https://pancakeswap.finance/info/pool/0x62608fa59fcd378cd71ce277a50f24df333b4633) | 

在将来,我们会增加更多的代币,欢迎提出建议。
