## 1. 광고주 리스트 조회 API

* 링크프라이스의 광고주 리스트를 조회



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
    category_id: "3",
    category_name: "패션",
    deeplink_yn: "Y",
    max_commission_mobile: "2%",
    max_commission_pc: "2000원",
    merchant_id: "wizwid",
    merchant_logo: "http://img.wizwid.com/WIZWID/RAW-DOC2/pc/mkt-2019-raink/logo.jpg",
    merchant_name: "위즈위드",
    merchant_url: "http://www.wizwid.com/CSW/handler/wizwid/kr/MainView-MainView",
    mobile_yn: "Y",
    return_day: 7,
    reward_yn: "Y",
    subscript: "APR",
    click_url: "http://click.linkprice.com/click.php?m=wizwid&a=A100000131&l=0000&l_cd1=B&l_cd2=1"
  }
]
```



* 정산에 관련한 정보와 같은 추가적인 머천트 상세 정보가 추가 필요 시, URL 뒤에 detail 옵션을 추가

``` 
http://api.linkprice.com/ci/service/all_merchant/A100000131/apr/cps/detail
```



### 추가 정보 응답 샘플

```json
[
  {
    category_id: "3",
    category_name: "패션",
    deeplink_yn: "Y",
    max_commission_mobile: "2%",
    max_commission_pc: "2000원",
    merchant_id: "wizwid",
    merchant_logo: "http://img.wizwid.com/WIZWID/RAW-DOC2/pc/mkt-2019-raink/logo.jpg",
    merchant_name: "위즈위드",
    merchant_url: "http://www.wizwid.com/CSW/handler/wizwid/kr/MainView-MainView",
    mobile_yn: "Y",
    return_day: 7,
    reward_yn: "Y",
    subscript: "APR",
    click_url: "http://click.linkprice.com/click.php?m=wizwid&a=A100000131&l=0000&l_cd1=B&l_cd2=1",
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



## 2. 리워드 API

* 실적 발생 시, 아래와 같은 RAW 데이터를 매체의 Endpoint URL로 전달
* POST방식으로 전송, CURL로 호출



### 전송 샘플

```json
curl --location --request POST '[매체 측의 ENDPOINT URL]' \
--data-raw '{
    "day": "20200701",
    "time": "112719",
    "merchant_id": "linkprice",
    "order_code": "oc11123",
    "product_code": "pc11123",
    "product_name" : "test product",
    "category_code": "cc11",
    "item_count": 1,
    "price": 20000,
    "commision": 500,
    "affiliate_id": "A100000000",
    "affiliate_user_id": "ac_aaa",
    "member_id" : "test_member",
    "trlog_id" : "1000232321232",
    "base_commission" : "8%",
    "incentive_commission" : "500KRW"
}'
```



### 전송 정의

| 키                   | 값                                                           | 타입      |
| -------------------- | ------------------------------------------------------------ | --------- |
| day                  | 실적발생 날짜                                                | CHAR(8)   |
| time                 | 실적발생 시간                                                | CHAR(6)   |
| merchant_id          | 머천트 ID                                                    | CHAR(10)  |
| order_code           | 주문 코드                                                    | CHAR(100) |
| product_code         | 제품 코드                                                    | CHAR(100) |
| product_name         | 제품명 * 해당 값의 캐릭터셋은 UTF-8이고 URL ENCODING 처리를 합니다. | CHAR(300) |
| category_code        | 카테고리 코드                                                | CHAR(200) |
| item_count           | 개수                                                         | INT       |
| price                | 실적 총 금액                                                 | FLOAT     |
| commision            | 커미션                                                       | FLOAT     |
| affiliate_id         | 링크프라이스 어필레이트 아이디                               | CHAR(10)  |
| affiliate_user_id    | 리워드 아이디 * click.linkprice.com 유입 URL의 "u_id" 값을 전송합니다. | CHAR(560) |
| member_id            | 머천트 사이트의 유저 ID * 해당 값의 캐릭터셋은 UTF-8이고 URL ENCODING 처리를 합니다. | CHAR(100) |
| trlog_id             | 실적 ID                                                      | CHAR(20)  |
| base_commission      | 기본 커미션. 커미션의 형태에 따라 % 혹은 KRW(원화)로 전송합니다. | CHAR(20)  |
| incentive_commission | 인센티브 커미션. 추가적으로 지급받는 커미션을 의미합니다. 커미션의 형태에 따라 % 혹은 KRW(원화)로 전송합니다. | CHAR(20)  |



## 3. 실적 조회 API

* 링크프라이스는 매월 5일에 전전월 실적에 대한 확정 처리를 진행

* 12월 6일 이후에 실적API URL을 호출하면 10월 1일 ~ 10월 31일 사이의 확정된 실적을 조회 가능



### 실적 API URL 호출 예시

```
http://api.linkprice.com/affiliate/translist.php?a_id=A100000000&auth_key=abcedfg&yyyymmdd=201910&cancel_flag=Y
```



### 매개변수 정의

| 키          | 값                                                           | 타입             |
| ----------- | ------------------------------------------------------------ | ---------------- |
| a_id        | 라스트세이브에서 발급된 어필리에이트 아이디 (고정값)         | CHAR(10), 필수   |
| auth_key    | 라스트세이브에서 발급된 인증키 (고정값)                      | CHAR(32), 필수   |
| cancel_flag | 취소 실적만 조회 시, "Y"<br/>생략하면 취소, 확정 실적 전체 조회 | CHAR(1), 옵션    |
| yyyymmdd    | 실적 조회 날짜<br/> 20191213(년월일) 또는 201912 (년월)      | VARCHAR(8), 필수 |
| page        | 페이징 시, 페이지 번호                                       | INT, 옵션        |
| per_page    | 페이징 시, 페이징할 건수                                     | INT, 옵션        |



### 응답 샘플

```json
{
  result: "0",
  list_count: "1",
  order_list: [
    {
      trlog_id: "13002318018486",
      yyyymmdd: "20150514",
      hhmiss: "111324",
      m_id: "clickbuy",
      o_cd: "20150514111324",
      p_cd: "3",
      p_nm: "회원가입",
      applied_pgm_id: "0034",
      it_cnt: 1,
      sales: 0,
      commission: 0,
      membership_id: "opmanager",
      remote_addr: "211.189.137.198",
      status: "310",
      trans_comment: "TEST실적 취소",
      create_time_stamp: "20150514"
    }
  ]
}
```



### 응답 정의

| 키                             | 값                                                           | 타입       |
| ------------------------------ | ------------------------------------------------------------ | ---------- |
| result                         | 리턴 코드<br/> 0: 정상<br/> 100: 어필아이디 없음<br/> 200: 조회일자 없음<br/> 210: 날짜 자리수가 6 또는 8자리가 아님 220: 일별실적조회이면서 날짜 자리수가 8자 리가 아님<br/> 300: 인증키가 맞지 않음 | CHAR(3)    |
| list_count                     | 조회된 실적 건수                                             | TEXT       |
| order_list[].trlog_id          | 링크프라이스에서 발급한 내부 실적 고유 코드                  | CHAR(22)   |
| order_list[].yyyymmdd          | 실적 발생 년월일                                             | CHAR(8)    |
| order_list[].hhmiss            | 실적 발생 시분초                                             | CHAR(6)    |
| order_list[].m_id              | 링크프라이스에서 발급한 광고주 고유 아이디                   | CHAR(10)   |
| order_list[].o_cd              | 주문코드                                                     | CHAR(100)  |
| order_list[].p_cd              | 상품코드                                                     | CHAR(100)  |
| order_list[].p_nm              | 상품명                                                       | CHAR(300)  |
| order_list[].applied_pgm_id    | 링크프라이스에서 발급한 프로그램 아이디                      | CHAR(4)    |
| order_list[].it_cnt            | 상품 갯수                                                    | INT        |
| order_list[].sales             | 상품 금액                                                    | INT        |
| order_list[].commission        | 적립받을 커미션 금액                                         | INT        |
| order_list[].membership_id     | 광고주의 회원 아이디                                         | CHAR(100)  |
| order_list[].remote_addr       | 구매한 사람의 아이피                                         | CHAR(300)  |
| order_list[].status            | 실적의 확정 상태  <br />100 : 미확정  <br />200 : 정산대기  <br />210 : 머천트측 정산완료  <br />220 : 어필리에이트측 정산완료 <br />300 : 취소신청<br />310 : 취소확정 | CHAR(3)    |
| order_list[].trans_comment     | 실적 확정 상태 변경 코멘트                                   | CHAR(1000) |
| order_list[].create_time_stamp | 데이터베이스 적재 시간                                       | CHAR(8)    |



* 값은 많지만 실제로 사용하는 값은 링크프라이스 고유 코드(trlog_id), 실적 확정 상태(status) 정도로 추측됩니다.