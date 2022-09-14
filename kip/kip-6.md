---
title: KIP 6 Update WEMIX LTV
author: klaybank
discussions: https://forum.klaybank.org/t/update-wemix-ltv/30
created: 15.09.2022
updated: 
---

## Title

Update WEMIX LTV

## Summary

WEMIX의 LTV를 25%에서 50%로 상향 조절합니다.

## Specification

WEMIX가 클레이뱅크에 상장하고 나서 두 달이 지났지만, 신규 토큰의 상장에도 WEMIX를 deposit, borrow하는 유저들은 저조 했습니다. 시장이 하락세 인것이 가장 큰 이유겠지만 25%라는 낮은 LTV도 영향이 있다고 판단내렸습니다. 이에 LTV를 상향조절 하고자 합니다.

25%라는 LTV는 WEMIX가 타 자산보다 변동성이 큰 토큰이기 때문에 고려된 보수적인 수치였습니다. 클레이뱅크 측은 2달 간 WEMIX 자산에 대한 사용자들의 반응을 확인하였고, 이에 현재 시장 상황을 기준으로 새로운 Risk Parameter를 제안합니다.

1. **LP에 예치된 자산의 양**
    - LP에 예치된 $WEMIX는 2개월 전 275만개보다 증가한 300만개 정도로 확인되었습니다.
2. **등락폭**
    - 10분 기준 최대 등락폭은 약 30~45%로 확인되었습니다.
3. **목표 예치량**
    - Kleva의 WEMIX 단일 예치의 약 1/3인 200만개
4. **청산 보너스**
    - 동일하게 15%
5. **담보 비율 분포**

   $WEMIX 최대 LTV의 N% 비율로 담보를 잡은 분포를 나타냅니다. 극단적인 상황을 가정한 분포입니다.
   ![collateral_ratio](https://raw.githubusercontent.com/klaybank/proposal/main/images/proposal-6/collateral_ratio.png)



LTV가 50%, Liquidation Threshold가 55%일 때 최대 30%가 등락하면 담보잡힌 자산의 31%를 청산해야한다는 결과가 나옵니다. 이를 $WEMIX 양으로 환산하면 약 200,000개의 $WEMIX를 청산해야합니다.

이는 LP에 예치된 양인 300만개의 $WEMIX가 Price Impact, Liquidation Bonus를 고려했을 때 손해 없이 청산가능한 수치입니다.

- LTV 25% → 50%
- Liquidation Threshold 30% → 55%
- Liquidation Bonus 15%
- Reserve Factor 40%

## Implementation

Risk Parameter를 조절합니다.

- contract: LendingPoolConfigurator
- method: configureReserveAsCollateral