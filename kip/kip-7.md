---
title: KIP 7 Re-enable ETH Borrowing
author: klaybank
discussions: https://forum.klaybank.org/t/re-enable-oeth-borrowing/32
created: 22.09.2022
updated: 
---

## Title

Re-enable ETH Borrowing

## Summary

oETH Borrowing 기능을 다시 활성화시킵니다.

## Specification

[KIP 5](https://app.klaybank.org/governance/4-0xa050dcb58943b3361bf100b3b1f0ae44f6376b98acda779922325688ca2e64ee)에서 논의된 대로 oETH Borrowing 기능은 중단되었습니다. 이는 이더리움 머지 업데이트에 앞서 oETH에 대한 높은 Utilization Rate를 방지하기 위함이었고, 2022.09.15 15:44(KRT)에 이더리움 머지 업데이트는 완료되었습니다.

이후 여러 체인의 시장을 모니터링하였고 클레이뱅크 oETH의 Utilization Rate는 2022.09.20 기준 27%를 유지하며 위험하지 않은 수치를 보이고 있습니다. 그렇기 때문에 머지 업데이트(ETHW 및 ETHS)가 클레이뱅크에 미치는 영향 및 리스크는 없다고 판단하였고 oETH Borrowing 기능을 다시 활성화시키고자 합니다.



## Implementation

- contract: LendingPoolConfigurator
- method: enableBorrowingOnReserve