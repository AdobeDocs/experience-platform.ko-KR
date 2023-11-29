---
keywords: Experience Platform;쿼리 서비스;쿼리 서비스;중첩된 데이터 구조;중첩된 데이터;
title: 쿼리 서비스에서 중첩 데이터 구조 작업
description: 이 문서에서는 CTAS 및 INSERT INTO 문을 사용하여 중첩된 데이터 필드를 처리하고 변환하는 작업 예제를 제공합니다.
exl-id: 593379fb-88ad-4b14-8d2e-aa6d18129974
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 2%

---

# 쿼리 서비스에서 중첩 데이터 구조 작업

Adobe Experience Platform 쿼리 서비스는 중첩 데이터 필드의 사용을 지원합니다. 엔터프라이즈 데이터 구조가 복잡하면 이 데이터의 변환이나 처리가 복잡해질 수 있습니다. 이 문서에서는 중첩된 데이터 구조를 비롯한 복잡한 데이터 유형을 사용하여 데이터 세트를 만들거나, 처리하거나, 변형하는 방법에 대한 예를 제공합니다.

쿼리 서비스에서 다음을 제공합니다 [!DNL PostgreSQL] Experience Platform에서 관리하는 모든 데이터 세트에서 SQL 쿼리를 실행하는 인터페이스입니다. Platform은 구조체, 배열, 맵 및 깊게 중첩된 구조체, 배열 및 맵과 같은 테이블 열에서 기본 데이터 유형 또는 복잡한 데이터 유형을 사용할 수 있도록 지원합니다. 또한 데이터 세트에는 열 데이터 유형이 중첩된 구조의 배열만큼 복잡할 수 있는 중첩된 구조나 키-값 쌍의 값이 여러 수준의 중첩을 갖는 구조일 수 있는 맵 맵이 포함될 수 있습니다.

## 시작하기

이 자습서에서는 서드파티 PSQL 클라이언트 또는 쿼리 편집기 도구를 사용하여 Experience Platform UI(사용자 인터페이스) 내에서 쿼리를 작성, 유효성 검사 및 실행해야 합니다. UI를 통해 쿼리를 실행하는 방법에 대한 자세한 내용은 [쿼리 편집기 UI 안내서](../ui/user-guide.md). Query Service에 연결할 수 있는 타사 데스크탑 클라이언트에 대한 자세한 목록은 다음을 참조하십시오. [클라이언트 연결 개요](../clients/overview.md).

또한 다음을 잘 이해해야 합니다. `INSERT INTO` 및 `CTAS` 구문. 사용 방법에 대한 자세한 내용은 [`INSERT INTO`](../sql/syntax.md#insert-into) 및 [`CTAS`](../sql/syntax.md#create-table-as-select) 의 섹션 [SQL 구문 참조 설명서](../sql/syntax.md).

## 데이터 세트 만들기

쿼리 서비스에서는 선택 항목으로 테이블 만들기(`CTAS`) 의 출력을 기반으로 테이블을 만드는 기능입니다. `SELECT` 문 또는 이 경우처럼 Adobe Experience Platform의 기존 XDM 스키마에 대한 참조를 사용하는 방법. 아래에 의 XDM 스키마가 표시됩니다. `Final_subscription` 이 예제를 위해 만들어졌습니다.

![final_subscription 스키마의 다이어그램입니다.](../images/best-practices/final-subscription-schema.png)

다음 예제에서는 SQL을 사용하여 `final_subscription_test2` 데이터 세트. `final_subscription_test2` 다음을 사용하여 생성됨 `Final_subscription` 스키마. 데이터를 소스에서 추출 `SELECT` 조항을 사용하여 일부 행을 채울 수 있습니다.

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

초기 데이터 세트에서 `final_subscription_test2`, 구조 데이터 형식은 를 모두 포함하는 데 사용됩니다. `subscription` 필드 및 `userid` 각 사용자에 대해 고유합니다. 다음 `subscription` 필드는 사용자에 대한 제품 구독을 설명합니다. 여러 구독이 있을 수 있지만 테이블에는 행당 하나의 구독에 대한 정보만 포함될 수 있습니다.

## INSERT INTO를 사용하여 중첩된 데이터 필드 업데이트

다음 이후 `final_subscription_test2` 데이터 세트가 생성되었습니다. `INSERT INTO` 문은 테이블에 추가 데이터를 추가하는 데 사용됩니다. 데이터를 복사할 때에는 소스와 타겟의 데이터 유형이 일치해야 합니다. 또는 소스 데이터 유형은 다음과 같아야 합니다. `CAST` 대상 데이터 형식에 매핑할 수도 있습니다. 그런 다음 증분 데이터가 다음 SQL을 사용하여 대상 데이터 세트에 추가됩니다.

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

## 중첩 데이터 세트의 데이터 처리

데이터 세트에서 사용자의 활성 구독 목록을 확인하려면 배열의 요소를 여러 행과 열로 구분하는 쿼리를 작성해야 합니다. 이렇게 하려면 먼저 구독 정보가 데이터 세트 내에 중첩된 배열 내에 유지되므로 데이터 모델의 모양을 이해해야 합니다.

PSQL `\d` 명령은 수준별로 필요한 구독 데이터로 탐색하는 데 사용됩니다. 이 표에서는 의 구조를 보여 줍니다. `final_subscription_test2` 데이터 세트. 복잡한 데이터 유형은 텍스트, 부울, 타임스탬프 등과 같은 일반적인 유형 값이 아니므로 한 눈에 알아볼 수 있습니다.

| 열 | 유형 |
|--------|-------|
| `_lumaservices3` | final_subscription_test2__lumaservices3 |

다음 열의 필드는 `\d final_subscription_test2__lumaservices3` 명령입니다.

| 열 | 유형 |
|---------|-------|
| `userid` | 텍스트 |
| `subscription` | _lumaservices3_subscription_e[] |

`subscription` 는 구조체 요소의 배열입니다. 해당 필드는 다음을 사용하여 표시됩니다. `\d _lumaservices3_subscription_e[]` 명령입니다.

| 열 | 유형 |
|---------|-------|
| `last_eventtime` | 타임스탬프 |
| `last_status` | 텍스트 |
| `offer_id` | 텍스트 |
| `subscription_id` | 텍스트 |

구독의 중첩된 필드를 쿼리하려면 먼저 의 요소를 분리해야 합니다. `subscription` 여러 행으로 정렬하고 분해 함수를 사용하여 결과를 반환합니다. 다음 SQL 예제는 다음을 기반으로 사용자의 활성 구독을 반환합니다. `userid`.

```sql
SELECT userid, subs AS active_subscription FROM (
    SELECT _lumaservices3.userid AS userid, explode(_lumaservices3.subscription) AS subs 
    FROM final_subscription_test2
)
WHERE subs.last_status='Active';
```

간소화된 이 예제 솔루션에서는 하나의 활성 사용자 구독만 허용합니다. 현실적으로, 단일 사용자에 대한 많은 활성 구독이 있을 수 있다. 다음 예제에서는 여러 개의 동시 활성 구독을 허용하도록 이전 쿼리를 수정합니다.

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

이 SQL 예제의 복잡성이 증가하고 있지만 `collect_list` 활성 구독의 경우 출력이 소스와 동일한 순서로 유지될 수 없습니다. 사용자에 대한 활성 구독 목록을 만들려면 GROUP BY 또는 셔플링을 사용하여 목록의 결과를 집계해야 합니다.

## 다음 단계

이제 이 문서를 읽고 Adobe Experience Platform Query Service에서 복잡한 데이터 유형을 사용하는 데이터 세트를 처리하거나 변환하는 방법을 이해합니다. 다음을 참조하십시오. [쿼리 실행 지침](../best-practices/writing-queries.md) 데이터 레이크 내의 데이터 세트에서 SQL 쿼리를 실행하는 방법에 대한 자세한 정보.
