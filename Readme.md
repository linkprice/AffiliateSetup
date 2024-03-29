#### 어필리에이트 서비스를 돕기위해 링크프라이스에서 제공하는 API 가이드입니다.

![](https://raw.githubusercontent.com/linkprice/AffiliateSetup/master/reward_diagram.jpg)

## 1. 리워드의 개요
> 실적 발생 시 어떤 회원의 실적인지 실시간으로 데이터를 받을 수 있습니다.
> 리워드 데이터를 사용하면 회원들에게 가입/구매를 홍보하고, 실적이 발생하면 해당 회원에게 보상해 줄 수 있기 때문에 캐시백 또는 리워드 서비스를 운영하는 어필리에이트에 적합합니다.

1. 배너클릭
2. 클릭 링크에 어필리에이트 회원구분을 위한 u_id를 함께 전송하여 링크프라이스 click 서비스로 이동 [(리워드 API - u_id를 click과 연동하는 방법으로 이동)](https://github.com/linkprice/AffiliateSetup/blob/master/docs/%EB%A6%AC%EC%9B%8C%EB%93%9C_%EC%98%A4%ED%94%88_API.md#uid)
3. click 서비스에서 어필리에이트 정보와 함께 머천트 상품 페이지로 이동
4. 어필리에이트 회원이 머천트 상품 구매시 실적 발생
5. 머천트는 어필리에이트 정보 확인 후, 발생한 실적 데이터를 링크프라이스로 전송
6. 링크프라이스에서 어필리에이트에게 발생한 실적의 리워드 데이터 전송
    * 리워드 전송은 AC 리워드 API 승인 후 사용 가능 [(리워드 API - 리워드 승인 신청으로 이동)](https://github.com/linkprice/AffiliateSetup/blob/master/docs/%EB%A6%AC%EC%9B%8C%EB%93%9C_%EC%98%A4%ED%94%88_API.md#rewardJoin)
    * 링크프라이스로부터 리워드 데이터를 받아 처리할 페이지 작성 및 등록
    * 머천트에 따라 리워드 전송 시기 및 금액이 실적 정보와 다를수 있습니다. [(리워드 API - 리워드 주의사항으로 이동)](https://github.com/linkprice/AffiliateSetup/blob/master/docs/%EB%A6%AC%EC%9B%8C%EB%93%9C_%EC%98%A4%ED%94%88_API.md#warning)
7. 매달 한 번 링크프라이스에서 머천트측으로 정산 요청
8. 실적 확정 및 취소
9. 실적 조회 API를 통하여 링크프라이스측으로 실적 조회 요청 [(실적조회 API로 이동)](https://github.com/linkprice/AffiliateSetup/blob/master/docs/%EC%8B%A4%EC%A0%81_%EC%A1%B0%ED%9A%8C_%EC%98%A4%ED%94%88_API_v1.6.md)
10. 링크프라이스는 요청받은 실적 데이터 정보를 제공
11. 응답받은 데이터를 통해 실적의 확정 또는 취소를 확인
12. 리워드 확정

## 2. [리워드 API 가이드 페이지 바로가기](https://github.com/linkprice/AffiliateSetup/blob/master/docs/%EB%A6%AC%EC%9B%8C%EB%93%9C_%EC%98%A4%ED%94%88_API.md)

* 링크프라이스에서 실적이 발생되면 AC > 툴박스 > 리워드API에 설정해놓으신 POSTBACK URL로 실적 정보를 전송해드리는 기능입니다.
* 주로 실시간으로 즉시 포인트 내역을 적립해야 하는 캐시백 기능이 있는 사이트에서 이용하는 기능입니다.



## 3. [실적 조회 API 가이드 페이지 바로가기](https://github.com/linkprice/AffiliateSetup/blob/master/docs/%EC%8B%A4%EC%A0%81_%EC%A1%B0%ED%9A%8C_%EC%98%A4%ED%94%88_API_v1.6.md)

* 발생된 실적 데이터를 월별, 일별로 JSON 형태로 조회할 수 있는 API 입니다.
* 리워드 API를 통해 전달 받은 실적 데이터에 대해 상태를 최신화하는데 주로 사용합니다.



## 4. 참고사항

### 정산 실적 리워드 처리 방법
**Step1)**  
리워드 API를 통해 실적을 전송받고 별도 데이터베이스에 적재합니다.

**Step2)**  
링크프라이스 정산 시점을 확인합니다.  
링크프라이스에서는 광고주와 협의하여 실적의 발생월 기준 익익월 6일에 적재된 실적의 확정/취소 처리를 진행하고 있습니다.  
EX: 7월에 발생된 실적 -> 9월 6일에 확정/취소 처리

**Step3)**  
링크프라이스 정산 완료 후, 링크프라이스의 실적 조회 API를 조회 하여 머천트 아이디(merchant_id), 주문번호(order_code), 상품코드(product_code)를 기준으로
데이터베이스에 적재된 실적과 비교하여 확정/취소 처리를 진행합니다.

**주의사항)**
1. 각 광고주의 정산 방식에 따라 상품금액(sales)과 커미션(commission)같은 일부 데이터가 달라질 수 있습니다.
2. 드물게 예외 케이스가 발생하여 리워드 데이터를 수기로 적재, 삭제를 진행할 수도 있습니다.
