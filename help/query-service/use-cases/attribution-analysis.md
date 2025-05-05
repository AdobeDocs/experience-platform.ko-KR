---
title: 속성 분석
description: 이 문서에서는 쿼리 서비스를 사용하여 첫 번째 및 마지막 터치의 마케팅 속성 모델을 기반으로 마케팅 효율성 측정 기법을 만드는 방법을 설명합니다.
exl-id: d62cd349-06fc-4ce6-a5e8-978f11186927
source-git-commit: e33d59c4ac28f55ba6ae2fc073d02f8738159263
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 0%

---

# 속성 분석

기여도 분석은 채널, 오퍼 및 메시지와 같은 비즈니스 판매 또는 전환에 기여하는 마케팅 전략을 결정하는 데 도움이 되는 분석 개념입니다. 이 개념은 고객 접점(소비자가 브랜드와 상호 작용할 때마다)을 기반으로 구매 또는 획득을 초래하는 소비자 여정(고객이 목표를 달성하기 위해 회사와 상호 작용하는 프로세스)을 평가합니다. 마케터는 속성 분석을 통해 잠재 고객과 연결하는 채널의 투자 수익을 평가할 수 있습니다.

## 시작하기

이 문서 전체의 SQL 예제는 Adobe Analytics 데이터에 일반적으로 사용되는 쿼리입니다. 이 자습서에서는 다음 구성 요소를 이해하고 있어야 합니다.

* [보고서 세트 데이터 개요용 Adobe Analytics 소스 커넥터](../../sources/connectors/adobe-applications/mapping/analytics.md).
* [Analytics 필드 매핑 설명서](../../sources/connectors/adobe-applications/mapping/analytics.md)에서 쿼리 서비스에 사용할 분석 데이터를 수집 및 매핑하는 방법에 대한 자세한 정보를 제공합니다.
* [Attribution IQ 개요](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html?lang=ko)
* [Adobe Analytics 속성 패널 안내서](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/attribution.html?lang=ko).

`OVER()` 함수 내의 매개 변수에 대한 설명은 [window 함수 섹션](../sql/adobe-defined-functions.md#window-functions)에 있습니다. [Adobe 마케팅 및 Commerce 용어 용어집](https://business.adobe.com/glossary/index.html)도 사용할 수 있습니다.

다음 각 사용 사례에 대해 사용자 정의할 템플릿으로 매개 변수가 있는 SQL 쿼리 예제가 제공됩니다. 평가하려는 SQL 예제에 `{ }`이(가) 표시되는 모든 위치에 매개 변수를 제공합니다.

## 목표

속성 사용 사례는 Adobe Analytics 데이터를 사용하여 고객 작업을 성공적인 결과에 연결하는 데 도움이 됩니다. 이러한 연관성은 고객 경험에 영향을 미치는 요인을 이해하는 데 중요한 부분입니다. 속성 분석 데이터를 사용하여 고객 여정 중에 고객의 터치 포인트의 중요성을 이해할 수 있습니다.

이 문서에 포함된 쿼리 예제는 다양한 만료 설정을 사용하는 첫 번째 터치 및 마지막 터치 속성에 대한 다양한 사용 사례를 지원합니다. 이 안내서에서는 다음 주요 개념을 설명합니다.

* 첫 번째 터치 및 마지막 터치 속성.
* 만료 시간 제한이 있는 첫 번째 터치 및 마지막 터치 속성.
* 만료 조건이 있는 첫 번째 터치 및 마지막 터치 속성.

## 속성 쿼리 매개 변수 {#attribution-query-parameters}

아래 표는 첫 번째 터치 및 마지막 터치 속성 쿼리에 사용되는 매개 변수의 분류 및 설명을 제공합니다.

| 매개변수 | 설명 |
|---|---|
| `{TIMESTAMP}` | 데이터 세트에 있는 타임스탬프 필드입니다. |
| `{CHANNEL_NAME}` | 반환된 개체의 레이블입니다. |
| `{CHANNEL_VALUE}` | 쿼리의 대상 채널인 열 또는 필드입니다. |
| `{EXP_TIMEOUT}` | 쿼리가 첫 번째 터치 이벤트를 검색하는 채널 이벤트까지 남은 시간(초)입니다. |
| `{EXP_CONDITION}` | 채널의 만료 지점을 결정하는 조건입니다. |
| `{EXP_BEFORE}` | 지정된 조건 `{EXP_CONDITION}`이(가) 충족되기 전이나 후에 채널이 만료되는지 여부를 나타내는 부울입니다. 이 기능은 주로 세션의 만료 조건에 대해 활성화되어 이전 세션에서 첫 번째 터치가 선택되지 않도록 합니다. 기본적으로 이 값은 `false`(으)로 설정됩니다. |

## 쿼리 결과 열 구성 요소 {#query-result-column-components}

속성 쿼리의 결과는 `first_touch` 또는 `last_touch` 열에 제공됩니다. 이러한 열은 다음 구성 요소로 구성됩니다.

```console
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `{NAME}` | Azure Data Factory(ADF)에 레이블로 입력한 `{CHANNEL_NAME}`입니다. |
| `{VALUE}` | 지정된 `{EXP_TIMEOUT}` 간격 내의 마지막 터치인 `{CHANNEL_VALUE}`의 값 |
| `{TIMESTAMP}` | 마지막 터치가 발생한 [!DNL Experience Event]의 타임스탬프 |
| `{FRACTION}` | 소수 값으로 표현되는 마지막 터치 속성입니다. |

### 첫 번째 터치 속성 {#first-touch}

첫 번째 터치 속성은 소비자가 접한 초기 채널에 대한 성공적인 결과에 대한 책임을 100% 승인합니다. 이 SQL 예제는 후속 고객 작업을 유도한 상호 작용을 강조 표시하는 데 사용됩니다.

아래 쿼리는 첫 번째 터치 속성 값과 대상 [!DNL Experience Event] 데이터 집합에 있는 채널의 세부 정보를 반환합니다. 또한 각 행에 대해 첫 번째 터치 값, 타임스탬프 및 속성을 사용하여 선택한 채널에 대한 `struct` 개체를 반환합니다.

>[!NOTE]
>
>ECID(Experience Cloud ID)는 MCID라고도 하며 네임스페이스에서 계속 사용됩니다.

**쿼리 구문**

```sql
ATTRIBUTION_FIRST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

잠재적으로 필요한 매개 변수의 전체 목록 및 설명은 [속성 쿼리 매개 변수 섹션](#attribution-query-parameters)을 참조하세요.

**예제 쿼리**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_FIRST_TOUCH(timestamp, 'Paid First', marketing.trackingCode)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS first_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
LIMIT 10
```

**결과**

아래 결과에서는 [!DNL Experience Event] 데이터 집합에서 초기 추적 코드 `em:946426`을(를) 가져옵니다. 이 추적 코드는 첫 번째 상호 작용이었으므로 고객 작업에 대한 100%(`1.0`)의 책임으로 인한 것입니다.

```console
                 id                 |       timestamp       | trackingCode |                   first_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:06:12.0 | em:946426    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0) 
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:07:02.0 | em:946426    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0) 
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:07:55.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0) 
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-18 07:08:44.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0) 
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-23 17:50:10.0 | em:513526    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0) 
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-23 17:50:43.0 | em:513526    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0) 
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-23 17:53:02.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0) 
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-26 20:37:12.0 | sms:70175    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0) 
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-12-26 20:37:57.0 |              | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0) 
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2019-01-02 19:41:38.0 | em:526702    | (Paid First,em:946426,2018-12-18 07:06:12.0,1.0)
(10 rows)
```

`first_touch` 열에 표시된 결과를 분류하려면 [열 구성 요소 섹션](#query-result-column-components)을 참조하세요.

### 마지막 터치 속성 {#second-touch}

마지막 터치 속성은 소비자가 접한 마지막 채널에 대한 성공적인 결과에 대한 책임을 100% 승인합니다. 이 SQL 예는 일련의 고객 작업에서 최종 상호 작용을 강조 표시하는 데 사용됩니다.

쿼리가 마지막 터치 속성 값과 대상 [!DNL Experience Event] 데이터 집합에 있는 채널의 세부 정보를 반환합니다. 또한 각 행에 대한 마지막 터치 값, 타임스탬프 및 속성을 사용하여 선택한 채널에 대한 `struct` 개체를 반환합니다.

**쿼리 구문**

```sql
ATTRIBUTION_LAST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

**예제 쿼리**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_LAST_TOUCH(timestamp, 'trackingCode', marketing.trackingCode)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS last_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**결과**

아래에 표시된 결과에서 반환된 개체의 추적 코드는 각 [!DNL Experience Event] 레코드에서 마지막 상호 작용입니다. 각 코드는 마지막 상호 작용이었으므로 고객의 작업에 대한 100%(`1.0`) 책임에 연결됩니다.

```console
                 id                |       timestamp       | trackingCode |                   last_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:06:12.0 | em:946426    | (Paid Last,em:946426,2017-12-18 07:06:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:07:02.0 | em:946426    | (Paid Last,em:946426,2017-12-18 07:07:02.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:07:55.0 |              | (Paid Last,em:946426,2017-12-18 07:07:02.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-18 07:08:44.0 |              | (Paid Last,em:946426,2017-12-18 07:07:02.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-23 17:50:10.0 | em:513526    | (Paid Last,em:513526,2017-12-23 17:50:10.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-23 17:50:43.0 | em:513526    | (Paid Last,em:513526,2017-12-23 17:50:43.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-23 17:53:02.0 |              | (Paid Last,em:513526,2017-12-23 17:50:43.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-26 20:37:12.0 | sms:70175    | (Paid Last,sms:70175,2017-12-26 20:37:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2017-12-26 20:37:57.0 |              | (Paid Last,sms:70175,2017-12-26 20:37:12.0,1.0)
 5D9D1DFBCEEBADF6-4097750903CE64DB | 2018-01-02 19:41:38.0 | em:526702    | (Paid Last,em:526702,2018-01-02 19:41:38.0,1.0)
(10 rows)
```

`last_touch` 열에 표시된 결과를 분류하려면 [열 구성 요소 섹션](#query-result-column-components)을 참조하세요.

### 만료 조건이 있는 첫 번째 터치 속성 {#first-touch-attribution-with-expiration-condition}

이 쿼리는 선택 조건에 따라 결정된 [!DNL Experience Event] 데이터 집합의 일부 내에서 일련의 고객 작업을 유도한 상호 작용을 확인하는 데 사용됩니다.

쿼리는 조건 후 또는 이전에 만료되는 대상 [!DNL Experience Event] 데이터 집합의 단일 채널에 대한 첫 번째 터치 속성 값과 세부 정보를 반환합니다. 또한 선택한 채널에 대해 반환된 각 행에 대해 첫 번째 터치 값, 타임스탬프 및 속성이 있는 `struct` 개체도 반환합니다.

**쿼리 구문**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE})
    OVER ({PARTITION} {ORDER} {FRAME})
```

잠재적으로 필요한 매개 변수의 전체 목록 및 설명은 [속성 쿼리 매개 변수 섹션](#attribution-query-parameters)을 참조하세요.

**예제 쿼리**

아래 예에서는 결과에 표시된 4일(7월 15일, 21일, 23일 및 29일) 각각에 구매가 기록(`commerce.purchases.value IS NOT NULL`)되고 각 날의 초기 추적 코드는 고객 작업에 대한 100%(`1.0`) 책임으로 연결됩니다.

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_FIRST_TOUCH_EXP_IF(timestamp, 'Paid First', marketing.trackingCode, commerce.purchases.value IS NOT NULL, false)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS first_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**결과**

```console
                 id               |       timestamp       | trackingCode |                   first_touch                   
----------------------------------+-----------------------+--------------+-------------------------------------------------
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:05.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid First,em:70558,2019-07-23 12:25:12.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 |              | (Paid First,em:70558,2019-07-23 12:25:12.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid First,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

`first_touch` 열에 표시된 결과를 분류하려면 [열 구성 요소 섹션](#query-result-column-components)을 참조하세요.

### 만료 시간 제한이 있는 첫 번째 터치 속성 {#first-touch-attribution-with-expiration-timeout}

이 쿼리는 선택한 기간 내에서 성공적인 고객 행동을 유도한 상호 작용을 찾는 데 사용됩니다.

아래 쿼리는 지정된 기간 동안 대상 [!DNL Experience Event] 데이터 집합의 단일 채널에 대한 첫 번째 터치 속성 값과 세부 정보를 반환합니다. 쿼리는 선택한 채널에 대해 반환된 각 행에 대해 첫 번째 터치 값, 타임스탬프 및 속성이 포함된 `struct` 개체를 반환합니다.

**쿼리 구문**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE})
    OVER ({PARTITION} {ORDER} {FRAME})
```

잠재적으로 필요한 매개 변수의 전체 목록 및 설명은 [속성 쿼리 매개 변수 섹션](#attribution-query-parameters)을 참조하세요.

**예제 쿼리**

아래 표시된 예에서 각 고객 작업에 대해 반환되는 첫 번째 터치는 이전 7일 이내의 가장 빠른 상호 작용입니다(expTimeout = 86400 * 7).

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_FIRST_TOUCH_EXP_IF(timestamp, 'Paid First', marketing.trackingCode, commerce.purchases.value IS NOT NULL, false)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS first_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**결과**

```console
                 id                 |       timestamp       | trackingCode |                   first_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:05.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid First,em:483339,2019-07-21 18:45:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid First,em:70558,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 |              | (Paid First,em:70558,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid First,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

`first_touch` 열에 표시된 결과를 분류하려면 [열 구성 요소 섹션](#query-result-column-components)을 참조하세요.

### 만료 조건이 있는 마지막 터치 속성 {#last-touch-attribution-with-expiration-condition}

이 쿼리는 선택 조건에 따라 결정된 [!DNL Experience Event] 데이터 집합의 일부 내에서 일련의 고객 작업에서 마지막 상호 작용을 찾는 데 사용됩니다.

아래 쿼리는 대상 [!DNL Experience Event] 데이터 집합의 단일 채널에 대한 마지막 터치 속성 값과 세부 정보를 반환하며 조건 이후 또는 이전에 만료됩니다. 쿼리는 선택한 채널에 대해 반환된 각 행의 마지막 터치 값, 타임스탬프 및 속성이 포함된 `struct` 개체를 반환합니다.

**쿼리 구문**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

잠재적으로 필요한 매개 변수의 전체 목록 및 설명은 [속성 쿼리 매개 변수 섹션](#attribution-query-parameters)을 참조하세요.

**예제 쿼리**

아래 예에서는 결과에 표시된 4일(7월 15일, 21일, 23일 및 29일) 각각에 구매가 기록(`commerce.purchases.value IS NOT NULL`)되고 각 날의 마지막 추적 코드는 고객 작업에 대한 100%(`1.0`) 책임으로 연결됩니다.

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_LAST_TOUCH_EXP_IF(timestamp, 'trackingCode', marketing.trackingCode, commerce.purchases.value IS NOT NULL, false)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS last_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**결과 예**

```console
                id                 |       timestamp       | trackingCode |                   last_touch                   
-----------------------------------+-----------------------+--------------+------------------------------------------------
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 | em:1024841   | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 | em:550984    | (Paid Last,em:550984,2019-07-15 06:08:30.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid Last,em:380097,2019-07-23 12:38:51.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 | em:380097    | (Paid Last,em:380097,2019-07-23 12:38:51.0,1.0)
7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

`last_touch` 열에 표시된 결과를 분류하려면 [열 구성 요소 섹션](#query-result-column-components)을 참조하세요.

### 만료 시간 제한이 있는 마지막 터치 속성 {#last-touch-attribution-with-expiration-timeout}

이 쿼리는 선택한 시간 간격 내에서 마지막 상호 작용을 찾는 데 사용됩니다. 쿼리가 지정된 기간 동안 대상 [!DNL Experience Event] 데이터 집합의 단일 채널에 대한 마지막 터치 속성 값과 세부 정보를 반환합니다. 쿼리는 선택한 채널에 대해 반환된 각 행의 마지막 터치 값, 타임스탬프 및 속성이 포함된 `struct` 개체를 반환합니다.

**쿼리 구문**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_TIMEOUT}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

잠재적으로 필요한 매개 변수의 전체 목록 및 설명은 [속성 쿼리 매개 변수 섹션](#attribution-query-parameters)을 참조하세요.

**예제 쿼리**

아래 표시된 예에서 각 고객 작업에 대해 반환되는 마지막 터치는 다음 7일(`expTimeout = 86400 * 7`) 내의 최종 상호 작용입니다.

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(timestamp, 'trackingCode', marketing.trackingCode, 86400 * 7)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS last_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**결과**

```console
                id                 |       timestamp       | trackingcode |                   last_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 | em:1024841   | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 |              | (Paid Last,em:483339,2019-07-21 18:56:56.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid Last,sms:70558,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid Last,sms:70558,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid Last,sms:70558,2019-07-23 12:38:51.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 |              | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid Last,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

`last_touch` 열에 표시된 결과를 분류하려면 [열 구성 요소 섹션](#query-result-column-components)을 참조하세요.
