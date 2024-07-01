# 리워드 API

## 1. 리워드 이용방법
1. **Affiliate Center > 어필리에이트 > 툴박스 > 리워드 API**에서 승인 신청을 한 뒤, 링크프라이스에서 승인하면 사용이 가능합니다.
   ![](https://raw.githubusercontent.com/linkprice/AffiliateSetup/master/reward_request.png)
  

2. **같은 메뉴 하단**에 리워드 데이터를 수신 받을 주소가 입력되면, 실적 발생시 해당 주소로 리워드 데이터를 전송해드립니다.  
   ![](https://raw.githubusercontent.com/linkprice/AffiliateSetup/master/reward_url.png)  
    ※ 리워드를 받아 처리하는 페이지의 **타임아웃 시간은 최대 10초**입니다.  


3. 리워드 데이터를 받았을 때 회원을 식별하기 위해 제휴링크에 회원 식별 값(u_id)를 추가해야 합니다.
   - 최대 500byte까지 전달 가능합니다.
   - 반드시 URL ENCODING 해야 합니다.
   - 예) 회원 식별 값(u_id)이 'exampleId101' 일 때
     ```html
         https://click.linkprice.com/click.php?m=gmarket&a=A100000131&l=0000&u_id=exampleId101
     ```
## 2. 리워드 전송 데이터
- 실적 데이터는 POST방식으로 전송되며 데이터 형식은 JSON 입니다.(server to server 방식)

|     파라미터 값      |   타입    | 길이  | 설명                                                         |
| :------------------: |:-------:|:---:|:-----------------------------------------------------------|
|         day          | VARCHAR |  8  | 실적발생 날짜(YYYYMMDD)                                          |
|         time         | VARCHAR |  6  | 실적발생 시간(hhmmss)                                            |
|     merchant_id      | VARCHAR | 10  | 머천트 ID                                                     |
|      order_code      | VARCHAR | 100 | 주문 코드                                                      |
|     product_code     | VARCHAR | 100 | 제품 코드                                                      |
|     product_name     | VARCHAR | 300 | 제품명<br />* 해당 값의 캐릭터셋은 UTF-8이고 URL ENCODING 처리를 합니다.       |
|    category_code     | VARCHAR | 200 | 카테고리 코드                                                    |
|      item_count      |   INT   | 11  | 개수                                                         |
|        price         |  FLOAT  |  -  | 실적 총 금액(KRW)                                               |
|      commision       |   INT   | 11  | 커미션 금액(KRW)                                                |
|     affiliate_id     | VARCHAR | 10  | 링크프라이스 어필레이트 아이디                                           |
|  affiliate_user_id   | VARCHAR | 560 | 어필리에이트 회원 식별값, 어필리에이트에서 제휴링크를 통해 전달한 u_id 값입니다.            |
|       trlog_id       |   INT   | 14  | 실적 ID                                                      |
|   base_commission    | VARCHAR | 20  | 기본 커미션에 대한 계산 기준. 실적 총금액 비율(%) 또는 개수당 지급되는 금액(KRW) 입니다.    |
| incentive_commission | VARCHAR | 20  | 추가 지급 커미션에 대한 계산 기준. 실적 총금액 비율(%) 또는 개수당 지급되는 금액(KRW) 입니다. |

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
    "trlog_id" : 10000536080255,
    "base_commission" : "8%",
    "incentive_commission" : "500KRW"
}
```



## 3. 리워드 전송 조회 및 재전송
- **Affiliate Center > 어필리에이트 > 툴박스 > 리워드 API**, 하단 로그정보 조회 버튼을 통해 로그 조회 화면으로 이동 가능합니다.
- 로그조회 상단 필터링 부분을 이용하여 원하는 조건으로 조회할 수 있습니다.
- 리워드 데이터 전송 내역을 확인할 수 있으며, 전송 실패건에 대해 재전송 할 수 있습니다. ※ 재전송 시 실적이 중복 될수 있습니다.
    ![reward1](https://raw.githubusercontent.com/linkprice/AffiliateSetup/master/reward1.png)
    ![reward2](https://raw.githubusercontent.com/linkprice/AffiliateSetup/master/reward2.png)