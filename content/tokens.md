+++
title = "Tokens"
description = "Tokens and Trading Pairs"
+++
## The Basics
* PlotBridge will be called PB for short.
* BEP20 Tokens issued by PB(such as PXCC/PXCH) will be called PXX for short.
* Blockchain networks and coins corresponding to PXX will be called XX for short.

#### Issue
PXX is the BEP20 token issued by PB on Binance Smart Chain (BSC).
The initial mint amount for PXX is 0.
Source code for PXX contracts are open and can be found in BSC block explorer website.

#### Address Binding
PB maintains a wallet for XX.
XX deposit addresses are generated in the PB wallet, and stored in BSC chain with PXX contract.
PB keeps there are enough free deposit addresses stored in BSC chain for deposit address binding.
When user bind deposit address, a free deposit address will be allocated, and the relationship between BEP20 address of user and the allocated deposit address are then stored in BSC chain.

Withdraw address of XX are always obtained from user input. When user bind the withdraw address, the relationship between BEP20 address and the withdraw address are then stored in BSC chain.

User can rebind withdraw address to a new XX address with PXX contract.


#### Mint
PB system keeps tracking the XX wallet. When a deposit transaction with enough confirmations(such as 10 confirmations) found and the amount are validated, it then be stored and put into the minting queue.
PB system keeps tracking the minting queue, and mint PXX tokens accordingly.

#### Burn
User may burn PXX tokens with the PB web app.
PB system keeps tracking the BSC chain. When a __burn__ transaction is detected with enough confirmations (such as 10 confirmations), it will be stored and put into the withdraw queue.
PB system keeps tracking the withdraw queue, and send XX coins back to the XX withdraw address bind in BSC.

Please note that after withdraw address rebind, it may require some time for PB system to update the XX withdraw address. If user wants to ensure the withdrawal to arrive the new address, please burn PXX after some time(like 10 minutes) of the rebind.

#### Safety Considerations
All XX coin deposited are stored in the PB system wallet.
We are planning to collect then into a single address. It may be better for the community audit.

PXX are minted only when XX deposit, and are burnt for XX withdrawal. This can ensure __NO__ overdraft for PXX.

For better safety, we completely separate web app and PB system. The only connection between them is the BSC blockchain network.

## Current Status
#### Tokens issued

All tokens are issued in Binance Smart Chain (BSC).

| Coin Name                             | Coin Symbol | Token Symbol                                                                                                   | Contract Address                           | Trading Pair|
| ------------------------------------- | ----------- | -------------------------------------------------------------------------------------------------------------- | ------------------------------------------ | --------------------------------------------------------------------------------------------- |
| [Chia](https://www.chia.net)          | XCH         | ![chia](/images/chia-logo.png)[PXCH](https://bscscan.com/token/0x8fCD852147d1BbA1C4f4dFf07880cCB25DD36DD7)     | 0x8fCD852147d1BbA1C4f4dFf07880cCB25DD36DD7 | [PXCH/BUSD](https://pancakeswap.finance/info/pool/0xffdfb45e3d743ec10eb793fdcee3055ea82c270c) |
| [Chives](https://www.chivescoin.org/) | XCC         | ![chives](/images/chives-logo.png)[PXCC](https://bscscan.com/token/0x24D7ec172b331c7636a5Ca604de890996e5e2028) | 0x24D7ec172b331c7636a5Ca604de890996e5e2028 | [PXCC/BUSD](https://pancakeswap.finance/info/pool/0x62608fa59fcd378cd71ce277a50f24df333b4633) |

More tokens will be added in the future. Suggestions are welcome.
