---
title: KIP 3 Add Collateral Cap
author: klaybank
discussions: https://forum.klaybank.org/t/add-collateral-cap/28
created: 10.08.2022
updated: 
---

## Summary
특정 자산에 대해 담보로 활용할 수 있는 규모의 제한을 둡니다.

## Specification
Background
Klaybank에는 현재 $KLAY, $OUSDT, $OETH, $KDAI, $OWBTC, $OUSDC, $KSD, $WEMIX 총 8개의 자산이 리스팅되어 있습니다. 이는 Claimswap, Klayswap 등의 Dex에 상장되어 있는 자산 수와 비교하면 확연하게 적은 개수입니다.

다양한 자산을 큰 장벽 없이 상장시킬 수 있는 Dex와 다르게 Lending Protocol은 상장되는 자산이 직접적으로 프로토콜에 영향을 미칠 수 있고, 이 영향은 프로토콜을 사용하는 사용자에게도 고스란히 전해집니다. 그렇기 때문에 자산이 가지는 여러 위험성을 사전에 식별하고 적절한 Parameter를 부여해야합니다.

현재 Klaytn 기반 Dex에 상장된 자산은 많지만, 상위 몇 개의 자산을 제외한 자산의 페어에 예치 된 규모는 매우 작은 수준입니다. 이는 렌딩 프로토콜의 부채 청산을 어렵게하는 요인으로 작용하기 때문에, 프로토콜 입장에서는 여러 자산을 담보 활용가능한 자산으로 리스팅하거나 높은 LTV를 가지는 파라미터를 부여하기 어렵습니다. 더군다나 이는 특정 자산을 다른 자산으로 탈취해가는 악용의 소지가 존재합니다.

예를들어서 A 자산이 Dex에서 500,000$ 규모의 페어를 가지고 있지만 유통량(Circulating Supply)이 500,000$를 넘는다면 매우 낮은 LTV 혹은 상장 불가능한 자산이 될 것입니다.

이에 대한 해결책으로 다음과 같은 프로포절을 제안합니다.

## Proposal
여러 자산에 대해 담보로 활용할 수 있는 규모에 대한 Cap을 부여합니다.

프로토콜 전체에 부여된 담보 Total Cap이 존재합니다.
사용자 개인(주소 당)에게 부여되는 담보 Personal Cap이 존재합니다.
담보 Cap의 기준은 자산의 가치가 아닌 수량으로 정의합니다. (N$가 아닌 N개)
담보 Cap의 수량은 필요할 시 거버넌스로 조절됩니다.
예를들어서 위에서 언급한 A 자산의 Total Cap을 200,000$, Personal Cap을 5,000$ 설정한다면 총 40명의 사용자가 A 자산을 최대 5,000$ 만큼 담보로 활용할 수 있습니다. 그리고 Cap은 내부적으로 오라클을 활용한 5,000$가 아닌 거버넌스로 정해진 5,000$에 해당하는 개수로 정해집니다. (A 하나당 10$ 라면 500개)

이 제안은 사용자에게 여러 자산을 활용할 수 있게 하며 프로토콜 입장에서도 여러 자산을 리스팅하며 TVL을 높일 수 있음을 기대합니다.

## Implementation
Collateral Cap의 구현을 위해서는 LendingPool.sol 내의 deposit, withdraw, borrow, liquidateCall 함수 내부의 로직 추가와 Collateral Cap을 관리하기 위한 추가 Contract 배포가 예상됩니다.