#### 어필리에이트 서비스를 돕기위해 링크프라이스에서 제공하는 API 가이드입니다.



## 1. [리워드 API](https://github.com/linkprice/AffiliateSetup/blob/api_separation/docs/%EB%A6%AC%EC%9B%8C%EB%93%9C_%EC%98%A4%ED%94%88_API.md)

* 어필리에이트 회원이 상품 구매 등으로 실적을 발생시키면 링크프라이스에서 어필리에이트로 실적 데이터를 전송하는 API 입니다.



## 2. [실적 조회 API](https://github.com/linkprice/AffiliateSetup/blob/master/docs/%EC%8B%A4%EC%A0%81_%EC%A1%B0%ED%9A%8C_%EC%98%A4%ED%94%88_API_v1.6.md)

* 요청된 기간내 발생한 실적 데이터를 제공하는 API 입니다.



## 3. 참고사항

### 정산 실적 리워드 처리 방법

* 매월 6일 실적의 정산이 완료된 후 실적 조회 API를 사용하여 확정 / 취소 실적을 확인 할 수 있습니다.

* 저장된 리워드 실적(리워드 API [1-6](https://github.com/linkprice/AffiliateSetup/blob/api_separation/docs/%EB%A6%AC%EC%9B%8C%EB%93%9C_%EC%98%A4%ED%94%88_API.md#1-6), [1-9](https://github.com/linkprice/AffiliateSetup/blob/api_separation/docs/%EB%A6%AC%EC%9B%8C%EB%93%9C_%EC%98%A4%ED%94%88_API.md#1-9))과 조회된 정산 실적(리워드 API [1-11](https://github.com/linkprice/AffiliateSetup/blob/api_separation/docs/%EB%A6%AC%EC%9B%8C%EB%93%9C_%EC%98%A4%ED%94%88_API.md#1-11))의 머천트 아이디, 주문 번호, 상품코드가 같은 데이터를 찾은 후 주문 상태에 따라 업데이트 하여 줍니다.

* 머천트 정산 방식에 따라 같은 머천트 아이디, 주문번호, 상품번호의 리워드 실적(리워드 API [1-6](https://github.com/linkprice/AffiliateSetup/blob/api_separation/docs/%EB%A6%AC%EC%9B%8C%EB%93%9C_%EC%98%A4%ED%94%88_API.md#1-6), [1-9](https://github.com/linkprice/AffiliateSetup/blob/api_separation/docs/%EB%A6%AC%EC%9B%8C%EB%93%9C_%EC%98%A4%ED%94%88_API.md#1-9))과 정산 실적(리워드 API [1-11](https://github.com/linkprice/AffiliateSetup/blob/api_separation/docs/%EB%A6%AC%EC%9B%8C%EB%93%9C_%EC%98%A4%ED%94%88_API.md#1-11))의 일부 데이터(특히 **금액**, **커미션**)가 달라질 수 있습니다.

* 드물게 예외 케이스가 발생하여, 리워드 데이터를 Insert, Delete가 필요할 수 도 있습니다.
