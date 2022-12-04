---
title: KIP 9 Disable WEMIX as Collateral
author: klaybank
discussions: https://forum.klaybank.org/t/disable-wemix-as-collateral/36
created: 25.11.2022
updated: 
---

## Title

Disable WEMIX as Collateral

## Summary

WEMIX를 담보 자산에서 제외합니다. 

## Specification

WEMIX가 DAXA의 결정에 의해 Upbit, Bithumb 등 한국 주요거래소에서 상장폐지가 결정됨에 따라 Klaybank도 프로토콜, 홀더들의 리스크 관리를 위하여 담보 자산에서 제외시키고자 합니다.

### Risk Parameter

- LTV 50% → 0%
- Liquidation Threshold 55%
- Liquidation Bonus 15%
- Reserve Factor 40%

## Implementation

Risk Parameter를 조절합니다.
- contract: LendingPoolConfigurator
- method: configureReserveAsCollateral