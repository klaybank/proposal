---
title: KIP 4 Update BTC LTV
author: klaybank
discussions: https://forum.klaybank.org/t/update-btc-ltv/29
created: 04.09.2022
updated: 
---

## Summary
BTC의 LTV를 45%에서 65%로 상향 조절합니다.

## Specification

1. LP에 예치된 자산의 양
    - LP에 예치된 $BTC는 약 100개 정도로 확인되었습니다.

2. 등락폭
    - 10분 기준 최대 등락폭은 약 10 ~ 20%로 확인되었습니다.

3. 목표 예치량
    - 현재 클레이뱅크에 예치된 양의 약 2배인 30개

4. 청산 보너스
    - 동일하게 10%

5. 담보 비율 분포
    - $BTC의 최대 LTV의 N% 비율로 담보를 잡은 분포를 나타냅니다. 극단적인 상황을 가정한 분포입니다.
      ![collateral_ratio](https://raw.githubusercontent.com/klaybank/proposal/main/images/proposal-4/collateral_ratio.png)

LTV가 65%, Liquidation Threshold가 70%일 때 최대 20%가 등락하면 담보잡힌 자산의 14%를 청산해야한다는 결과가 나옵니다. 이를 $BTC 양으로 환산하면 1.57개의 $BTC를 청산해야합니다.

이는 LP에 예치된 양인 100개의 $BTC가 Price Impact, Liquidation Bonus를 고려했을 때 손해 없이 청산가능한 수치입니다.

현재 LP와 클레이뱅크에 예치된 자산을 비교했을 시 더 높은 LTV 설정이 가능할 것으로 보이지만, 점진적인 상향이 안전하다고 판단되기 때문에 아래와 같은 Risk Parameter를 제안합니다.

- LTV 45% -> 65%
- Liquidation Threshold 50% -> 70%
- Liquidation Bonus 10%
- Reserve Factor 25%

## Implementation

Risk Parameter를 조절합니다.

- contract: LendingPoolConfigurator
- method: configureReserveAsCollateral