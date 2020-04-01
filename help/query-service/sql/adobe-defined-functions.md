---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe 정의 함수
topic: functions
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# Adobe 정의 함수

ADF(Adobe Defined Functions)는 ExperienceEvent 데이터에 대한 일반적인 비즈니스 관련 작업을 수행하는 데 도움이 되는 쿼리 서비스에 미리 만들어진 함수입니다. 여기에는 Adobe Analytics에 있는 것과 같은 세션화 및 기여도 분석 기능이 포함됩니다. Adobe [Analytics와 이 페이지에 정의된 ADF의 이면에 대한 자세한 내용은 Adobe Analytics 설명서를](https://docs.adobe.com/content/help/en/analytics/landing/home.html) 참조하십시오. 이 문서에서는 쿼리 서비스에서 사용할 수 있는 Adobe에서 정의한 함수에 대한 정보를 제공합니다.

## 창 함수

비즈니스 로직의 대부분은 고객의 접점을 수집하여 시간의 경과에 따라 주문해야 합니다. 이 지원은 Spark SQL에서 윈도우 기능의 형태로 제공합니다. 창 함수는 표준 SQL의 일부이며 다른 많은 SQL 엔진에서 지원됩니다.

창 함수는 집계를 업데이트하고 주문된 하위 집합의 각 행에 대해 단일 항목을 반환합니다. 가장 기본적인 집계 기능은 `SUM()`입니다. `SUM()` 행을 가져와서 하나의 합계를 제공합니다. 대신 `SUM()` 창에 적용하여 창 함수로 전환하면 각 행에 누적 합계를 받게 됩니다.

Spark SQL 도움말의 대부분은 창의 각 행을 업데이트하는 창 함수입니다. 이때 행 상태가 추가됩니다.

### 사양

구문: `OVER ([partition] [order] [frame])`

| 매개 변수 | 설명 |
| --- | --- |
| [파티션] | 열 또는 사용 가능한 필드를 기반으로 하는 행의 하위 그룹입니다. 예, `PARTITION BY endUserIds._experience.mcid.id` |
| [주문] | 하위 집합 또는 행의 순서를 지정하는 데 사용되는 열 또는 사용 가능한 필드입니다. 예, `ORDER BY timestamp` |
| [프레임] | 파티션의 행 하위 그룹입니다. 예, `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` |

## 세션화

웹 사이트, 모바일 애플리케이션, 인터랙티브한 음성 응답 시스템 또는 기타 고객 인터랙션 채널에서 생성된 ExperienceEvent 데이터를 사용하여 작업하는 경우 관련 활동 기간 동안 이벤트를 그룹화할 수 있는 경우에 도움이 됩니다. 일반적으로 제품 연구, 청구서 지불, 계좌 잔액 확인, 신청서 작성 등과 같은 활동을 유도하는 특정 의도가 있습니다. 이 그룹화는 이벤트를 연결하여 고객 경험에 대한 더 많은 컨텍스트를 파악하는 데 도움이 됩니다.

Adobe Analytics의 세션화에 대한 자세한 내용은 [컨텍스트 인식 세션에](https://docs.adobe.com/content/help/en/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html)대한 설명서를 참조하십시오.

### 사양

구문: `SESS_TIMEOUT(timestamp, expirationInSeconds) OVER ([partition] [order] [frame])`

| 매개 변수 | 설명 |
| --- | --- |
| `timestamp` | 데이터 세트에 있는 타임스탬프 필드 |
| `expirationInSeconds` | 현재 세션의 끝과 새 세션의 시작을 확인하는 이벤트 간 소요 시간(초) |

| 반환된 개체 매개 변수 | 설명 |
| ---------------------- | ------------- |
| `timestamp_diff` | 현재 레코드와 이전 레코드 간 시간(초) |
| `num` | 창 함수의 에 정의된 키에 대해 1부터 시작하는 `PARTITION BY` 단일 세션 번호입니다. |
| `is_new` | 레코드가 세션의 첫 번째인지 여부를 식별하는 데 사용되는 부울 |
| `depth` | 세션 내의 현재 레코드 심도 |

#### 예제 쿼리

```sql
SELECT 
  endUserIds._experience.mcid.id as id, 
  timestamp,
  SESS_TIMEOUT(timestamp, 60 * 30)
    OVER (PARTITION BY endUserIds._experience.mcid.id
        ORDER BY timestamp
        ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
    AS session
FROM experience_events
ORDER BY id, timestamp ASC
LIMIT 10
```

#### 결과

```
                id                |       timestamp       |      session       
----------------------------------+-----------------------+--------------------
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:55:53.0 | (0,1,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:56:51.0 | (58,1,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:57:47.0 | (56,1,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:58:27.0 | (40,1,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:59:22.0 | (55,1,false,5)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:16:23.0 | (1361821,2,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:17:17.0 | (54,2,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:06.0 | (49,2,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:39.0 | (33,2,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:19:10.0 | (31,2,false,5)
(10 rows)
```

## 속성

고객 행동과 고객 행동을 성공적으로 연결시키는 것은 고객 경험에 영향을 미치는 요인을 이해하는 데 중요한 요소입니다. 다음 ADF 파섹

Adobe Analytics의 기여도에 대한 자세한 내용은 분석 [안내서의 기여도 IQ 개요를](https://docs.adobe.com/content/help/en/analytics/analyze/analysis-workspace/panels/attribution.html) 참조하십시오.

### 첫 번째 터치 속성

대상 ExperienceEvent 데이터 세트에 있는 단일 채널에 대한 첫 번째 터치 속성 값과 세부 사항을 반환합니다. 쿼리는 선택한 채널에 대해 반환되는 각 행에 대해 첫 번째 터치 값, 타임스탬프 및 속성이 있는 `struct` 개체를 반환합니다.

이 쿼리는 일련의 고객 작업으로 인한 상호 작용을 확인하려는 경우 유용합니다. 아래 예에서, ExperienceEvent 데이터의 초기 추적 코드(`em:946426`)는 첫 번째 상호 작용이므로 고객 작업에 대한 100%(`1.0`) 책임이 있습니다.

### 사양

구문: `ATTRIBUTION_FIRST_TOUCH(timestamp, channelName, channelValue) OVER ([partition] [order] [frame])`

| 매개 변수 | 설명 |
| --- | --- |
| `timestamp` | 데이터 세트에 있는 타임스탬프 필드 |
| `channelName` | 반환된 객체에서 레이블로 사용할 친숙한 이름 |
| `channelValue` | 쿼리의 대상 채널인 열 또는 필드 |


| 반환된 개체 매개 변수 | 설명 |
| ---------------------- | ------------- |
| `name` | ADF에 레이블로 `channelName` 입력된 |
| `value` | ExperienceEvent의 첫 번째 `channelValue` 터치에 해당하는 값 |
| `timestamp` | 첫 번째 터치가 발생한 ExperienceEvent의 타임스탬프 |
| `fraction` | 분수 크레딧으로 표현된 첫 번째 터치 특성 |

#### 예제 쿼리

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

#### 결과

```
                id                 |       timestamp       | trackingCode |                   first_touch                    
-----------------------------------+-----------------------+--------------+--------------------------------------------------
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

### 마지막 터치 속성

대상 ExperienceEvent 데이터 세트에 있는 단일 채널에 대한 마지막 터치 속성 값과 세부 사항을 반환합니다. 쿼리는 선택한 채널에 대해 반환되는 각 행에 대한 마지막 터치 값, 타임스탬프 및 속성이 있는 `struct` 개체를 반환합니다.

이 쿼리는 일련의 고객 작업에서 최종 상호 작용을 보려는 경우에 유용합니다. 아래 표시된 예에서 반환된 객체의 추적 코드는 각 ExperienceEvent 레코드의 마지막 상호 작용입니다. 마지막 인터랙션이었기 때문에 각 코드는 고객 작업에 대한 100%(`1.0`) 책임을 부담합니다.

### 사양

구문: `ATTRIBUTION_LAST_TOUCH(timestamp, channelName, channelValue) OVER ([partition] [order] [frame])`

| 매개 변수 | 설명 |
| --- | --- |
| `timestamp` | 데이터 세트에 있는 타임스탬프 필드 |
| `channelName` | 반환된 객체에서 레이블로 사용할 친숙한 이름 |
| `channelValue` | 쿼리의 대상 채널인 열 또는 필드 |


| 반환된 개체 매개 변수 | 설명 |
| ---------------------- | ------------- |
| `name` | ADF에 레이블로 `channelName` 입력된 |
| `value` | ExperienceEvent의 마지막 터치인 `channelValue` 값의 값 |
| `timestamp` | ExperienceEvent가 사용된 타임스탬프 `channelValue` |
| `fraction` | 분수 크레딧으로 표현된 마지막 터치의 특성 |

#### 예제 쿼리

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

#### 결과

```
                id                 |       timestamp       | trackingcode |                   last_touch                   
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

### 만료 조건이 있는 첫 번째 터치 속성

조건 후 또는 그 이전에 만료되는 대상 ExperienceEvent 데이터 세트에 있는 단일 채널에 대한 첫 번째 터치 속성 값과 세부 사항을 반환합니다. 쿼리는 선택한 채널에 대해 반환되는 각 행에 대해 첫 번째 터치 값, 타임스탬프 및 속성이 있는 `struct` 개체를 반환합니다.

이 쿼리는 선택 조건에 의해 결정되는 ExperienceEvent 데이터 세트의 일부 내에서 일련의 고객 작업으로 이어지는 상호 작용을 보려는 경우 유용합니다. 아래 예에서, 구매는 (`commerce.purchases.value IS NOT NULL`) 각 4일 동안 결과(7월 15일, 21일, 23일 및 29일)에 기록되며, 각 날의 초기 추적 코드는 고객 작업에 대한 100%(`1.0`) 책임을 기여합니다.

#### 사양

구문: `ATTRIBUTION_FIRST_TOUCH_EXP_IF(timestamp, channelName, channelValue, expCondition, expBefore) OVER ([partition] [order] [frame])`

| 매개 변수 | 설명 |
| --- | --- |
| `timestamp` | 데이터 세트에 있는 타임스탬프 필드 |
| `channelName` | 반환된 객체에서 레이블로 사용할 친숙한 이름 |
| `channelValue` | 쿼리의 대상 채널인 열 또는 필드 |
| `expCondition` | 채널의 만료 지점을 결정하는 조건 |
| `expBefore` | 기본값은 `false`입니다. 지정된 조건을 충족하기 전 또는 후에 채널이 만료되는지 여부를 나타내는 부울입니다. 세션 만료 조건(예: `sess.depth = 1, true`)에 대해 기본적으로 활성화되어 이전 세션에서 첫 번째 터치가 선택되지 않도록 합니다. |

| 반환된 개체 매개 변수 | 설명 |
| ---------------------- | ------------- |
| `name` | ADF에 레이블로 `channelName` 입력된 |
| `value` | ExperienceEvent `channelValue` 의 첫 번째 터치에서 `expCondition` |
| `timestamp` | 첫 번째 터치가 발생한 ExperienceEvent의 타임스탬프 |
| `fraction` | 분수 크레딧으로 표현된 첫 번째 터치 특성 |

#### 예제 쿼리

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

#### 결과

```
                id                 |       timestamp       | trackingCode |                   first_touch                    
-----------------------------------+-----------------------+--------------+--------------------------------------------------
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

### 만료 시간 초과로 첫 번째 터치 속성

지정된 기간 동안 대상 ExperienceEvent 데이터 세트에 있는 단일 채널에 대한 첫 번째 터치 속성 값과 세부 사항을 반환합니다. 쿼리는 선택한 채널에 대해 반환되는 각 행에 대해 첫 번째 터치 값, 타임스탬프 및 속성이 있는 `struct` 개체를 반환합니다. 이 쿼리는 선택한 시간 간격 내에 고객 작업으로 이어지는 상호 작용을 보려는 경우에 유용합니다. 아래 예에서 각 고객 작업에 대해 반환된 첫 번째 접촉은 이전 7일(`expTimeout = 86400 * 7`) 내의 가장 빠른 상호 작용입니다.

#### 사양

구문: `ATTRIBUTION_FIRST_TOUCH_EXP_TIMEOUT(timestamp, channelName, channelValue, expTimeout) OVER ([partition] [order] [frame])`

| 매개 변수 | 설명 |
| --- | --- |
| `timestamp` | 데이터 세트에 있는 타임스탬프 필드 |
| `channelName` | 반환된 객체에서 레이블로 사용할 친숙한 이름 |
| `channelValue` | 쿼리의 대상 채널인 열 또는 필드 |
| `expTimeout` | 쿼리가 첫 번째 터치 이벤트를 검색하는 채널 이벤트 전 시간(초) |

| 반환된 개체 매개 변수 | 설명 |
| ---------------------- | ------------- |
| `name` | ADF에 레이블로 `channelName` 입력된 |
| `value` | 지정된 `channelValue` `expTimeout` 간격 내의 첫 번째 터치에 해당하는 값 |
| `timestamp` | 첫 번째 터치가 발생한 ExperienceEvent의 타임스탬프 |
| `fraction` | 분수 크레딧으로 표현된 첫 번째 터치 특성 |

#### 예제 쿼리

```sql
SELECT endUserIds._experience.mcid.id, timestamp, marketing.trackingCode,
    ATTRIBUTION_FIRST_TOUCH_EXP_TIMEOUT(timestamp, 'Paid First', marketing.trackingCode, 86400 * 7)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS first_touch
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

#### 결과

```
                id                 |       timestamp       | trackingCode |                   first_touch                    
-----------------------------------+-----------------------+--------------+--------------------------------------------------
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:04:10.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:05.0 | em:1024841   | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:05:35.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-15 06:08:30.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:45:10.0 | em:483339    | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:50:22.0 | em:483339    | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-21 18:56:56.0 |              | (Paid First,em:1024841,2019-07-15 06:04:10.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:25:12.0 | sms:70558    | (Paid First,em:483339,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-23 12:38:51.0 |              | (Paid First,em:483339,2019-07-23 12:25:12.0,1.0)
 7J82HGSSBNELKLD4-4107750913DE65DA | 2019-07-29 21:33:30.0 | em:884210    | (Paid First,em:884210,2019-07-29 21:33:30.0,1.0)
(10 rows)
```

### 만료 조건이 있는 마지막 터치 속성

조건 후 또는 그 이전에 만료되는 대상 ExperienceEvent 데이터 세트에 있는 단일 채널에 대한 마지막 터치 속성 값과 세부 사항을 반환합니다. 쿼리는 선택한 채널에 대해 반환되는 각 행에 대한 마지막 터치 값, 타임스탬프 및 속성이 있는 `struct` 개체를 반환합니다. 이 쿼리는 선택 조건에 의해 결정되는 ExperienceEvent 데이터 세트의 일부 내에서 일련의 고객 작업에서 마지막 상호 작용을 보려는 경우에 유용합니다. 아래 예에서, 구매는 (`commerce.purchases.value IS NOT NULL`) 결과에 표시된 4일(7월 15일, 21일, 23일 및 29일)마다 기록되며, 매일의 마지막 추적 코드는 고객 작업에 대한 100%(`1.0`) 책임을 기여합니다.

#### 사양

구문: `ATTRIBUTION_LAST_TOUCH_EXP_IF(timestamp, channelName, channelValue, expCondition, expBefore) OVER ([partition] [order] [frame])`

| 매개 변수 | 설명 |
| --- | --- |
| `timestamp` | 데이터 세트에 있는 타임스탬프 필드 |
| `channelName` | 반환된 객체에서 레이블로 사용할 친숙한 이름 |
| `channelValue` | 쿼리의 대상 채널인 열 또는 필드 |
| `expCondition` | 채널의 만료 지점을 결정하는 조건 |
| `expBefore` | 기본값은 `false`입니다. 지정된 조건을 충족하기 전 또는 후에 채널이 만료되는지 여부를 나타내는 부울입니다. 세션 만료 조건(예: `sess.depth = 1, true`)에 대해 기본적으로 활성화되므로 이전 세션에서 마지막 터치를 선택하지 않습니다. |

| 반환된 개체 매개 변수 | 설명 |
| ---------------------- | ------------- |
| `name` | ADF에 레이블로 `channelName` 입력된 |
| `value` | ExperienceEvent의 `channelValue` 마지막 터치인 값이 `expCondition` |
| `timestamp` | 마지막 터치가 발생한 ExperienceEvent의 타임스탬프 |
| `percentage` | 분수 크레딧으로 표현된 마지막 터치의 특성 |

#### 예제 쿼리

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

#### 결과

```
                id                 |       timestamp       | trackingcode |                   last_touch                   
-----------------------------------+-----------------------+--------------+-------------------------------------------------
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

### 만료 시간 초과가 있는 마지막 터치 속성

지정된 기간 동안 대상 ExperienceEvent 데이터 세트에 있는 단일 채널에 대한 마지막 터치 속성 값과 세부 사항을 반환합니다. 쿼리는 선택한 채널에 대해 반환되는 각 행에 대한 마지막 터치 값, 타임스탬프 및 속성이 있는 `struct` 개체를 반환합니다. 이 쿼리는 선택한 시간 간격 내에 마지막 상호 작용을 보려는 경우에 유용합니다. 아래 예에서 각 고객 작업에 대해 반환된 마지막 접촉은 다음 7일(`expTimeout = 86400 * 7`) 내의 마지막 인터랙션입니다.

#### 사양

구문: `ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(timestamp, channelName, channelValue, expTimeout) OVER ([partition] [order] [frame])`

| 매개 변수 | 설명 |
| --- | --- |
| `timestamp` | 데이터 세트에 있는 타임스탬프 필드 |
| `channelName` | 반환된 객체에서 레이블로 사용할 친숙한 이름 |
| `channelValue` | 쿼리의 대상 채널인 열 또는 필드 |
| `expTimeout` | 쿼리가 마지막 터치 이벤트를 검색하는 채널 이벤트까지 남은 시간(초) |

| 반환된 개체 매개 변수 | 설명 |
| ---------------------- | ------------- |
| `name` | ADF에 레이블로 `channelName` 입력된 |
| `value` | 지정된 `channelValue` `expTimeout` 간격 내의 마지막 터치에 해당하는 값 |
| `timestamp` | 마지막 터치가 발생한 ExperienceEvent의 타임스탬프 |
| `percentage` | 분수 크레딧으로 표현된 마지막 터치의 특성 |

#### 예제 쿼리

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

#### 결과

```
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

## 이전/다음 터치

고객이 경험 내에서 탐색하는 방식을 이해하는 것이 중요합니다. 고객의 참여도를 파악하고 경험의 의도된 단계를 설계된 대로 확인하며 고객에게 영향을 줄 수 있는 잠재적 고충점을 식별하는 데 사용할 수 있습니다. 다음 ADF는 이전 및 다음 관계에서 경로 지정 보기를 설정하는 것을 지원합니다. 이전 페이지 및 다음 페이지를 만들거나 여러 이벤트를 통해 경로 지정을 만들 수 있습니다.

### 이전 터치

특정 필드의 이전 값을 창 내에서 정의된 단계 수를 결정합니다. 이 예제에서는 `WINDOW` ADF를 `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` 설정하여 현재 행과 그 앞의 모든 행을 보도록 함수를 구성합니다.

#### 사양

구문: `PREVIOUS(key, [shift, [ignoreNulls]]) OVER ([partition] [order] [frame])`

| 매개 변수 | 설명 |
| --- | --- |
| `key` | 이벤트의 열 또는 필드입니다. |
| `shift` | (선택 사항) 현재 이벤트 외의 이벤트 수입니다. 기본값은 1입니다. |
| `ingnoreNulls` | null `key` 값을 무시해야 하는지 여부를 나타내는 부울입니다. Default is `false`. |


| 반환된 개체 매개 변수 | 설명 |
| ---------------------- | ------------- |
| `value` | ADF에서 `key` 사용되는 |

#### 예제 쿼리

```sql
SELECT endUserIds._experience.mcid.id, _experience.analytics.session.num, timestamp, web.webPageDetails.name
    PREVIOUS(web.webPageDetails.name, 3)
      OVER(PARTITION BY endUserIds._experience.mcid.id, _experience.analytics.session.num
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS previous_page
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, _experience.analytics.session.num, timestamp ASC
```

#### 결과

```
                id                 |       timestamp       |                 name                |                    previous_page                    
-----------------------------------+-----------------------+-------------------------------------+-----------------------------------------------------
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:15:28.0 |                                     | 
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:05.0 | Home                                | 
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:45.0 | Kids                                | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 19:22:34.0 |                                     | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:12.0 | Home                                | 
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:57.0 | Kids                                | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:03:36.0 | Search Results                      | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:04:30.0 | Product Details: Pemmican Power Bar | (Search Results)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:05:27.0 | Shopping Cart: Cart Details         | (Product Details: Pemmican Power Bar)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:06:07.0 | Shopping Cart: Shipping Information | (Shopping Cart: Cart Details)
(10 rows)
```

### 다음 터치

특정 필드의 다음 값을 창 내에서 정의된 여러 단계를 결정합니다. 이 예제에서는 `WINDOW` ADF를 `ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING` 설정하여 현재 행과 그 이후의 모든 행을 보도록 함수를 구성합니다.

#### 사양

구문: `NEXT(key, [shift, [ignoreNulls]]) OVER ([partition] [order] [frame])`

| 매개 변수 | 설명 |
| --- | --- |
| `key` | 이벤트의 열 또는 필드 |
| `shift` | (선택 사항) 현재 이벤트 외의 이벤트 수입니다. 기본값은 1입니다. |
| `ingnoreNulls` | null `key` 값을 무시해야 하는지 여부를 나타내는 부울입니다. Default is `false`. |


| 반환된 개체 매개 변수 | 설명 |
| ---------------------- | ------------- |
| `value` | ADF에서 `key` 사용되는 |

#### 예제 쿼리

```sql
SELECT endUserIds._experience.aaid.id, timestamp, web.webPageDetails.name,
    NEXT(web.webPageDetails.name, 1, true)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
      AS previous_page
FROM experience_events
ORDER BY endUserIds._experience.aaid.id, timestamp ASC
LIMIT 10
```

#### 결과

```
                id                 |       timestamp       |                name                 |             previous_page             
-----------------------------------+-----------------------+-------------------------------------+---------------------------------------
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:15:28.0 |                                     | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:05.0 | Home                                | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 17:53:45.0 | Kids                                | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 19:22:34.0 |                                     | (Home)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:12.0 | Home                                | (Kids)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:01:57.0 | Kids                                | (Search Results)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:03:36.0 | Search Results                      | (Product Details: Pemmican Power Bar)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:04:30.0 | Product Details: Pemmican Power Bar | (Shopping Cart: Cart Details)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:05:27.0 | Shopping Cart: Cart Details         | (Shopping Cart: Shipping Information)
 457C3510571E5930-69AA721C4CBF9339 | 2017-11-08 20:06:07.0 | Shopping Cart: Shipping Information | (Shopping Cart: Billing Information)
(10 rows)
```

## 시간 간격

시간 간격을 사용하면 이벤트 발생 전 또는 후 기간 내에 잠재된 고객 행동을 파악할 수 있습니다. 캠페인 또는 모든 고객의 다른 유형의 이벤트가 발생한 후 7일 이내에 이벤트를 확인합니다.

### 이전 일치 시간 사이

특정 사고 이후 경과된 시간을 측정하는 새 차원을 제공합니다.

#### 사양

구문: `TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventDefintion, [timeUnit]) OVER ([partition] [order] [frame])`

| 매개 변수 | 설명 |
| --- | --- |
| `timestamp` | 모든 이벤트에 채워진 데이터 세트에 있는 타임스탬프 필드 |
| `eventDefintion` | 이전 이벤트의 자격을 규정하는 식입니다. |
| `timeUnit` | 출력 단위:일, 시간, 분 및 초 기본값은 초입니다. |

출력:이전 일치 이벤트가 표시된 이후의 시간 단위를 나타내는 숫자를 반환하거나 일치하는 이벤트가 없는 경우 null로 남습니다.

#### 예제 쿼리

```sql
SELECT 
  page_name,
  SUM (time_between_previous_match) / COUNT(page_name) as average_minutes_since_registration
FROM
(
SELECT 
  endUserIds._experience.mcid.id as id, 
  timestamp, web.webPageDetails.name as page_name, 
  TIME_BETWEEN_PREVIOUS_MATCH(timestamp, web.webPageDetails.name='Account Registration|Confirmation', 'minutes')
    OVER(PARTITION BY endUserIds._experience.mcid.id
       ORDER BY timestamp
       ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
    AS time_between_previous_match
FROM experience_events
)
WHERE time_between_previous_match IS NOT NULL
GROUP BY page_name
ORDER BY average_minutes_since_registration
LIMIT 10
```

#### 결과

```
             page_name             | average_minutes_since_registration 
-----------------------------------+------------------------------------
                                   |                                   
 Account Registration|Confirmation |                                0.0
 Seasonal                          |                   5.47029702970297
 Equipment                         |                  6.532110091743119
 Women                             |                  7.287081339712919
 Men                               |                  7.640918580375783
 Product List                      |                  9.387459807073954
 Unlimited Blog|February           |                  9.954545454545455
 Product Details|Buffalo           |                 13.304347826086957
 Unlimited Blog|June               |                  770.4285714285714
(10 rows)
```

### 다음 일치 시간 사이

특정 이벤트가 발생하기 전의 시간을 측정하는 새 차원을 제공합니다.

#### 사양

구문: `TIME_BETWEEN_NEXT_MATCH(timestamp, eventDefintion, [timeUnit]) OVER ([partition] [order] [frame])`

| 매개 변수 | 설명 |
| --- | --- |
| `timestamp` | 모든 이벤트에 채워진 데이터 세트에 있는 타임스탬프 필드 |
| `eventDefintion` | 다음 이벤트의 자격을 규정하는 식입니다. |
| `timeUnit` | 출력 단위:일, 시간, 분 및 초 기본값은 초입니다. |

출력:다음 일치 이벤트 뒤의 시간 단위를 나타내는 음수를 반환하거나 일치하는 이벤트를 찾을 수 없는 경우 null로 남습니다.

#### 예제 쿼리

```
SELECT 
  page_name,
  SUM (time_between_next_match) / COUNT(page_name) as average_minutes_until_order_confirmation
FROM
(
SELECT 
  endUserIds._experience.mcid.id as id, 
  timestamp, web.webPageDetails.name as page_name, 
  TIME_BETWEEN_NEXT_MATCH(timestamp, web.webPageDetails.name='Shopping Cart|Order Confirmation', 'minutes')
    OVER(PARTITION BY endUserIds._experience.mcid.id
       ORDER BY timestamp
       ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
    AS time_between_next_match
FROM experience_events
)
WHERE time_between_next_match IS NOT NULL
GROUP BY page_name
ORDER BY average_minutes_until_order_confirmation DESC
LIMIT 10
```

#### 결과

```
             page_name             | average_minutes_until_order_confirmation 
-----------------------------------+------------------------------------------
 Shopping Cart|Order Confirmation  |                                      0.0
 Men                               |                       -9.465295629820051
 Equipment                         |                       -9.682098765432098
 Product List                      |                       -9.690661478599221
 Women                             |                       -9.759459459459459
 Seasonal                          |                                  -10.295
 Shopping Cart|Order Review        |                      -366.33567364956144
 Unlimited Blog|February           |                       -615.0327868852459
 Shopping Cart|Billing Information |                       -775.6200495367711
 Product Details|Buffalo           |                      -1274.9571428571428
(10 rows)
```

## 다음 단계

여기에 설명된 기능을 사용하여 쿼리를 작성하여 쿼리 서비스를 사용하여 고유한 ExperienceEvent 데이터 세트에 액세스할 수 있습니다. 쿼리 서비스의 쿼리 작성에 대한 자세한 내용은 쿼리 [만들기에 대한 설명서를 참조하십시오](../creating-queries/creating-queries.md).
