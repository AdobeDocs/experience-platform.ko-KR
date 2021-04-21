---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;adobe defined functions;sql
solution: Experience Platform
title: 쿼리 서비스의 Adobe 정의 SQL 함수
topic-legacy: functions
description: 이 문서에서는 Adobe Experience Platform 쿼리 서비스에서 사용할 수 있는 Adobe 정의 기능에 대한 정보를 제공합니다.
exl-id: 275aa14e-f555-4365-bcd6-0dd6df2456b3
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '2913'
ht-degree: 2%

---

# 쿼리 서비스의 Adobe 정의 SQL 함수

여기에서 ADF라고 하는 Adobe 정의 함수는 [!DNL Experience Event] 데이터에서 일반적인 비즈니스 관련 작업을 수행하는 데 도움이 되는 Adobe Experience Platform 쿼리 서비스에 미리 작성된 함수입니다. 여기에는 Adobe Analytics에 있는 것과 같은 [세션화](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html) 및 [속성](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html)에 대한 함수가 포함됩니다.

이 문서에서는 [!DNL Query Service]에서 사용할 수 있는 Adobe 정의 함수에 대한 정보를 제공합니다.

## 윈도우 함수 {#window-functions}

비즈니스 로직의 대부분은 고객의 접점을 모으고 시간에 따라 주문해야 합니다. 이 지원은 윈도우 함수 형태로 [!DNL Spark] SQL에서 제공합니다. 윈도우 함수는 표준 SQL의 일부이며 다른 많은 SQL 엔진에서 지원됩니다.

창 함수는 집계를 업데이트하고 주문한 하위 집합의 각 행에 대해 단일 항목을 반환합니다. 가장 기본적인 집계 함수는 `SUM()`입니다. `SUM()` 행을 가져와서 하나의 합계를 제공합니다. 대신 윈도우에 `SUM()`을 적용하여 윈도우 함수로 전환하면 각 행에 대해 누적 합계를 받게 됩니다.

[!DNL Spark] SQL 도우미의 대부분은 윈도우의 각 행을 업데이트하면서 해당 행의 상태가 추가된 윈도우 함수입니다.

**쿼리 구문**

```sql
OVER ({PARTITION} {ORDER} {FRAME})
```

| 매개 변수 | 설명 | 예 |
| --------- | ----------- | ------- |
| `{PARTITION}` | 열 또는 사용 가능한 필드를 기반으로 하는 행 하위 그룹. | `PARTITION BY endUserIds._experience.mcid.id` |
| `{ORDER}` | 하위 집합 또는 행의 순서를 지정하는 데 사용되는 열 또는 사용 가능한 필드. | `ORDER BY timestamp` |
| `{FRAME}` | 파티션의 행 하위 그룹입니다. | `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` |

## 세션화

웹 사이트, 모바일 애플리케이션, 인터랙티브한 음성 응답 시스템 또는 기타 고객 상호 작용 채널에서 시작된 [!DNL Experience Event] 데이터로 작업하는 경우 관련 활동 기간을 기준으로 이벤트를 그룹화할 수 있는지 여부를 확인하는 데 도움이 됩니다. 일반적으로 제품 연구, 청구서 지불, 계좌 잔액 확인, 신청서 작성 등과 같이 사용자의 활동을 유도하는 특정 의도가 있습니다.

이러한 데이터 그룹화 또는 세션을 통해 이벤트를 연결하여 고객 경험에 대한 더 많은 컨텍스트를 파악할 수 있습니다.

Adobe Analytics의 세션화에 대한 자세한 내용은 [컨텍스트 인식 세션](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html)의 설명서를 참조하십시오.

**쿼리 구문**

```sql
SESS_TIMEOUT({TIMESTAMP}, {EXPIRATION_IN_SECONDS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{TIMESTAMP}` | 데이터 세트에 있는 타임스탬프 필드입니다. |
| `{EXPIRATION_IN_SECONDS}` | 현재 세션의 끝과 새 세션의 시작을 검증하는 데 필요한 이벤트 간 시간(초)입니다. |

`OVER()` 함수 내의 매개 변수에 대한 설명은 [window functions 섹션](#window-functions)에서 찾을 수 있습니다.

**쿼리 예**

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

**결과**

```console
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

지정된 샘플 쿼리의 경우 결과는 `session` 열에 제공됩니다. `session` 열은 다음 구성 요소로 구성됩니다.

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| 매개 변수 | 설명 |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | 현재 레코드와 이전 레코드 간의 시간 차이(초)입니다. |
| `{NUM}` | 윈도우 함수의 `PARTITION BY`에 정의된 키에 대해 1부터 시작하는 고유한 세션 번호입니다. |
| `{IS_NEW}` | 레코드가 세션의 첫 번째인지 여부를 식별하는 데 사용되는 부울 값입니다. |
| `{DEPTH}` | 세션 내의 현재 레코드 깊이입니다. |

### SESS_START_IF

이 쿼리는 현재 타임스탬프 및 지정된 표현식을 기반으로 현재 행의 세션 상태를 반환하고 현재 행으로 새 세션을 시작합니다.

**쿼리 구문**

```sql
SESS_START_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{TIMESTAMP}` | 데이터 세트에 있는 타임스탬프 필드입니다. |
| `{TEST_EXPRESSION}` | 데이터 필드를 확인하려는 표현식입니다. 예: `application.launches > 0`. |

`OVER()` 함수 내의 매개 변수에 대한 설명은 [window functions 섹션](#window-functions)에서 찾을 수 있습니다.

**쿼리 예**

```sql
SELECT
    endUserIds._experience.mcid.id AS id,
    timestamp,
    IF(application.launches.value > 0, true, false) AS isLaunch,
    SESS_START_IF(timestamp, application.launches.value > 0)
        OVER (PARTITION BY endUserIds._experience.mcid.id
            ORDER BY timestamp
            ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
        AS session
    FROM experience_events
    ORDER BY id, timestamp ASC
    LIMIT 10
```

**결과**

```console
                id                |       timestamp       | isLaunch |      session       
----------------------------------+-----------------------+----------+--------------------
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:55:53.0 | true     | (0,1,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:56:51.0 | false    | (58,1,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:57:47.0 | false    | (56,1,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:58:27.0 | true     | (40,2,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:59:22.0 | false    | (55,2,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:16:23.0 | false    | (1361821,2,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:17:17.0 | false    | (54,2,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:06.0 | false    | (49,2,false,5)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:39.0 | false    | (33,2,false,6)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:19:10.0 | false    | (31,2,false,7)
(10 rows)
```

지정된 샘플 쿼리의 경우 결과는 `session` 열에 제공됩니다. `session` 열은 다음 구성 요소로 구성됩니다.

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| 매개 변수 | 설명 |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | 현재 레코드와 이전 레코드 간의 시간 차이(초)입니다. |
| `{NUM}` | 윈도우 함수의 `PARTITION BY`에 정의된 키에 대해 1부터 시작하는 고유한 세션 번호입니다. |
| `{IS_NEW}` | 레코드가 세션의 첫 번째인지 여부를 식별하는 데 사용되는 부울 값입니다. |
| `{DEPTH}` | 세션 내의 현재 레코드 깊이입니다. |

### SESS_END_IF

이 쿼리는 현재 타임스탬프와 제공된 식을 기반으로 현재 행의 세션 상태를 반환하고 현재 세션을 종료하고 다음 행에서 새 세션을 시작합니다.

**쿼리 구문**

```sql
SESS_END_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{TIMESTAMP}` | 데이터 세트에 있는 타임스탬프 필드입니다. |
| `{TEST_EXPRESSION}` | 데이터 필드를 확인하려는 표현식입니다. 예: `application.launches > 0`. |

`OVER()` 함수 내의 매개 변수에 대한 설명은 [window functions 섹션](#window-functions)에서 찾을 수 있습니다.

**쿼리 예**

```sql
SELECT
    endUserIds._experience.mcid.id AS id,
    timestamp,
    IF(application.applicationCloses.value > 0 OR application.crashes.value > 0, true, false) AS isExit,
    SESS_END_IF(timestamp, application.applicationCloses.value > 0 OR application.crashes.value > 0)
        OVER (PARTITION BY endUserIds._experience.mcid.id
            ORDER BY timestamp
            ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
        AS session
    FROM experience_events
    ORDER BY id, timestamp ASC
    LIMIT 10
```

**결과**

```console
                id                |       timestamp       | isExit   |      session       
----------------------------------+-----------------------+----------+--------------------
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:55:53.0 | false    | (0,1,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:56:51.0 | false    | (58,1,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:57:47.0 | true     | (56,1,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:58:27.0 | false    | (40,2,true,1)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-01-18 06:59:22.0 | false    | (55,2,false,2)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:16:23.0 | false    | (1361821,2,false,3)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:17:17.0 | false    | (54,2,false,4)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:06.0 | false    | (49,2,false,5)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:18:39.0 | false    | (33,2,false,6)
 100080F22A45CB40-3A2B7A8E11096B6 | 2018-02-03 01:19:10.0 | false    | (31,2,false,7)
(10 rows)
```

지정된 샘플 쿼리의 경우 결과는 `session` 열에 제공됩니다. `session` 열은 다음 구성 요소로 구성됩니다.

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| 매개 변수 | 설명 |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | 현재 레코드와 이전 레코드 간의 시간 차이(초)입니다. |
| `{NUM}` | 윈도우 함수의 `PARTITION BY`에 정의된 키에 대해 1부터 시작하는 고유한 세션 번호입니다. |
| `{IS_NEW}` | 레코드가 세션의 첫 번째인지 여부를 식별하는 데 사용되는 부울 값입니다. |
| `{DEPTH}` | 세션 내의 현재 레코드 깊이입니다. |

## 속성

고객 행동을 성공에 연결하는 것은 고객 경험에 영향을 주는 요인을 이해하는 데 중요한 요소입니다. 다음 ADF는 다른 만료 설정으로 첫 번째 터치 속성 및 마지막 터치 속성을 지원합니다.

Adobe Analytics의 속성에 대한 자세한 내용은 [!DNL Analytics] 속성 패널 안내서의 [Attribution IQ 개요](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/attribution.html)를 참조하십시오.

### 첫 번째 터치 속성

이 쿼리는 대상 [!DNL Experience Event] 데이터 세트에 있는 단일 채널에 대한 첫 번째 터치 속성 값과 세부 사항을 반환합니다. 쿼리는 선택한 채널에 대해 반환되는 각 행에 대해 첫 번째 터치 값, 타임스탬프 및 속성이 있는 `struct` 개체를 반환합니다.

이 쿼리는 일련의 고객 작업으로 이어지는 상호 작용을 보려는 경우에 유용합니다. 아래 예에서, 고객 작업에 대한 첫 번째 상호 작용이므로 [!DNL Experience Event] 데이터의 초기 추적 코드(`em:946426`)는 100%(`1.0`) 권한을 부여합니다.

**쿼리 구문**

```sql
ATTRIBUTION_FIRST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{TIMESTAMP}` | 데이터 세트에 있는 타임스탬프 필드입니다. |
| `{CHANNEL_NAME}` | 반환된 객체의 레이블입니다. |
| `{CHANNEL_VALUE}` | 쿼리의 대상 채널인 열 또는 필드입니다. |

`OVER()` 내의 매개 변수에 대한 설명은 [window functions 섹션](#window-functions)에서 찾을 수 있습니다.

**쿼리 예**

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

```console
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

지정된 샘플 쿼리의 경우 결과는 `first_touch` 열에 제공됩니다. `first_touch` 열은 다음 구성 요소로 구성됩니다.

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{NAME}` | ADF에 레이블로 입력된 `{CHANNEL_NAME}`. |
| `{VALUE}` | [!DNL Experience Event]에서 첫 번째 터치에 해당하는 `{CHANNEL_VALUE}`의 값 |
| `{TIMESTAMP}` | 첫 번째 터치가 발생한 [!DNL Experience Event]의 타임스탬프. |
| `{FRACTION}` | 첫 번째 터치의 어트리뷰션(십진수)으로 표현됩니다. |

### 마지막 터치 속성

이 쿼리는 대상 [!DNL Experience Event] 데이터 세트에 있는 단일 채널에 대한 마지막 터치 속성 값과 세부 사항을 반환합니다. 쿼리는 선택한 채널에 대해 반환되는 각 행에 대한 마지막 터치 값, 타임스탬프 및 속성이 있는 `struct` 개체를 반환합니다.

이 쿼리는 일련의 고객 작업에서 최종 상호 작용을 보려는 경우에 유용합니다. 아래 예에서, 반환된 객체의 추적 코드는 각 [!DNL Experience Event] 레코드에 있는 마지막 상호 작용입니다. 마지막 상호 작용이므로 각 코드는 고객 작업에 대해 100%(`1.0`) 책임을 갖습니다.

**쿼리 구문**

```sql
ATTRIBUTION_LAST_TOUCH({TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{TIMESTAMP}` | 데이터 세트에 있는 타임스탬프 필드입니다. |
| `{CHANNEL_NAME}` | 반환된 객체의 레이블입니다. |
| `{CHANNEL_VALUE}` | 쿼리의 대상 채널인 열 또는 필드입니다. |

`OVER()` 내의 매개 변수에 대한 설명은 [window functions 섹션](#window-functions)에서 찾을 수 있습니다.

**쿼리 예**

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

```console
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

지정된 샘플 쿼리의 경우 결과는 `last_touch` 열에 제공됩니다. `last_touch` 열은 다음 구성 요소로 구성됩니다.

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `{NAME}` | ADF에 레이블로 입력된 `{CHANNEL_NAME}`. |
| `{VALUE}` | [!DNL Experience Event]에서 마지막 터치인 `{CHANNEL_VALUE}`의 값 |
| `{TIMESTAMP}` | `channelValue`이(가) 사용된 [!DNL Experience Event]의 타임스탬프. |
| `{FRACTION}` | 십진수로 표현되는 마지막 터치 속성. |

### 만료 조건이 있는 첫 번째 터치 속성

이 쿼리는 조건 후 또는 그 이전에 만료되는 대상 [!DNL Experience Event] 데이터 세트에 있는 단일 채널에 대한 첫 번째 터치 속성 값과 세부 사항을 반환합니다. 쿼리는 선택한 채널에 대해 반환되는 각 행에 대해 첫 번째 터치 값, 타임스탬프 및 속성이 있는 `struct` 개체를 반환합니다.

이 쿼리는 선택한 조건에 따라 결정되는 [!DNL Experience Event] 데이터 세트 중 일부 내에서 일련의 고객 작업으로 이어지는 상호 작용을 보려는 경우에 유용합니다. 아래 예에서, 구매(`commerce.purchases.value IS NOT NULL`)는 결과에 표시된 4일 각각에 기록되고(7월 15일, 21일, 23일 및 29일) 각 날의 초기 추적 코드는 고객 작업에 대한 100%(`1.0`) 권한을 부여합니다.

**쿼리 구문**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{TIMESTAMP}` | 데이터 세트에 있는 타임스탬프 필드입니다. |
| `{CHANNEL_NAME}` | 반환된 객체의 레이블입니다. |
| `{CHANNEL_VALUE}` | 쿼리의 대상 채널인 열 또는 필드입니다. |
| `{EXP_CONDITION}` | 채널의 만료 지점을 결정하는 조건. |
| `{EXP_BEFORE}` | 지정된 조건인 `{EXP_CONDITION}`이(가) 충족되기 전이나 후에 채널이 만료되는지 여부를 나타내는 부울입니다. 이전 세션에서 첫 번째 터치를 선택하지 않도록 세션의 만료 조건에 대해 기본적으로 활성화됩니다. 기본적으로 이 값은 `false`으로 설정됩니다. |

`OVER()` 함수 내의 매개 변수에 대한 설명은 [window functions 섹션](#window-functions)에서 찾을 수 있습니다.

**쿼리 예**

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

지정된 샘플 쿼리의 경우 결과는 `first_touch` 열에 제공됩니다. `first_touch` 열은 다음 구성 요소로 구성됩니다.

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `{NAME}` | ADF에 레이블로 입력된 `{CHANNEL_NAME}`. |
| `{VALUE}` | `{EXP_CONDITION}` 앞에 있는 [!DNL Experience Event]의 첫 번째 터치에 해당하는 `CHANNEL_VALUE}`의 값입니다. |
| `{TIMESTAMP}` | 첫 번째 터치가 발생한 [!DNL Experience Event]의 타임스탬프. |
| `{FRACTION}` | 첫 번째 터치의 어트리뷰션(십진수)으로 표현됩니다. |

### 만료 시간 초과가 있는 첫 번째 터치 속성

이 쿼리는 지정된 기간 동안 대상 [!DNL Experience Event] 데이터 세트에 있는 단일 채널에 대한 첫 번째 터치 속성 값과 세부 사항을 반환합니다. 쿼리는 선택한 채널에 대해 반환되는 각 행에 대해 첫 번째 터치 값, 타임스탬프 및 속성이 있는 `struct` 개체를 반환합니다.

이 쿼리는 선택한 시간 간격 내에서 고객 작업으로 이어지는 상호 작용을 보려는 경우에 유용합니다. 아래 예에서 각 고객 작업에 대해 반환된 첫 번째 접촉은 이전 7일(`expTimeout = 86400 * 7`) 내의 가장 빠른 상호 작용입니다.

**사양**

```sql
ATTRIBUTION_FIRST_TOUCH_EXP_TIMEOUT(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_TIMEOUT}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{TIMESTAMP}` | 데이터 세트에 있는 타임스탬프 필드입니다. |
| `{CHANNEL_NAME}` | 반환된 객체의 레이블입니다. |
| `{CHANNEL_VALUE}` | 쿼리의 대상 채널인 열 또는 필드입니다. |
| `{EXP_TIMEOUT}` | 쿼리가 첫 번째 터치 이벤트를 검색하는 채널 이벤트 전 시간(초)입니다. |

`OVER()` 함수 내의 매개 변수에 대한 설명은 [window functions 섹션](#window-functions)에서 찾을 수 있습니다.

**쿼리 예**

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

**결과**

```console
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

지정된 샘플 쿼리의 경우 결과는 `first_touch` 열에 제공됩니다. `first_touch` 열은 다음 구성 요소로 구성됩니다.

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `{NAME}` | ADF에 레이블로 입력된 `{CHANNEL_NAME}`. |
| `{VALUE}` | 지정된 `{EXP_TIMEOUT}` 간격 내의 첫 번째 터치인 `CHANNEL_VALUE}`의 값입니다. |
| `{TIMESTAMP}` | 첫 번째 터치가 발생한 [!DNL Experience Event]의 타임스탬프. |
| `{FRACTION}` | 첫 번째 터치의 어트리뷰션(십진수)으로 표현됩니다. |

### 만료 조건이 있는 마지막 터치 속성

이 쿼리는 조건 후 또는 그 이전에 만료되는 대상 [!DNL Experience Event] 데이터 세트에 있는 단일 채널에 대한 마지막 터치 속성 값과 세부 사항을 반환합니다. 쿼리는 선택한 채널에 대해 반환되는 각 행에 대한 마지막 터치 값, 타임스탬프 및 속성이 있는 `struct` 개체를 반환합니다.

이 쿼리는 선택한 조건에 따라 결정되는 [!DNL Experience Event] 데이터 세트 중 일부 내에서 일련의 고객 작업에서 마지막 상호 작용을 보려는 경우에 유용합니다. 아래 예에서, 구매는 결과(7월 15일, 21일, 23일 및 29일)에 표시된 4일 각각에 대해 기록되며, 매일의 마지막 추적 코드는 고객 작업에 대한 100%(`1.0`) 권한을 부여합니다.`commerce.purchases.value IS NOT NULL`

**쿼리 구문**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_IF(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_CONDITION}, {EXP_BEFORE}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{TIMESTAMP}` | 데이터 세트에 있는 타임스탬프 필드입니다. |
| `{CHANNEL_NAME}` | 반환된 객체의 레이블입니다. |
| `{CHANNEL_VALUE}` | 쿼리의 대상 채널인 열 또는 필드입니다. |
| `{EXP_CONDITION}` | 채널의 만료 지점을 결정하는 조건. |
| `{EXP_BEFORE}` | 지정된 조건인 `{EXP_CONDITION}`이(가) 충족되기 전이나 후에 채널이 만료되는지 여부를 나타내는 부울입니다. 이전 세션에서 첫 번째 터치를 선택하지 않도록 세션의 만료 조건에 대해 기본적으로 활성화됩니다. 기본적으로 이 값은 `false`으로 설정됩니다. |

**쿼리 예**

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

지정된 샘플 쿼리의 경우 결과는 `last_touch` 열에 제공됩니다. `last_touch` 열은 다음 구성 요소로 구성됩니다.

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `{NAME}` | ADF에 레이블로 입력된 `{CHANNEL_NAME}`. |
| `{VALUE}` | `{EXP_CONDITION}` 앞에 있는 [!DNL Experience Event]의 마지막 터치인 `{CHANNEL_VALUE}`의 값입니다. |
| `{TIMESTAMP}` | 마지막 터치가 발생한 [!DNL Experience Event]의 타임스탬프. |
| `{FRACTION}` | 십진수로 표현되는 마지막 터치 속성. |

### 만료 시간 초과가 있는 마지막 터치 속성

이 쿼리는 지정된 기간 동안 대상 [!DNL Experience Event] 데이터 세트에 있는 단일 채널에 대한 마지막 터치 속성 값과 세부 사항을 반환합니다. 쿼리는 선택한 채널에 대해 반환되는 각 행에 대한 마지막 터치 값, 타임스탬프 및 속성이 있는 `struct` 개체를 반환합니다.

이 쿼리는 선택한 시간 간격 내의 마지막 상호 작용을 보려는 경우에 유용합니다. 아래 예에서, 각 고객 작업에 대해 반환된 마지막 접촉은 다음 7일(`expTimeout = 86400 * 7`) 내의 최종 상호 작용입니다.

**쿼리 구문**

```sql
ATTRIBUTION_LAST_TOUCH_EXP_TIMEOUT(
    {TIMESTAMP}, {CHANNEL_NAME}, {CHANNEL_VALUE}, {EXP_TIMEOUT}) 
    OVER ({PARTITION} {ORDER} {FRAME})
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{TIMESTAMP}` | 데이터 세트에 있는 타임스탬프 필드입니다. |
| `{CHANNEL_NAME}` | 반환된 객체의 레이블 |
| `{CHANNEL_VALUE}` | 쿼리의 대상 채널인 열 또는 필드 |
| `{EXP_TIMEOUT}` | 쿼리가 마지막 터치 이벤트를 검색하는 채널 이벤트 후 시간(초)입니다. |

`OVER()` 함수 내의 매개 변수에 대한 설명은 [window functions 섹션](#window-functions)에서 찾을 수 있습니다.

**쿼리 예**

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

지정된 샘플 쿼리의 경우 결과는 `last_touch` 열에 제공됩니다. `last_touch` 열은 다음 구성 요소로 구성됩니다.

```sql
({NAME}, {VALUE}, {TIMESTAMP}, {FRACTION})
```

| 매개 변수 | 설명 |
| ---------- | ----------- |
| `{NAME}` | ADF에 레이블로 입력된 `{CHANNEL_NAME}`. |
| `{VALUE}` | 지정된 `{EXP_TIMEOUT}` 간격 내의 마지막 터치인 `{CHANNEL_VALUE}`의 값 |
| `{TIMESTAMP}` | 마지막 터치가 발생한 [!DNL Experience Event]의 타임스탬프 |
| `{FRACTION}` | 십진수로 표현되는 마지막 터치 속성. |

## 경로 지정

경로 지정을 사용하여 고객의 참여 심도를 이해하고 경험의 의도한 단계가 설계된 대로 작동하는지 확인하고 고객에게 영향을 줄 수 있는 잠재적인 고충점을 식별할 수 있습니다.

다음 ADF는 이전 및 다음 관계에서 경로 지정 보기를 설정하는 것을 지원합니다. 이전 페이지와 다음 페이지를 만들거나 여러 이벤트를 통해 경로 지정을 만들 수 있습니다.

### 이전 페이지

특정 필드의 이전 값을 창 내에서 정의된 단계 수를 결정합니다. 이 예제에서 `WINDOW` 함수는 `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` 프레임으로 구성되어 현재 행과 모든 후속 행을 볼 수 있도록 ADF를 설정합니다.

**쿼리 구문**

```sql
PREVIOUS({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{KEY}` | 이벤트의 열 또는 필드입니다. |
| `{SHIFT}` | (선택 사항) 현재 이벤트로부터 떨어진 이벤트 수입니다. 기본적으로 값은 1입니다. |
| `{IGNORE_NULLS}` | (선택 사항) null `{KEY}` 값을 무시해야 하는지 여부를 나타내는 부울 값입니다. 기본적으로 이 값은 `false`입니다. |

`OVER()` 함수 내의 매개 변수에 대한 설명은 [window functions 섹션](#window-functions)에서 찾을 수 있습니다.

**쿼리 예**

```sql
SELECT endUserIds._experience.mcid.id, timestamp, web.webPageDetails.name
    PREVIOUS(web.webPageDetails.name, 3)
      OVER(PARTITION BY endUserIds._experience.mcid.id
           ORDER BY timestamp
           ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)
      AS previous_page
FROM experience_events
ORDER BY endUserIds._experience.mcid.id, timestamp ASC
```

**결과**

```console
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

지정된 샘플 쿼리의 경우 결과는 `previous_page` 열에 제공됩니다. `previous_page` 열 내의 값은 ADF에 사용되는 `{KEY}`을 기반으로 합니다.

### 다음 페이지

특정 필드의 다음 값을 창 내에서 정의된 단계 수를 결정합니다. 이 예제에서 `WINDOW` 함수는 `ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING` 프레임으로 구성되어 현재 행과 모든 후속 행을 볼 수 있도록 ADF를 설정합니다.

**쿼리 구문**

```sql
NEXT({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{KEY}` | 이벤트의 열 또는 필드입니다. |
| `{SHIFT}` | (선택 사항) 현재 이벤트로부터 떨어진 이벤트 수입니다. 기본적으로 값은 1입니다. |
| `{IGNORE_NULLS}` | (선택 사항) null `{KEY}` 값을 무시해야 하는지 여부를 나타내는 부울 값입니다. 기본적으로 이 값은 `false`입니다. |

`OVER()` 함수 내의 매개 변수에 대한 설명은 [window functions 섹션](#window-functions)에서 찾을 수 있습니다.

**쿼리 예**

```sql
SELECT endUserIds._experience.aaid.id, timestamp, web.webPageDetails.name,
    NEXT(web.webPageDetails.name, 1, true)
      OVER(PARTITION BY endUserIds._experience.aaid.id
           ORDER BY timestamp
           ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING)
      AS next_page
FROM experience_events
ORDER BY endUserIds._experience.aaid.id, timestamp ASC
LIMIT 10
```

**결과**

```console
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

지정된 샘플 쿼리의 경우 결과는 `previous_page` 열에 제공됩니다. `previous_page` 열 내의 값은 ADF에 사용되는 `{KEY}`을 기반으로 합니다.

## 시간 간격

기간 간격을 사용하면 이벤트가 발생하기 전이나 후에 특정 기간 내에 잠재된 고객 행동을 파악할 수 있습니다.

### 이전 일치 시간 간격

이 쿼리는 이전 일치 이벤트가 표시된 이후의 시간 단위를 나타내는 숫자를 반환합니다. 일치하는 이벤트를 찾을 수 없으면 null을 반환합니다.

**쿼리 구문**

```sql
TIME_BETWEEN_PREVIOUS_MATCH(
    {TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT})
    OVER ({PARTITION} {ORDER} {FRAME})
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{TIMESTAMP}` | 모든 이벤트에 채워진 데이터 세트에 있는 타임스탬프 필드. |
| `{EVENT_DEFINITION}` | 이전 이벤트의 자격을 규정하는 표현식입니다. |
| `{TIME_UNIT}` | 출력 단위입니다. 가능한 값에는 일, 시간, 분 및 초가 포함됩니다. 기본적으로 값은 초입니다. |

`OVER()` 함수 내의 매개 변수에 대한 설명은 [window functions 섹션](#window-functions)에서 찾을 수 있습니다.

**쿼리 예**

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

**결과**

```console
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

지정된 샘플 쿼리의 경우 결과는 `average_minutes_since_registration` 열에 제공됩니다. `average_minutes_since_registration` 열 내의 값은 현재 이벤트와 이전 이벤트 간의 시간입니다. 시간 단위는 이전에 `{TIME_UNIT}`에 정의되어 있었습니다.

### 다음 일치 항목 간 시간

이 쿼리는 다음 일치 이벤트 뒤의 시간 단위를 나타내는 음수를 반환합니다. 일치하는 이벤트를 찾을 수 없으면 null이 반환됩니다.

**쿼리 구문**

```sql
TIME_BETWEEN_NEXT_MATCH({TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 매개 변수 | 설명 |
| --------- | ----------- |
| `{TIMESTAMP}` | 모든 이벤트에 채워진 데이터 세트에 있는 타임스탬프 필드. |
| `{EVENT_DEFINITION}` | 다음 이벤트의 자격을 규정하는 표현식입니다. |
| `{TIME_UNIT}` | (선택 사항) 출력 단위입니다. 가능한 값에는 일, 시간, 분 및 초가 포함됩니다. 기본적으로 값은 초입니다. |

`OVER()` 함수 내의 매개 변수에 대한 설명은 [window functions 섹션](#window-functions)에서 찾을 수 있습니다.

**쿼리 예**

```sql
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

**결과**

```console
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

지정된 샘플 쿼리의 경우 결과는 `average_minutes_until_order_confirmation` 열에 제공됩니다. `average_minutes_until_order_confirmation` 열 내의 값은 현재 이벤트와 다음 이벤트 간의 시간 차입니다. 시간 단위는 이전에 `{TIME_UNIT}`에 정의되어 있었습니다.

## 다음 단계

여기에 설명된 기능을 사용하여 [!DNL Query Service]을(를) 사용하여 자신의 [!DNL Experience Event] 데이터 세트에 액세스하는 쿼리를 작성할 수 있습니다. [!DNL Query Service]에서의 쿼리 작성에 대한 자세한 내용은 [쿼리 만들기](../best-practices/writing-queries.md)에 대한 설명서를 참조하십시오.

## 추가 리소스

다음 비디오에서는 Adobe Experience Platform 인터페이스와 PSQL 클라이언트에서 쿼리를 실행하는 방법을 보여 줍니다. 또한 이 비디오에서는 XDM 개체의 개별 속성과 관련된 예제와 Adobe 정의 함수를 사용하고 CREATE TABLE AS SELECT(CTAS SELECT) 를 사용합니다.

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)
