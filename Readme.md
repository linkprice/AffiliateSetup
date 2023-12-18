#### 어필리에이트 서비스를 돕기위해 링크프라이스에서 제공하는 API 가이드입니다.

![](https://raw.githubusercontent.com/linkprice/AffiliateSetup/edit_request_231211/reward_diagram.jpg)

## 1. [리워드 API 가이드 페이지 바로가기](https://github.com/linkprice/AffiliateSetup/blob/master/docs/%EB%A6%AC%EC%9B%8C%EB%93%9C_%EC%98%A4%ED%94%88_API.md)

* 링크프라이스에서 실적이 발생되면 AC > 툴박스 > 리워드API에 설정해놓으신 POSTBACK URL로 실적 정보를 전송해드리는 기능입니다.
* 주로 실시간으로 즉시 포인트 내역을 적립해야 하는 캐시백 기능이 있는 사이트에서 이용하는 기능입니다.



## 2. [실적 조회 API 가이드 페이지 바로가기](https://github.com/linkprice/AffiliateSetup/blob/master/docs/%EC%8B%A4%EC%A0%81_%EC%A1%B0%ED%9A%8C_%EC%98%A4%ED%94%88_API_v1.6.md)

* 발생된 실적 데이터를 월별, 일별로 JSON 형태로 조회할 수 있는 API 입니다.
* 리워드 API를 통해 전달 받은 실적 데이터에 대해 상태를 최신화하는데 주로 사용합니다.



## 3. 참고사항

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
