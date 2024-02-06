# <center>Linkprice  어필 실적/취소 주문내역 조회 API</center>

본 문서는 어필리에이트의 리워드 서비스를 위해 링크프라이스에서 제공하는 실적 조회 API 사용 가이드입니다. 기간내 발생한 실적 정보를 조회하고 해당 실적의 상태를 확인할 수 있습니다. 인증키의 발급은 링크프라이스 어필리에이트 담당자에게 문의 부탁드립니다. 

<b>문의 : [[고객센터]](https://www.linkprice.com/link/views/about_us/contact_us_detail.html?cat_id=1)</b> 



## **REQUEST**   

### **조회 URL 예**

> **모든 실적 조회**
>
> * 기간내 모든 실적을 검색합니다. 월 단위 검색은 1일 부터 마지막 일까지 모든 날짜를 검색합니다.
>
> api.linkprice.com/affiliate/translist.php ?a_id=[A코드(사이트코드)] & auth_key=[인증키] & yyyymmdd=20231120



> **취소 외 실적 조회**
>
> - 기간내 일반, 정산대기, 정산완료 실적을 검색합니다.
>
> api.linkprice.com/affiliate/translist.php ?a_id=[A코드(사이트코드)] & auth_key=[인증키] & yyyymmdd=20231120 & cancel_flag=N



> **취소 실적 조회** 
>
> - 기간내 취소신청, 취소완료 실적을 검색합니다.
>
> api.linkprice.com/affiliate/translist.php ?a_id=[A코드(사이트코드)] & auth_key=[인증키] & yyyymmdd=20231120 & cancel_flag=Y



### **파라미터 설명**

| **파라미터 값** | **타입** | **길이** | **필수여부** | **설명**                                                                                                                                 |
| :-------------: | :------: | :------: | :----------: |----------------------------------------------------------------------------------------------------------------------------------------|
|      a\_id      | VARCHAR  |    10    |     필수     | 링크프라이스에 가입된 A코드(사이트코드, A100~ 으로 시작하는 코드입니다)                                                                                           |
|    auth\_key    | VARCHAR  |    32    |     필수     | 링크프라이스가 발행한 인증키값                                                                                                                       |
|    yyyymmdd     | VARCHAR  |  8 \| 6  |     필수     | 조회일자<br>YYYYMMDD : 일 단위 실적 조회<br>YYYYMM : 월 단위 실적 조회                                                                                   |
|  cancel\_flag   | VARCHAR  |    1     |     옵션     | 취소주문 조회<br>Y : 취소 실적 조회<br>N : 취소 외 실적 조회                                                                                              |
|    currency     | VARCHAR  |    3     |     옵션     | ISO 4217 통화 코드<sup>[[1]](#currency_list)</sup> 기본값 KRW<br>판매 합계금액, 어필 커미션 항목을 구매일 기준 환율을 반영하여 <br />요청된 통화로 변환 ※ 지원되는 통화 목록은 문서 최하단 참조 |
|  merchant\_id   | VARCHAR  |    10    |     옵션     | 해당 머천트ID의 실적만 조회                                                                                                                       |
|      page       |   INT    |    11    |     옵션     | 페이지 번호 (Paging 처리)                                                                                                                     |
|    per\_page    |   INT    |    11    |     옵션     | 페이지당 데이터 (Paging 처리, 기본값 1000)<br>페이지당 몇 건의 정보를 취득할 것인지 지정합니다.                                                                         |





## RESPONSE

### JSON 형식 데이터 응답

|  **항목**  | **타입** | **길이** | **설명**                                                     |
| :--------: | :------: | :------: | ------------------------------------------------------------ |
|   result   | VARCHAR  |    3     | 결과 코드<sup>[[2]](#result_code)</sup>                      |
| list_count |   INT    |    11    | 검색된 전체 실적 수<br>※ page 사용시에도 전체 건수 리턴      |
| order_list |  ARRAY   |    -     | 검색된 데이터 배열<br>※ 검색된 데이터가 없을 경우 빈 배열 리턴 |



### **order_list 데이터 항목 설명**

|      **항목**       | **타입** |                **길이**                 | **설명**                                                         |
| :-----------------: | :------: |:-------------------------------------:|----------------------------------------------------------------|
|      trlog\_id      | VARCHAR  |                  14                   | 주문 고유번호                                                        |
|        m\_id        | VARCHAR  |                  10                   | 머천트 아이디                                                        |
|        o\_cd        | VARCHAR  |                  100                  | 주문 번호                                                          |
|        p\_cd        | VARCHAR  |                  100                  | 상품 코드                                                          |
|        p\_nm        | VARCHAR  |                  300                  | 상품명                                                            |
|       it\_cnt       | VARCHAR  |                  11                   | 주문수량                                                           |
|      user\_id       | VARCHAR  |                  560                  | 매체 사용자 정보<br>click 주소를 통해 u\_id로 전달된 값                         |
|       status        | VARCHAR  |                   3                   | 100 : 일반<br>300 : 취소신청<br>310 : 취소완료<br>200 : 정산대기<br>210 : 정산완료 |
|        c\_cd        | VARCHAR  |                  200                  | 카테고리 코드                                                        |
| create\_time\_stamp | VARCHAR  |                   8                   | 실적생성일                                                          |
|   applied_pgm_id    | VARCHAR  |                   4                   | 적용된 머천트 프로그램 코드                                                |
|      yyyymmdd       | VARCHAR  |                   8                   | 주문 일자                                                          |
|       hhmiss        | VARCHAR  |                   6                   | 주문 시간                                                          |
|   trans\_comment    | VARCHAR  |                 1000                  | 실적 취소 사유(값이 있을 경우에만)                                           |
|        sales        |   INT    |                  11                   | 판매 합계금액 (기본값 KRW)                                              |
|     commission      |   INT    |                  11                   | 어필 커미션 (기본값 KRW)                                               |
|      pgm_name       | VARCHAR  |                  100                  | 적용된 머천트 프로그램명                                                  |
|        is_pc        |   ENUM   | mobile \| pc \| app \| ios \| android | 매체 사용자가 접속한 플랫폼 구분                                             |
|      pur_rate       | VARCHAR  |                   -                   | 적용된 머천트 프로그램의 건당 커미션 금액 또는 구매액의 커미션 비율. 예) 1000원 또는 0.5%       |



### <a name="result_code">서버 응답 코드 및 메시지</a>

|Result | 메시지                         |
| :-: |-----------------------------|
|0 | 조회 성공                       |
|100 | A코드 (사이트코드)(a_id) 없음             |
|101 | 정상 페이지 번호(page)가 아님         |
|200 | 조회일자(yyyymmdd) 없음           |
|210 | 조회일자(yyyymmdd) 길이 오류        |
|300 | 인증키(auth_key)가 맞지 않음        |
|400 | 통화단위(currency)를 지원하지 않음     |



### 조회 성공시 응답 예

```json
GET https://api.linkprice.com/affiliate/translist.php?a_id=[A코드(사이트코드)]&auth_key=[인증키]&yyyymmdd=20231120
{
    "result": "0",
    "list_count": 2,
    "order_list": [
        {
            "trlog_id": "18000406750585",
            "m_id": "clickbuy",
            "o_cd": "recover_231019_182249",
            "p_cd": "recover_231019_182249",
            "p_nm": "pn_recover_5",
            "it_cnt": "1",
            "user_id": "u_id_recover_5",
            "status": "100",
            "c_cd": "test_c_cd",
            "create_time_stamp": "20231020",
            "applied_pgm_id": "0038",
            "yyyymmdd": "20231017",
            "hhmiss": "000000",
            "trans_comment": "",
            "sales": 39900,
            "commission": 1,
            "pgm_name": "tt_mo",
            "is_pc": "mobile",
            "pur_rate": "1원"
        },
        {
            "trlog_id": "18000406750586",
            "m_id": "clickbuy",
            "o_cd": "recover_231019_182243",
            "p_cd": "recover_231019_182243",
            "p_nm": "pn_recover_4",
            "it_cnt": "1",
            "user_id": "u_id_recover_4",
            "status": "100",
            "c_cd": "test_c_cd",
            "create_time_stamp": "20231020",
            "applied_pgm_id": "0038",
            "yyyymmdd": "20231017",
            "hhmiss": "000000",
            "trans_comment": "",
            "sales": 39900,
            "commission": 1,
            "pgm_name": "tt_mo",
            "is_pc": "mobile",
            "pur_rate": "1원"
        }
    ]
}
```


### 조회 오류시 응답 예

- 조회일자(yyyymmdd) 누락
```json
GET https://api.linkprice.com/affiliate/translist.php?a_id=[A코드(사이트코드)]&auth_key=[인증키]
{
    "result": "200",
    "list_count": 0,
    "order_list": []
}
```

### <a name="currency_list">지원되는 ISO 4217 통화코드</a>

- 조회시 판매 합계금액과 어필 커미션을 변환할 수 있는 통화코드(currency) 목록입니다. 환율정보는 매일 갱신됩니다.

| 코드 | 통화                |
| :--: | ------------------- |
| CNY  | 중화인민공화국 위안 |
| USD  | 미국 달러           |
| EUR  | 유로                |
| JPY  | 일본 엔             |
| AUD  | 오스트레일리아 달러 |
| GBP  | 파운드 스털링       |
| VND  | 베트남 동           |
| CHF  | 스위스 프랑         |
| HKD  | 홍콩 달러           |
| PHP  | 필리핀 페소         |
| SGD  | 싱가포르 달러       |
| TWD  | 신 대만 달러        |
| BRL  | 브라질 헤알         |
| IDR  | 인도네시아 루피아   |
| MYR  | 말레이시아 링깃     |
| PLN  | 폴란드 즈워티       |
| THB  | 태국 밧             |
| CAD  | 캐나다 달러         |
| INR  | 인도 루피           |
| NZD  | 뉴질랜드 달러       |
| RUB  | 러시아 루블         |
| TRY  | 튀르키예 리라       |
