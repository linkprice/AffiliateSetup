#### 어필리에이트 서비스를 돕기 위해 링크프라이스에서 제공하는 API 가이드입니다.

## 1. 리워드의 개요
> 어필리에이트의 회원이 실적을 발생시키면 해당 회원에게 포인트나 적립금 등의 보상을 지급하는 서비스입니다.  
> 사이트를 운영하여, 리워드를 지급할 회원들이 있는 어필리에이트에게 적합합니다.
> 
> 본 내용의 리워드 API와 실적 조회 API는 어필리에이트가 리워드 서비스를 운영할 수 있도록 지원합니다.  
> 리워드 API를 통해 실적 발생 시 실적 정보를 받을 수 있으며, 실적 조회 API를 통해 실적의 상태(확정 or 취소)를 조회할 수 있습니다.
> 
> **※ 본문 하단 주의사항을 필히 읽어보시기 바랍니다.**

#### 리워드 서비스는 다음과 같은 흐름으로 운영됩니다.
![](https://raw.githubusercontent.com/linkprice/AffiliateSetup/guide_renewal/reward_diagram_240701.jpg)

1. 어필리에이트의 제휴 링크를 회원이 클릭합니다.
2. 어필리에이트는 제휴 링크에 리워드 지급을 위한 회원 구분 값(u_id)을 추가하여 링크프라이스 클릭 서비스로 전달합니다. [[리워드 API - u_id를 제휴 링크와 연동하는 방법]](https://github.com/linkprice/AffiliateSetup/blob/guide_renewal/docs/%EB%A6%AC%EC%9B%8C%EB%93%9C_%EC%98%A4%ED%94%88_API.md#1-%EB%A6%AC%EC%9B%8C%EB%93%9C-%EC%9D%B4%EC%9A%A9%EB%B0%A9%EB%B2%95)
3. 실적 추적 및 성과 분석을 위해 링크프라이스 제휴 링크 파라미터들은 머천트 웹사이트에 트래킹 쿠키로 저장됩니다. 그다음 머천트 웹사이트로 이동됩니다.
4. 어필리에이트 회원이 머천트의 제품을 구매하여 실적을 발생시킵니다.
5. 머천트는 전달받은 어필리에이트 정보와 구매 정보를 링크프라이스에게 전송합니다.
6. 링크프라이스는 머천트에게 받은 정보를 적재 후 어필리에이트에게 리워드 데이터로 전송합니다.
    * Affiliate Center에서 리워드 API 신청 후 승인된 어필리에이트에게만 리워드 데이터를 전송해 드립니다. [[리워드 API - 리워드 승인 신청]](https://github.com/linkprice/AffiliateSetup/blob/guide_renewal/docs/%EB%A6%AC%EC%9B%8C%EB%93%9C_%EC%98%A4%ED%94%88_API.md#1-%EB%A6%AC%EC%9B%8C%EB%93%9C-%EC%9D%B4%EC%9A%A9%EB%B0%A9%EB%B2%95)
7. 링크프라이스는 매달 머천트에게 정산에 필요한 데이터를 요청합니다.
8. 머천트는 실적의 확정 또는 취소 정보를 링크프라이스에게 전달하고, 링크프라이스는 받은 정보로 실적을 확정하거나 취소합니다.
    * 매월 20일부터 익월 5일까지 진행되는 머천트 정산은 머천트에서 발생한 실적과 링크프라이스에 적재된 실적이 일치하는지 검증하고 발생한 실적에 대한 광고비 지급을 확정하는 단계입니다. 해당 단계를 통해 구매 취소된 실적 등 머천트 기준에 부합하지 않는 실적들이 취소되며 일부 머천트는 머천트 기준에 따라 커미션 조정됩니다(커미션 세분화, 부가세 제외 등).
9. 어필리에이트는 실적 조회 API로 리워드 지급에 필요한 정보를 조회할 수 있습니다.
10. 링크프라이스는 실적 조회 API로 요청된 데이터를 어필리에이트에게 전달합니다.
11. 어필리에이트는 실적 조회 API를 통해 받은 데이터로 실적의 확정 및 취소를 확인합니다.
12. 실적이 확정된 회원에게 포인트나 적립금 등의 보상을 지급합니다.

## 2. 리워드 API [바로 가기](https://github.com/linkprice/AffiliateSetup/blob/guide_renewal/docs/%EB%A6%AC%EC%9B%8C%EB%93%9C_%EC%98%A4%ED%94%88_API.md)
* 실적 발생 시 Affiliate Center > 어필리에이트 > 툴박스 > 리워드 API에 설정된 POSTBACK URL로 발생한 실적 정보를 전송해 드리는 기능입니다.
* 주로 적립 예정 내역을 제공하는 리워드 서비스를 운영하는 어필리에이트에서 이용하는 기능입니다.

## 3. 실적 조회 API [바로 가기](https://github.com/linkprice/AffiliateSetup/blob/guide_renewal/docs/%EC%8B%A4%EC%A0%81_%EC%A1%B0%ED%9A%8C_%EC%98%A4%ED%94%88_API_v1.6.md)
* 어필리에이트의 실적 데이터를 월별, 일별 단위로 조회할 수 있는 API입니다.
* 제공되는 데이터에는 실적의 확정 여부를 알 수 있는 상태 값이 존재하기 때문에 주로 리워드 적립 확정 / 취소 시 사용됩니다.

## 4. 주의사항
> 머천트별 리워드 전송부터 정산까지 특이 사항이 많기 때문에 리워드 서비스에 머천트 추가 전   
> **Affiliate Center > 어필리에이트 > 머천트 > 머천트 상세정보**를 꼭 참고해 주시기 바랍니다.

### 리워드 전송
- 리워드 API 전송 데이터는 머천트로부터 실적 정보를 받는 즉시 전송하기 때문에 머천트의 실적 전송 시점과 같습니다.   
  대부분의 머천트는 기본적으로 구매 후 실시간으로 실적이 전송되나, 일부 머천트의 경우 배송 완료 후, 구매확정 후, 4일 이내, 실시간 실적 미 전송 후 확정 시 전송 등 컨디션이 상이 하오니 상세한 내용은 머천트 상세정보의 실시간 커미션과 유의사항을 확인해 주시기 바랍니다.
- 머천트 실적 전송 시점은 **머천트 상세정보의 실시간 커미션** 항목에서 확인하실 수 있습니다.

### 리워드 데이터
- 머천트에 따라 첫 리워드 데이터의 금액은 0으로 전송되고, 하루나 이틀 뒤에 실제 금액으로 한 번 더 전송되기도 합니다.
- 머천트별 특이사항은 **머천트 상세정보의 실시간 커미션과 유의사항** 항목에서 확인해 주시기 바랍니다.

### 커미션 정산을 위한 실적 조회
- 일반적인 머천트의 실적은 **구매월 기준 익익월**에 정산됩니다.  
    > 예) 5월 24일 구매 시 7월 6일에 정산이 완료됩니다.
- 머천트에 따라 정산 기준월이 **구매확정 월, 배송 완료 월** 등 다양하고 **익익월이 아닌 그 이상**의 기간이 걸리기도 합니다.  
    > 예) **배송완료 월 기준 4개월 후 정산**일 때, 5월 29일 구매 후  6월 2일 배송완료시 10월 6일에 정산이 완료됩니다.   
      정산된 데이터는 10월 6일 이후 8월 리포트에서 확인가능합니다.
- 머천트 정산 기준은 **머천트 상세정보의 커미션 지급 일정** 항목에서 확인하실 수 있습니다.

### 실적의 상태
- 실적 조회 API 사용 시, 일반 실적이 취소된 경우를 확인할 수 있습니다. 이때 취소 사유가 재배치에 의한 취소로 확인된다면 해당 머천트의 정산 진행 과정에 따른 취소이므로 정상입니다.
- 머천트의 정산은 크게 **배치 방식과 미배치 방식**으로 나눌 수 있습니다.
  - 배치 방식은 일반 실적을 모두 취소한 후 확정된 실적만 재생성하여 확정하는 방식입니다.  
  - 미배치 방식은 일반 실적 중 취소가 필요한 실적만 취소 후 나머지 실적을 확정하는 방식입니다.
- 머천트의 정산 방식은 **머천트 상세정보의 커미션 정산 금액** 항목에서 확인하실 수 있습니다.

### 여행 머천트의 정산
- 여행 머천트는 상품의 특성상, 당일에서 몇 개월 후까지 이용되는 기간이 다양합니다. 이용 전 취소될 수 있기 때문에 이용 완료 후 정산됩니다. 이에 따라, 동일 주문으로 예약시 생성된 실적과 이용 완료시 생성된 실적 두 개를 갖습니다.  
  - 예약 시 생성된 실적은 리워드 API로 전송되며, 익익월 정산시 취소됩니다.   
  - 이용 완료 시 생성된 실적은 리워드 API로 전송되지 않으며, 익익월 정산 시 확정됩니다.
    > 예) 2024-05-01 날짜에 2024-06-10 예약을 했다면 예약실적은 7월 정산 시 취소되며, 이용실적은 8월 정산 시 생성되어 확정됩니다. 8월 6일에 실적 조회 API를 통해 실적 확인 후 리워드를 지급하시면 됩니다.
   
    > 예) 2024-05-01 날짜에 2024-05-21 예약을 했다면 예약실적은 7월 정산 시 취소되며, 이용실적은 7월 정산 시 생성되어 확정됩니다. 7월 6일 실적 조회 API를 통해 실적 확인 후 리워드를 지급하시면 됩니다.

### 하나의 주문은 링크프라이스를 통해 리워드를 받은 후 정산 과정에서
- 실시간 실적 전송 시의 같은 주문번호로 새로운 마이너스 실적이 생길 수 있습니다.
- 머천트 정산 방식에 따라 실시간 실적 전송 시의 금액과 정산 이후의 금액이 달라질 수 있습니다.

## 5. 참고사항

### 정산 기간 (익월 20일 ~ 익익월 5일)   
> 예시) 배치 머천트   
5월 29일 구매 → 7월 6일 커미션 확정 (5월 29일 발생한 실적은 6월 20일 ~ 7월 5일 내 전체 취소 후 재배치)   
>
> 예시) 미배치 머천트   
5월 29일 구매 → 7월 6일 커미션 확정 (발생한 실적은 6월 20일 ~ 7월 5일 내 취소 건 반영)

### 정산 실적 리워드 처리 방법
**Step1)**  
리워드 API를 통해 실적을 전송받고 별도 데이터베이스에 적재합니다.

**Step2)**  
링크프라이스 정산 시점을 확인합니다.  
링크프라이스에서는 광고주와 협의하여 실적의 발생월 기준 익익월 6일에 적재된 실적의 확정/취소 처리를 진행하고 있습니다.  
EX: 7월에 발생된 실적 -> 9월 6일에 확정/취소 처리

**Step3)**  
링크프라이스 정산 완료 후, 링크프라이스의 실적 조회 API를 조회하여 머천트 아이디(merchant_id), 주문번호(order_code), 상품코드(product_code)를 기준으로
데이터베이스에 적재된 실적과 비교하여 확정/취소 처리를 진행합니다.

**주의사항)**
1. 각 광고주의 정산 방식에 따라 상품 금액(sales)과 커미션(commission) 같은 일부 데이터가 달라질 수 있습니다.
2. 드물게 예외 케이스가 발생하여 리워드 데이터를 수기로 적재, 삭제를 진행할 수도 있습니다.
