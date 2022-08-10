---
title: Add KSD as Collateral
author: klaybank
discussions: https://forum.klaybank.org/t/add-ksd-as-collateral/17
created: 10.05.2022
updated: 
---

## Summary

KSD는 이미 Klaybank에 Listing되어있고 Deposit, Borrow가 가능합니다. Deposit되어있는 KSD를 Collateral로 사용하게 함으로써 Klaybank 내의 Asset 활용처를 늘리고 Market의 다양성을 제공합니다.

## Specification

KSD는 Kokoa Finance에서 개발한 크립토 자산 담보 기반의 탈중앙화 스테이블코인입니다. KSD는 1달러에 소프트 페깅된 스테이블 자산이며 여러 담보물로 인해 가치가 유지됩니다. 이는 클레이튼 생태계 최초의 초과담보 스테이블 코인이며 이더리움의 MakerDAO와 유사합니다. 클레이튼 내에서 OUSDC의 시가총액을 뛰어 넘었으며 레버리지 등의 꾸준한 개발을 하고 있습니다.

Klaybank에는 4만 달러 규모의 KSD Market이 형성되어 있으며 이는 다른 Asset보다 현저히 적은 수준의 Size입니다.

![onchain_1](https://raw.githubusercontent.com/klaybank/proposal/main/images/proposal-1/onchain_1.png)

총 발행량 대비 Klaybank에 예치된 자산의 비율을 보면 다른 Stable Asset에 비해 KSD가 현저하게 적은 수치를 가지고 있는 것을 확인할 수 있습니다. KSD를 담보로 사용할 수 있게 함으로써 Klaybank의 KSD Market Size를 키우는 것을 기대해볼 수 있습니다.

![onchain_2](https://raw.githubusercontent.com/klaybank/proposal/main/images/proposal-1/onchain_2.png)

위의 표에서 OUSDT, KDAI, OUSDC, KSD의 온체인 데이터를 확인할 수 있습니다. 위의 데이터는 각 자산들이 클레이튼 내에서 수치적으로 얼만큼의 지위를 가진지 간접적으로 보여줍니다. Total Supply로 Market Cap을, Holders와 Transfers로 각 자산의 탈중앙성 및 활용도를, Holders와 Volatility로 시장 위험성을 유추해볼 수 있습니다.
아래는 OUSDC와 KSD의 홀더 온체인 정보입니다.

![scope_usdc](https://raw.githubusercontent.com/klaybank/proposal/main/images/proposal-1/scope_ksd.png)

![scope_ksd](https://raw.githubusercontent.com/klaybank/proposal/main/images/proposal-1/scope_usdc.png)

대부분의 상위 홀더들은 타 디파이 프로토콜에서 활용되고 있습니다. KSD의 1위 홀더인 0x5e6215dfb33b1fb71e48000a47ed2ebb86d5bf3d 은 Kokoa finance의 Earn Contract인 dKSD 토큰입니다. 61.9%에 달하는 유동성이 한 곳에 집중되어 있으며 OUSDC가 다양한 곳에서 사용되는 것에 비해 상당히 사용처가 제한되어있음을 알 수 있습니다.
위의 온체인 정보를 종합하면 OUSDC보다 많이 쓰이는 Stable Asset이지만 활용처가 다소 떨어지는 모습을 확인할 수 있습니다. Klaybank에서 KSD에 대한 담보사용 승인은 KSD의 활용처가 늘어남과 동시에 Klaybank Market Size 확대를 기대할 수 있습니다.

### Risk Parameters

앞서 KSD의 탈중앙성 및 활용도를 제시했습니다. 이는 Risk Parameter의 근거로 쓰이며 시장 위험성에 대한 추가 설명이 필요합니다. 시장 위험성은 자산이 시장 내에서 얼마나 위험에 노출되어있는지를 나타내며 이는 프로토콜의 안전성을과 직결됩니다. 프로토콜이 얼마나 안전할 수 있는가는 프로토콜이 담보 자산에 대해 얼만큼 안전하게 청산을 하며 자산을 지킬 수 있는가로 귀결됩니다. 우리는 아래와 같은 수치 도출로 청산에 대비가 필요하며 적절한 Risk Parameter를 설정해야합니다. 수치들은 최악의 시나리오를 상정했으며 세부 수식은 제외했습니다.

1. LP에 예치된 자산의 양
    - 여러 LP들에 예치된 KSD 조사결과 약 4,415,903 KSD가 스왑할 수 있는 LP에 예치된걸로 확인되었습니다.
2. 등락폭
    - KSD가격이 약 10분내로 바로 회복되지않는 최대 등락폭은 약 20%로 확인되었습니다.
3. 목표 예치량 - Klaybank에 예치되는 예치될 KSD
    - i4i의 KSD-KLAY보다 높은 수치인 2,000,000개를 가정
4. 청산 보너스
    - 다른자산들과 동일한 10%를 채택합니다.
5. 담보 비율 분포
    - 해당 자산을 이용해 담보를 받은 비율을 다음과 같이 가정합니다. 이는 최대 LTV의 N% 비율로 담보를 잡았다는것을 의미하며, 예를들어 70% LTV의 담보비율 90%는 자산의 63%가 담보로 잡혀있다는것을 의미합니다.

아래 표는 많은 사용자들이 자산의 대부분을 담보로 사용하고있는 극단적인 상황의 분포를 가정하며, 최악의 경우를 생각하기위한 분포입니다.

![ratio](https://raw.githubusercontent.com/klaybank/proposal/main/images/proposal-1/ratio.png)

LTV가 70%, Liquidation Threshold가 75%일때 최대 20%가 등락하면 담보잡힌 자산의 42%를 청산해야한다는 결과가 나옵니다. 이를 KSD양으로 환산하면 335,125개의 KSD를 청산해야합니다.

이는 LP예치된 양인 4,415,903 KSD가 Price Impact, Liquidation Bonus를 고려했을때 손해 없이 청산가능한 거의 최대치입니다. ( 약 350,000 KSD 까지 한번에 손해 없이 청산 가능 )

따라서 이러한 가정에서 프로토콜이 청산을 무리없이 해낼 수 있는 다음과 같은 Risk Parameter 수치를 제안합니다.

- LTV 70%
- Liquidation Threshold 75%
- Liquidation Bonus 10%
- Reserve Factor 25%

## Implementation
1. Set pool admin to executor
   - contract: `LendingPoolAddressesProvider`
   - method: `setPoolAdmin`
2. Configure asset
   - contract: `BTokensAndRatesHelper`
   - method: `configureReserves`
3. Restore pool admin again
   - contract: `LendingPoolAddressesProvider`
   - method: `setPoolAdmin`