---
title: KIP 11 Preparation for Delisting WEMIX
author: klaybank
discussions: https://forum.klaybank.org/t/preparation-for-delisting-wemix/39
created: 05.12.2022
updated: 
---

## Title

Preparation for Delisting WEMIX

## Summary

WEMIX 상장폐지 대응을 위한 선행 작업을 실시합니다.

## Specification

$WEMIX는 DAXA의 결정에 의해 Upbit, Bithumb 등 한국 주요 거래소에서 상장폐지가 논의되고 있습니다. 이에 따라 클레이뱅크도 리스크를 관리하기 위하여 [$WEMIX를 담보 자산에서 제외](https://app.klaybank.org/governance/8-0x3bb55cf8c57a6a475a6a7821bdf9eb7b327a55849aa4b13abedff7f6be46a3fb) 하였습니다.

$WEMIX는 높은 가격 변동성을 띄고 있고 클레이뱅크에서는 $WEMIX의 Utilization Rate는 높은 수치를 지속적해서 띄고 있습니다. (최고 99.9%) 이는 청산자의 청산 유인을 떨어뜨릴뿐더러 최악의 경우 악의적인 공격자에 의해 악성 부채가 남거나, 뱅크런 등의 공격으로 이어질 수도 있습니다.

이에 Klaybank에서 $WEMIX를 delisting 하는 방향으로 결정하였습니다. 완전한 상장폐지를 하기 전에 아래와 같은 선행 작업을 시행하고자 합니다.

1. Liquidation Threshold 조절
    - 악성 부채의 가능성이 있는, 담보로 사용되고 있는 $WEMIX에 대한 조치입니다.
    - Liquidation Threshold: 55% → 5%

2. Borrow 비활성화
    - 상장 폐지에 앞서 Borrow를 비활성화합니다. 
      
3. Borrow APR 조절
    - U Optimal과 Slope를 조절해 Borrow APR을 높여 상환을 유도합니다.
    - U Optimal: 45% → 10%
    - Variable Slope 1: 7% → 200%
    - Variable Slope 2: 300% → 600%

## Implementation
- contract: LendingPoolConfigurator
- method1: configureReserveAsCollateral
- method2: disableBorrowingOnReserve
- method3: setReserveInterestRateStrategyAddress