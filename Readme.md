# 리워드 연동

## 리워드의 개요

> 실적 발생 시 어떤 회원의 실적인지 실시간으로 데이터를 받을 수 있습니다.
> 리워드 데이터를 사용하면 회원들에게 가입/구매를 홍보하고, 실적이 발생하면 해당 회원에게 보상해 줄 수 있기 때문에 캐시백 또는 리워드 서비스를 운영하는 어필리에이트에 적합합니다.

## 리워드 주의사항

- 링크프라이스로부터 허가를 받아 사용 가능(어필팀과 절차 논의 필요)
- 어필쪽 개발팀(개발자는 퇴사하면 연락이 안됨) 연락처 관리 필요(어필팀과 절차 논의 필요)
- u_id
    - 리워드를 받을 회원의 ID입니다.
    - 클릭링크에 u_id파라미터를 같이 전송합니다.
    - **길이제한: 50byte**
- 리워드 실적 받기
    - 모든 머천트가 실시간 실적 전송을 지원하지 않습니다.
    - 머천트에 따라 4시간 마다 1번씩 전송하기도 합니다.
    - 머천트에 따라 실시간 금액은 0으로 전송되고 익일 실제 금액이 전송되기도 합니다.
    - timeout: 10초
- 하나의 주문은 링크프라이스를 통해 리워드를 받은 이후에, 정산 과정에서 
    - 주문 하나의 전체가 취소 될 수 있습니다.
    - 주문 하나의 일부 실적이 취소 될 수 있습니다.
    - 머천트 정산 날짜는 머천트에 따라 다소 다를 수 있으며, 특히 여행 사이트의 경우에는 체크아웃 날짜 기준으로 정산이 되어, 구매 후 2년 후에 정산이 될 수도 있습니다.
    - 머천트 정산 방식에 따라 같은 주문번호와 특정 상품번호로 새로운 마이너스 실적이 생길 수 있습니다.
    - 머천트 정산 방식에 따라 주문시의 금액과 달라질 수 있습니다.

## 용어 설명

- PK(기본키)
  - trlog_id: 주문마다 링크프라이스에서 부여하는 ID
  - 하나의 주문은 하나의 trlog_id가 부여됩니다. 즉 한번에 여러개의 주문이 있을 경우, 주문마다 trlog_id가 부여됩니다.
- AK(대체키)
  - 리워드 데이타 중 merchant_id, order_code, product_code 조합으로 trlog_id를 대체 하실 수 있습니다. 

## u_id를 click과 연동하는 방법

- u_id는 클릭링크에 u_id파라미터를 추가하여 전송 하실 수 있습니다.

- 예) u_id의 값이 exampleId101 일때

    ```html
    https://click.linkprice.com/click.php?m=tmon&a=A100000131&l=0000&u_id=exampleId101
    ```

## 리워드 실적 조회하기

- AC센터 > 툴박스 > 리워드 API

- 하단 로그정보 조회 클릭

    ![reward1](C:\Users\Linkprice\Pictures\reward1.png)

- 상단 필터링 부분을 이용하여 원하는 조건으로 조회

    ![reward2](C:\Users\Linkprice\Pictures\reward2.png)

- 전송이 실패한 건에 대해서는 재전송이 가능합니다.
    (재전송 시 실적이 중복 될수 있습니다.)

## 실적 조회 API 사용법

> 귀사에서 발생한 링크프라이스의 실시간/확정/취소 실적을 확인 할 수 있는 API입니다.

* 실적 조회 API를 사용하기 위한 auth_key(인증키)를 발급 받습니다.
  
* 인증키 발급을 위해서는 링크프라이스로 연락 주십시요.
  
* 조회 

  * Request

  ```http
  GET /affiliate/translist.php?a_id=[어필아이디]&auth_key=[인증키]&yyyymmdd=[조회일자] HTTP/1.1
  Host: api.linkprice.com
  ```

* 파라미터 설명

| 파라미터    | 필수 여부 | 설명                                                         |
| ----------- | --------- | ------------------------------------------------------------ |
| auth_key    | 필수      | 링크프라이스에 가입된 어필리에이트 아이디                    |
| a_id        | 필수      | 링크프라이스가 발행한 인증키값                               |
| yyyymmdd    | 필수      | 조회일자<br/>ex) 20150515 또는 201505 (실적취소 조회 시에만 가능함) |
| cancel_flag | 옵션      | 취소주문 조회<br/>Y: 취소 실적 조회                          |
| currency    | 옵션      | 화폐 명시 (판매금액 및 커미션이 환율 적용됨)<br/>ISO 4217 사용 |
| cmd         | 옵션      | 부가 명령어<br/>total: 전체 실적 조회<br/>addon: 조회월 이후에 생성된 추가 실적 조회 |
| merchant_id | 옵션      | 해당 머천트 ID 의 실적만 조회                                |
| page        | 옵션      | 페이지 번호 (Paging 처리)                                    |
| per_page    | 옵션      | 페이지당 몇 건의 정보를 취득할 것인지 지정 (Paging 처리)     |

* curl 요청

```bash
// 실적조회
curl https://api.linkprice.com/affiliate/translist.php?a_id=yourAffiliateId&auth_key=yourAuthKeyIsHere&yyyymmdd=20190701
  
// 취소 주문조회
curl http://api.linkprice.com/affiliate/translist.php?a_id=yourAffiliateId&auth_key=yourAuthKeyIsHere&yyyymmdd=20190712&cancel_flag=Y
  
// 일별 전체실적 건수 조회
curl http://api.linkprice.com/affiliate/translist.php?a_id=yourAffiliateId&auth_key=yourAuthKeyIsHere&yyyymmdd=20190702&cmd=total
```

* 응답
  * 형식: JSON
  * Response

 ```http
  HTTP1.1 200 OK
  Content-Type: application/json; charset=utf-8
  {
  	"result":result,
  	"list_count": count,
  	"order_list":items
  }
  
 ```

  * JSON 데이터 설명

| 키         | 값                                                           |
| ---------- | ------------------------------------------------------------ |
| result     | 응답코드<br/>0: 조회 성공<br/>100: 어필 아이디 없음<br/>200: 조회일자 없음<br/>300: 인증키가 맞지 않음 |
| list_count | 조회 갯수(있을 경우)                                         |
| order_list | 조회 목록(있을 경우)                                         |

  * order_list 상세 명세

| 키            | 값                                                           |
| ------------- | ------------------------------------------------------------ |
| trlog_id      | 주문 고유번호(PK)                                            |
| yyyymmdd      | 주문 일자                                                    |
| hhmiss        | 주문 시간                                                    |
| m_id          | 머천트 아이디(AK)                                            |
| o_cd          | 주문 번호(AK)                                                |
| p_cd          | 상품 코드(AK)                                                |
| p_nm          | 상품명                                                       |
| c_cd          | 카테고리 코드                                                |
| it_cnt        | 주문 수량                                                    |
| sales         | 판매 합계금액                                                |
| commission    | 어필 커미션                                                  |
| user_id       | 매체 사용자 정보<br/>(click 주소를 통해 u_id로 전달 된 값)   |
| membership_id | 머천트의 주문자 정보                                         |
| remote_addr   | 사용자 PC 주소                                               |
| status        | 100 (일반) <br/>300(취소신청) <br/>310(취소완료) /<br/>200(정산대기)<br/>210(정산완료 MER) <br/>220(정산완료 AFF) |
| trans_comment | 실적 취소 사유(값이 있을 경우에만)                           |

