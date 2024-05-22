## 광고주 리스트 조회 API

* CPS 전체

```
http://api.linkprice.com/ci/service/all_merchant/A100000131/all/cps
```

* CPS 승인

```
http://api.linkprice.com/ci/service/all_merchant/A100000131/apr/cps
```

* CPA 전체

```
http://api.linkprice.com/ci/service/all_merchant/A100000131/all/cpa
```

* CPA 승인

```
http://api.linkprice.com/ci/service/all_merchant/A100000131/apr/cpa
```

### 기본 응답 샘플

```json
[
  {
    "category_id": "3",
    "category_name": "패션",
    "deeplink_yn": "Y",
    "max_commission_mobile": "2%",
    "max_commission_pc": "2000원",
    "merchant_id": "wizwid",
    "merchant_logo": "http://img.wizwid.com/WIZWID/RAW-DOC2/pc/mkt-2019-raink/logo.jpg",
    "merchant_name": "위즈위드",
    "merchant_url": "http://www.wizwid.com/CSW/handler/wizwid/kr/MainView-MainView",
    "mobile_yn": "Y",
    "return_day": 7,
    "reward_yn": "Y",
    "subscript": "APR",
    "click_url": "http://click.linkprice.com/click.php?m=wizwid&a=A100000131&l=0000&l_cd1=B&l_cd2=1"
  }
]
```



* 정산에 관련한 정보와 같은 추가적인 머천트 상세 정보가 추가 필요 시, URL 뒤에 detail 옵션을 추가

``` 
http://api.linkprice.com/ci/service/all_merchant/A100000131/apr/cps/detail
```



### 추가 정보 응답 샘플

```
[
  {
    "category_id": "3",
    "category_name": "패션",
    "deeplink_yn": "Y",
    "max_commission_mobile": "2%",
    "max_commission_pc": "2000원",
    "merchant_id": "wizwid",
    "merchant_logo": "http://img.wizwid.com/WIZWID/RAW-DOC2/pc/mkt-2019-raink/logo.jpg",
    "merchant_name": "위즈위드",
    "merchant_url": "http://www.wizwid.com/CSW/handler/wizwid/kr/MainView-MainView",
    "mobile_yn": "Y",
    "return_day": 7,
    "reward_yn": "Y",
    "subscript": "APR",
    "click_url": "http://click.linkprice.com/click.php?m=wizwid&a=A100000131&l=0000&l_cd1=B&l_cd2=1",
    "when_trans": "실시간 실적 전송",
    "trans_reposition": "전체 실적 중 확정 건 제외한 실적 취소",
    "commission_payment_standard": "구매 월 기준 익익월 6일 지급",
    "deny_product": "",
    "deny_ad": "상호 혹은 오타 키워드 활용한 유료 광고^유사 및 오타 도메인 포워딩^리워드 프로그램 배포^프로그램(키워드, 주소창, 리워드툴바, 바로가기 등)배포",
    "notice": "",
    "app_ios_yn": "N",
    "app_android_yn": "N"
  }
]
```



### 기본 응답 정의

| 키                    | 값                                                           | 타입      |
| --------------------- | ------------------------------------------------------------ | --------- |
| category_id           | 광고주가 속한 카테고리 코드                                  | CHAR(2)   |
| category_name         | 광고주가 속한 카테고리 명                                    | CHAR(50)  |
| deeplink_yn           | 딥링크 허용 여부<br />딥링크 : 제휴링크를 통해 원하는 상품페이지로 바로 이동하는 링크를 의미<br />Y : 허용, N: 거부 | CHAR(1)   |
| max_commission_mobile | 모바일 최대 커미션 율 혹은 금액<br />커미션율 : "2%" or 커미션금액 : "2000원" | TEXT      |
| max_commission_pc     | PC 최대 커미션 율 혹은 금액<br />커미션율 : "2%" or 커미션금액 : "2000원" | TEXT      |
| merchant_id           | 링크프라이스가 지정한 광고주 아이디                          | CHAR(10)  |
| merchant_logo         | 광고주 로고 이미지 URL<br />가로사이즈 : 120px, 세로사이즈 60px | CHAR(300) |
| merchant_name         | 광고주명                                                     | CHAR(200) |
| merchant_url          | 광고주 대표 주소                                             | CHAR(300) |
| mobile_yn             | 모바일 지원 여부<br />Y : 모바일 지원<br />N : 모바일 미지원 | CHAR(1)   |
| return_day            | 광고 효과 인정 기간 일수<br />사용자가 제휴링크를 통해 진입 후 실적 발생 인정 기간 | INT       |
| reward_yn             | 광고 리워드 여부<br />Y : 리워드<br />N : 비리워드<br />A : 리워드, 비리워드 둘다 | CHAR(1)   |
| subscript             | 광고주에 대한 매체의 승인 상태<br />APR : 승인완료<br />DEN : 승인거부<br />REQ : 광고주에게 승인요청상태 | CHAR(3)   |
| click_url             | 제휴링크                                                     | TEXT      |



### 추가 정보 응답 정의

| 키                          | 값                         | 타입    |
| --------------------------- | -------------------------- | ------- |
| when_trans                  | 실적발생 날짜              | TEXT    |
| trans_reposition            | 정산 방식                  | TEXT    |
| commission_payment_standard | 지급 방식                  | TEXT    |
| deny_product                | 커미션 미인정 상품         | TEXT    |
| deny_ad                     | 활동 불가 방식             | TEXT    |
| notice                      | 유의사항                   | TEXT    |
| app_ios_yn                  | 실적인정범위 유무(iOS)     | CHAR(1) |
| app_android_yn              | 실적인정범위 유무(Android) | CHAR(1) |
