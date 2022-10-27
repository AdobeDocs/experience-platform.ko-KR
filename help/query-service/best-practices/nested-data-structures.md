---
keywords: Experience Platform;쿼리 서비스;쿼리 서비스;중첩된 데이터 구조;중첩된 데이터;
title: Query Service에서 중첩된 데이터 구조 작업
description: 이 문서에서는 CTAS 및 INSERT INTO 문을 사용하여 중첩된 데이터 필드를 처리하고 변형하는 작업 예를 제공합니다.
exl-id: 593379fb-88ad-4b14-8d2e-aa6d18129974
source-git-commit: 9c450f340706040593dfea5292702c4b00dd9852
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 1%

---

# Query Service에서 중첩된 데이터 구조 작업

Adobe Experience Platform 쿼리 서비스는 중첩된 데이터 필드 사용을 지원합니다. 엔터프라이즈 데이터 구조의 복잡성으로 인해 이러한 데이터를 변환하거나 처리할 수 있습니다. 이 문서에서는 중첩 데이터 구조를 포함하여 복잡한 데이터 유형을 사용하여 데이터 세트를 생성, 처리 또는 변환하는 방법에 대한 예를 제공합니다.

쿼리 서비스에서는 [!DNL PostgreSQL] Experience Platform에서 관리하는 모든 데이터 세트에 대해 SQL 쿼리를 실행하는 인터페이스. 플랫폼은 구조체, 배열, 맵, 깊이 중첩된 구조체, 배열 및 맵과 같은 테이블 열에 기본 또는 복잡한 데이터 형식을 사용할 수 있도록 지원합니다. 또한 데이터 세트에는 열 데이터 유형이 중첩된 구조의 배열처럼 복잡할 수 있는 중첩 구조나 키-값 쌍의 값이 여러 중첩 수준이 있는 구조가 될 수 있는 맵 맵을 포함할 수 있습니다.

## 시작하기

이 자습서에서는 UI(Experience Platform 사용자 인터페이스) 내에서 쿼리를 작성, 유효성 검사 및 실행하려면 타사 PSQL 클라이언트나 쿼리 편집기 도구를 사용해야 합니다. UI를 통해 쿼리를 실행하는 방법에 대한 자세한 내용은 [쿼리 편집기 UI 안내서](../ui/user-guide.md). Query Service에 연결할 수 있는 타사 데스크탑 클라이언트가 자세히 필요하면 [클라이언트 연결 개요](../clients/overview.md).

또한 Adobe Analytics Mobile Apps의 `INSERT INTO` 및 `CTAS` 구문 사용 방법에 대한 특정 정보는 [`INSERT INTO`](../sql/syntax.md#insert-into) 및 [`CTAS`](../sql/syntax.md#create-table-as-select) 의 섹션 [SQL 구문 참조 설명서](../sql/syntax.md).

## 데이터 집합 만들기

쿼리 서비스는 테이블을 선택하여 만들기(`CTAS`) 기능을 사용하여 `SELECT` 또는 이 경우처럼 Adobe Experience Platform의 기존 XDM 스키마에 대한 참조를 사용하여 바꿉니다. 아래에 표시되는 XDM 스키마는 `Final_subscription` 이 예제에 대해 작성되었습니다.

![final_subscription 스키마의 다이어그램입니다.](../images/best-practices/final-subscription-schema.png)

다음 예제에서는 `final_subscription_test2` 데이터 세트. `final_subscription_test2` 는 `Final_subscription` 스키마. 데이터는 `SELECT` 일부 행을 채울 절

```sql
CREATE TABLE final_subscription_test2 with(schema='Final_subscription') AS (
        SELECT struct(userid, collect_set(subscription) AS subscription) AS _lumaservices3 FROM(
            SELECT user AS userid,
                   struct( last(eventtime) AS last_eventtime,
                           last(status) AS last_status,
                           offer_id, 
                           subsid AS subscription_id)
                   AS subscription
             FROM (
                   SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , TIMESTAMP eventtime
 
                   FROM
                        xbox_subscription_event
                   UNION   
                   SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , TIMESTAMP eventtime
                   FROM
                        office365_subscription_event
             ) 
             GROUP BY user,subsid,offer_id
             ORDER BY user ASC
       ) GROUP BY userid)
```

초기 데이터 세트에서 `final_subscription_test2`구조체 데이터 형식은 `subscription` 필드 및 `userid` 각 사용자에게 고유한 ID. 다음 `subscription` 필드는 사용자의 제품 가입에 대해 설명합니다. 여러 개의 구독이 있을 수 있지만 테이블에는 행당 하나의 구독에 대한 정보만 포함될 수 있습니다.

## 삽입 을 사용하여 중첩된 데이터 필드를 업데이트합니다

다음 이후 `final_subscription_test2` 데이터 세트가 생성되었습니다. `INSERT INTO` 문은 테이블에 추가 데이터를 추가하는 데 사용됩니다. 데이터를 복사할 때 소스와 타겟의 데이터 유형이 일치해야 합니다. 또는 소스 데이터 유형은 `CAST` 대상 데이터 유형에 추가합니다. 그런 다음 다음 다음 SQL을 사용하여 증분 데이터가 타겟 데이터 세트에 추가됩니다.

```sql
INSERT INTO final_subscription_test
      SELECT struct(userid, collect_set(subscription) AS subscription) AS _lumaservices3 FROM(
            SELECT user AS userid,
                   struct( last(eventtime) AS last_eventtime,
                           last(status) AS last_status,
                           offer_id, 
                           subsid AS subscription_id)
                   AS subscription
             FROM  SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , TIMESTAMP eventtime
 
                   FROM
                        xbox_subscription_event
                   UNION   
                   SELECT _lumaservices3.msftidentities.userid user
                        , _lumaservices3.subscription.subscription_id subsid
                        , _lumaservices3.subscription.subscription_status status
                        , _lumaservices3.subscription.offer_id offer_id
                        , timestamp eventtime
                   FROM
                        office365_subscription_event
             ) 
             GROUP BY user,subsid,offer_id
             ORDER BY user ASC
       ) GROUP BY userid)
```

## 중첩된 데이터 세트에서 데이터 처리

데이터 집합에서 사용자의 활성 구독 목록을 찾으려면 배열 요소를 여러 행 및 열로 구분하는 쿼리를 작성해야 합니다. 이렇게 하려면 먼저 구독 정보가 데이터 세트 내에 중첩된 배열 내에 유지되므로 데이터 모델의 모양을 이해해야 합니다.

PSQL `\d` 명령은 필요한 구독 데이터로 레벨별로 탐색하는 데 사용됩니다. 표는 `final_subscription_test2` 데이터 세트. 복잡한 데이터 유형은 텍스트, 부울, 타임스탬프 등과 같은 일반적인 유형 값이 아니므로 한 눈에 인식할 수 있습니다.

| 열 | 유형 |
|--------|-------|
| `_lumaservices3` | final_subscription_test2__lumaservices3 |

다음 열의 필드는 `\d final_subscription_test2__lumaservices3` 명령.

| 열 | 유형 |
|---------|-------|
| `userid` | text |
| `subscription` | _lumaservices3_subscription_e[] |

`subscription` 는 구조체 요소의 배열입니다. 해당 필드는 `\d _lumaservices3_subscription_e[]` 명령.

| 열 | 유형 |
|---------|-------|
| `last_eventtime` | timestamp |
| `last_status` | 텍스트 |
| `offer_id` | 텍스트 |
| `subscription_id` | 텍스트 |

구독의 중첩된 필드를 쿼리하려면 먼저 `subscription` 배열을 여러 행으로 나누고 분해 함수를 사용하여 결과를 반환합니다. 다음 SQL 예는 사용자를 기반으로 한 활성 가입을 반환합니다 `userid`.

```sql
SELECT userid, subs AS active_subscription FROM (
    SELECT _lumaservices3.userid AS userid, explode(_lumaservices3.subscription) AS subs 
    FROM final_subscription_test2
)
WHERE subs.last_status='Active';
```

이 간소화된 예제 솔루션은 하나의 활성 사용자 구독만 허용합니다. 현실적으로, 단일 사용자에 대해 여러 가지 활성 구독이 있을 수 있습니다. 다음 예에서는 여러 개의 동시 활성 가입을 허용하도록 이전 쿼리를 수정합니다.

```sql
SELECT userid, collect_list(subs) AS active_subscriptions FROM (
     SELECT
          _lumaservices3.userid AS userid,
          explode(_lumaservices3.subscription) AS subs
     FROM final_subscription_test2
     )
WHERE subs.last_status='Active' 
GROUP BY userid ;
```

이 SQL 예제의 복잡성이 높아지면서도 `collect_list` 활성 구독의 경우 출처가 소스와 동일한 순서로 지정되는지 보장하지 않습니다. 사용자에 대한 활성 구독 목록을 만들려면 GROUP BY 또는 섞어서 목록의 결과를 집계해야 합니다.

## 다음 단계

이 문서를 읽은 후에는 Adobe Experience Platform Query Service에서 복잡한 데이터 유형을 사용하는 데이터 세트를 처리하거나 변환하는 방법을 이해할 수 있습니다. 자세한 내용은 [쿼리 실행 지침](./writing-queries.md) data Lake 내 데이터 세트에서 SQL 쿼리 실행에 대한 자세한 정보.
