+++
title = "Tokens"
description = "Tokens and Trading Pairs"
+++

## The Basics

-   PlotBridge will be called PB for short.
-   BEP20 Tokens issued by PB(such as WXCC/WXCH) will be called WXX for short.
-   Blockchain networks and coins corresponding to WXX will be called XX for short.

#### Issue

WXX is the BEP20 token issued by PB on Binance Smart Chain (BSC).
The initial mint amount for WXX is 0.
Source code for WXX contracts are open and can be found in BSC block explorer website.

#### Address Binding

PB maintains a wallet for XX.
The deposit addresses of XX are generated in the PB wallet, and stored in BSC chain with WXX contract.
PB keeps there are enough free deposit addresses available in BSC chain for deposit address binding.
When user bind deposit address, a free deposit address will be allocated, and the relationship between BEP20 address of user and the allocated deposit address are then stored in BSC chain.

{{< mermaid >}}
graph LR;
PB(PlotBridge) --> PC[(WXCH)]
{{< /mermaid >}}

Withdraw address of XX are always obtained from user input. When user bind the withdraw address, the relationship between BEP20 address and the withdraw address are then stored in BSC chain.

User can rebind withdraw address to a new XX address with WXX contract.

#### Mint

PB system keeps tracking the XX wallet. When a deposit transaction with enough confirmations(such as 10 confirmations) found and the amount are validated, it then be stored and put into the minting queue.
PB system keeps tracking the minting queue, and mint WXX tokens accordingly.

{{< mermaid >}}
graph LR;
XD[XCH Deposit] --> PB(PlotBridge) --> PM[WXCH Mint]
{{< /mermaid >}}

#### Burn

User may burn WXX tokens with the PB web app.
PB system keeps tracking the BSC chain. When a **burn** transaction is detected with enough confirmations (such as 10 confirmations), it will be stored and put into the withdraw queue.
PB system keeps tracking the withdraw queue, and send XX coins back to the XX withdraw address bind in BSC.

Please note that after withdraw address rebind, it may require some time for PB system to update the XX withdraw address. If user wants to ensure the withdrawal to arrive the new address, please burn WXX after some time(like 10 minutes) of the rebind.

{{< mermaid >}}
graph LR;
PBR[WXCH Burn] --> PB(PlotBridge) --> XW[XCH Withdraw]
{{< /mermaid >}}

#### Safety Considerations

All XX coin deposited are stored in the PB system wallet.
We are planning to collect then into a single address. It may be better for the community audit.

WXX are minted only when XX deposit, and are burnt for XX withdrawal. This can ensure **NO** overdraft for WXX.

For better safety, we completely separate web app and PB system. The only connection between them is the BSC blockchain network.

{{< mermaid >}}
graph LR;
App[PlotBridge App Web Server] <--> BSC([BSC Network]) <--> PB[PlotBridge App and Node]
{{< /mermaid >}}

## Current Status

#### Tokens issued

All tokens are issued in Binance Smart Chain (BSC).

| Coin Name                             | Coin Symbol | Token Symbol                   | Contract Address                           | Trading Pair                                                                                 |
| ------------------------------------- | :---------- | ------------------------------ | ------------------------------------------ | -------------------------------------------------------------------------------------------- |
| [PBP](https://www.plotbridge.io)      | PBP         | ![PBP](/images/pbp.png)PBP     | 0x217634d01809d7B9C6348D70A95AE7f5E5179de3 | [BNB/PBP](https://pancakeswap.finance/info/pool/0xb8d7e1982d01a613708b3235a5781a734f63d082)  |
| [Chia](https://www.chia.net)          | XCH         | ![奇亚](/images/wxch.png)WXCH  | 0xEc02B1b904a4e925F67fA8Bc6c5d428266F5C1a5 | [WXCH/PBP](https://pancakeswap.finance/info/pool/0x10d2a3f0f7485fcee84407bbd4272918fe864a55) |
| [Chives](https://www.chivescoin.org/) | XCC         | ![韭菜](/images/wxcc.png) WXCC | 0x1aDCC92C322c21e387e6112bf162858AF208ff3a | [WXCC/PBP](https://pancakeswap.finance/info/pool/0xa9d19fe91bbb3d9f91ca313f71aa58101015014b) |

More tokens will be added in the future. Suggestions are welcome.
