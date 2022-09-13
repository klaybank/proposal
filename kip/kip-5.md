---
title: KIP 5 Pause oETH Borrowing
author: klaybank
discussions: https://forum.klaybank.org/t/pause-oeth-borrowing/31
created: 09.09.2022
updated: 
---

## Title

Pause oETH Borrowing

## Summary

이더리움 머지 업데이트 기간 동안 oETH Borrowing 기능을 중단시킵니다.

## Specification

### Motivation

이더리움 머지는 이더리움 체인의 컨센서스 알고리즘을 PoW에서 PoS로 전환하는 대규모 업데이트입니다. 이는 체인의 하드포크가 필요하고 PoS로 전환하지 않고 기존 PoW 알고리즘을 유지하고자하는 집단이 존재함에 따라 ETHPoW와 ETHPoS로 체인별 ETH를 구분하는 움직임이 있습니다. 거래소들은 각 체인 위에서 사용될 ETHW와 ETHS라는 코인을 각각 상장시켜 시장에 유통시키고 있고(혹은 예정 중이고), 이더리움의 디파이 프로토콜들 또한 머지 업데이트를 앞두고 많은 혼란을 겪고 있습니다.

### Proposal

클레이튼의 이더리움 기반 자산 또한 이더리움 머지 업데이트에 영향을 받을 것이며 클레이 뱅크는 오지스 브릿지 자산(oETH, oUSDT, oUSDC, oDAI)을 취급하고 있습니다. 참고로 오지스는 이더리움 머지 업데이트를 대비해 다음과 같은 결정을 내렸습니다.

- 기존 oToken은 ETHPoS 자산에 기반을 한다.
- oToken 소유자에게 oTokenW를 에어드랍한다. (클레이뱅크의 oTokenW 에어드랍 계획은 현 거버넌스와 별개로 따로 논의됩니다)

이에 클레이 뱅크가 다음과 같은 리스크에 노출될 수 있음을 인지하였습니다.

- ETHPoS 가격 변동성
- ETHPoW 에어드랍 수령을 위한 과도한 레버리지, 높은 Utilization Rate 형성

높은 Utilization Rate와 가격 변동이 동반될 수 있음에 따라 클레이뱅크는 이더리움 머지 업데이트 기간 동안 oETH Borrowing 기능을 중단시키고자 합니다. 기한은 거버넌스가 통과 된 시점부터 머지 업데이트 이후 시장이 안정화 되었다고 판단하는 시점까지입니다.

## Implementation

- contract: LendingPoolConfigurator
- method: disableBorrowingOnReserve