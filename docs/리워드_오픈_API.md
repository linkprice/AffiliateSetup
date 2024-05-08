# 리워드 API


## 1. <a name="warning">리워드 주의사항</a>

- **AC > 어필리에이트 > 툴박스 > 리워드 API**에서 승인 신청을 합니다. 링크프라이스로부터 승인 후 사용 가능 합니다.
    [(4. 리워드 승인 신청 참조)](#rewardJoin)
- u_id
    - 리워드를 받을 회원의 ID입니다.
    - 클릭링크에 u_id파라미터를 같이 전송합니다.[(3. u_id를 click과 연동하는 방법 참조)](#uid)
    - **길이제한: 500byte**
    - **반드시 url encoding 되어 있어야 합니다.**
- 리워드 실적 받기
    - 모든 머천트가 실시간 실적 전송을 지원하지 않습니다.
    - 머천트에 따라 하루에 1번씩만 실적을 전송하기도 합니다.
    - 머천트에 따라 실시간 실적의 금액은 0으로 전송되고, 익일이나 익익일에 실제 금액이 전송되기도 합니다.
- 하나의 주문은 링크프라이스를 통해 리워드를 받은 이후에, 정산 과정에서 
    - 주문 하나의 전체 실적이 취소되거나 또는 일부 실적이 취소 될 수 있습니다.
    - 실시간 실적 전송시의 같은 주문번호로 새로운 마이너스 실적이 생길 수 있습니다.
    - 머천트 정산 방식에 따라 실시간 실적 전송시의 금액과 정산 이후의 금액이 달라질 수 있습니다.
    - 머천트 정산 날짜는 머천트에 따라 상이합니다.
    - 특히 여행 사이트의 경우에는 실시간 실적은 정산시 일단 전부 취소됩니다. 이후 체크아웃 날짜 기준으로 실제 정산이 되어 , 구매 후 1년 후에 정산이 될 수도 있습니다.



## 2. <a name="uid">u_id를 click과 연동하는 방법</a>

- u_id는 클릭링크에 u_id파라미터를 추가하여 전송 하실 수 있습니다.

- 예) u_id의 값이 exampleId101 일때

    ```html
    https://click.linkprice.com/click.php?m=tmon&a=A100000131&l=0000&u_id=exampleId101
    ```



## 3. <a name="rewardJoin">리워드 승인 신청</a>

- **AC > 어필리에이트 > 툴박스 > 리워드 API** 

- 리워드 승인 신청

    ![](https://raw.githubusercontent.com/linkprice/AffiliateSetup/master/reward_request.png)

- 실적 발생 시 머천트에서 링크프라이스로 실적을 보내주면, 링크프라이스에서 어필리에이트로 리워드 데이터를 전송합니다. 링크프라이스가 전송한 데이터를 받아 처리할 페이지를 개발해야 하며, 그 주소를 리워드 승인 후 리워드 API 받을 주소에 저장하셔야 합니다.

    ![](https://raw.githubusercontent.com/linkprice/AffiliateSetup/master/reward_url.png)

- 리워드를 받아 처리하는 페이지의 **타임아웃 시간은 최대 10초**입니다.




## 4. 리워드 전송 데이터
- 리워드 API를 통해 데이터를 받기 위해서는 스크립트 (ASP, PHP, JSP, CGI 등)을 작성하여 리워드 API 받을 주소에 기재 합니다.
- 링크프라이스에서 실적이 발생되는 시점에 리워드 API 받을 주소로 실적을 전송합니다.
- 실적 데이터는 POST방식으로 전송되며 데이터 형식은 JSON 입니다.(server to server 방식)

|     파라미터 값      |  타입   | 길이 | 설명                                                         |
| :------------------: | :-----: | :--: | :----------------------------------------------------------- |
|         day          | VARCHAR |  8   | 실적발생 날짜                                                |
|         time         | VARCHAR |  6   | 실적발생 시간                                                |
|     merchant_id      | VARCHAR |  10  | 머천트 ID                                                    |
|      order_code      | VARCHAR | 100  | 주문 코드                                                    |
|     product_code     | VARCHAR | 100  | 제품 코드                                                    |
|     product_name     | VARCHAR | 300  | 제품명<br />* 해당 값의 캐릭터셋은 UTF-8이고 URL ENCODING 처리를 합니다. |
|    category_code     | VARCHAR | 200  | 카테고리 코드                                                |
|      item_count      |   INT   |  11  | 개수                                                         |
|        price         |  FLOAT  |  -   | 실적 총 금액                                                 |
|      commision       |  FLOAT  |  -   | 커미션                                                       |
|     affiliate_id     | VARCHAR |  10  | 링크프라이스 어필레이트 아이디                               |
|  affiliate_user_id   | VARCHAR | 560  | 리워드 아이디<br />* click.linkprice.com 유입 URL의 "u_id" 값을 전송합니다. |
|       trlog_id       |   INT   |  11  | 실적 ID                                                      |
|   base_commission    | VARCHAR |  20  | 기본 커미션. 커미션의 형태에 따라 % 혹은 KRW(원화)로 전송합니다. |
| incentive_commission | VARCHAR |  20  | 인센티브 커미션. 추가적으로 지급받는 커미션을 의미합니다.<br /> 커미션의 형태에 따라 % 혹은 KRW(원화)로 전송합니다. |

###### 실적 발생시 전송되는 리워드 데이터 예
```json
POST
{
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
    "trlog_id" : 1000232321232,
    "base_commission" : "8%",
    "incentive_commission" : "500KRW"
}
```



## 5. 리워드 조회

- **AC > 어필리에이트 > 툴박스 > 리워드 API** 하단 로그정보 조회 클릭

    ![reward1](https://raw.githubusercontent.com/linkprice/AffiliateSetup/master/reward1.png)

- 로그조회 상단 필터링 부분을 이용하여 원하는 조건으로 조회

    ![reward2](https://raw.githubusercontent.com/linkprice/AffiliateSetup/master/reward2.png)

- 전송이 실패한 건에 대해서는 재전송이 가능합니다.
    (재전송 시 실적이 중복 될수 있습니다.)
