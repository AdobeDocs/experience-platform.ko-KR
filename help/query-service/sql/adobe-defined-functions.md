---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;adobe 정의 함수;sql;
solution: Experience Platform
title: 쿼리 서비스의 Adobe 정의 SQL 함수
description: 이 문서에서는 Adobe Experience Platform 쿼리 서비스에서 사용할 수 있는 Adobe 정의 함수에 대한 정보를 제공합니다.
exl-id: 275aa14e-f555-4365-bcd6-0dd6df2456b3
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '1468'
ht-degree: 2%

---

# 쿼리 서비스의 Adobe 정의 SQL 함수

Adobe 정의 함수(여기서는 ADF라고 함)는 [!DNL Experience Event] 데이터에 대해 일반적인 비즈니스 관련 작업을 수행하는 데 도움이 되는 Adobe Experience Platform Query Service의 미리 빌드된 함수입니다. 여기에는 Adobe Analytics에 있는 것과 같은 [세션화](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html?lang=ko) 및 [속성](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/attribution/overview.html?lang=ko)에 대한 함수가 포함됩니다.

이 문서에서는 [!DNL Query Service]에서 사용할 수 있는 Adobe 정의 함수에 대한 정보를 제공합니다.

>[!NOTE]
>
>ECID(Experience Cloud ID)는 MCID라고도 하며 네임스페이스에서 계속 사용됩니다.

## 창 함수 {#window-functions}

대부분의 비즈니스 논리는 고객의 접점을 수집하고 시간별로 주문해야 합니다. 이 지원은 [!DNL Spark] SQL에서 창 함수 형식으로 제공됩니다. 창 함수는 표준 SQL의 일부이며 다른 여러 SQL 엔진에서 지원됩니다.

창 함수는 합계를 갱신하고 정렬된 하위 집합의 각 행에 대해 단일 항목을 반환합니다. 가장 기본적인 집계 함수는 `SUM()`입니다. `SUM()`이(가) 내 행을 가져와서 합계 하나를 제공합니다. 대신 창에 `SUM()`을(를) 적용하여 창 함수로 변환하면 각 행의 누적 합계가 표시됩니다.

대부분의 [!DNL Spark] SQL 도우미는 해당 행의 상태가 추가된 상태에서 창의 각 행을 업데이트하는 창 함수입니다.

**쿼리 구문**

```sql
OVER ({PARTITION} {ORDER} {FRAME})
```

| 매개변수 | 설명 | 예 |
| --------- | ----------- | ------- |
| `{PARTITION}` | 열 또는 사용 가능한 필드를 기반으로 한 행의 하위 그룹. | `PARTITION BY endUserIds._experience.mcid.id` |
| `{ORDER}` | 하위 집합 또는 행의 순서를 지정하는 데 사용되는 열 또는 사용 가능한 필드입니다. | `ORDER BY timestamp` |
| `{FRAME}` | 분할 영역에 있는 행의 하위 그룹. | `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW` |

## 세션화

웹 사이트, 모바일 애플리케이션, 대화형 음성 응답 시스템 또는 기타 고객 상호 작용 채널에서 가져온 [!DNL Experience Event] 데이터로 작업할 때 관련 활동 기간에 이벤트를 그룹화할 수 있는지 확인하는 데 도움이 됩니다. 일반적으로 제품 조사, 청구서 결제, 계좌 잔액 확인, 애플리케이션 작성 등과 같은 활동을 유도하는 특정 의도가 있습니다.

이러한 그룹화 또는 데이터 세션화는 이벤트를 연결하여 고객 경험에 대한 더 많은 컨텍스트를 발견하는 데 도움이 됩니다.

Adobe Analytics의 세션화에 대한 자세한 내용은 [컨텍스트 인식 세션](https://experienceleague.adobe.com/docs/analytics/components/virtual-report-suites/vrs-mobile-visit-processing.html?lang=ko)에 대한 설명서를 참조하십시오.

**쿼리 구문**

```sql
SESS_TIMEOUT({TIMESTAMP}, {EXPIRATION_IN_SECONDS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{TIMESTAMP}` | 데이터 세트에 있는 타임스탬프 필드입니다. |
| `{EXPIRATION_IN_SECONDS}` | 현재 세션이 끝나고 새 세션이 시작되는 것을 확인하기 위해 이벤트 사이에 필요한 초 수입니다. |

`OVER()` 함수 내의 매개 변수에 대한 설명은 [window 함수 섹션](#window-functions)에 있습니다.

**예제 쿼리**

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

제공된 샘플 쿼리에 대한 결과는 `session` 열에 제공됩니다. `session` 열은 다음 구성 요소로 구성됩니다.

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| 매개 변수 | 설명 |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | 현재 레코드와 이전 레코드 간의 시간 차이(초)입니다. |
| `{NUM}` | 창 함수의 `PARTITION BY`에 정의된 키에 대한 고유 세션 번호(1부터 시작)입니다. |
| `{IS_NEW}` | 레코드가 세션의 첫 번째 레코드인지 여부를 식별하는 데 사용되는 부울입니다. |
| `{DEPTH}` | 세션 내 현재 레코드의 깊이입니다. |

### SESS_START_IF

이 쿼리는 현재 타임스탬프 및 지정된 표현식을 기반으로 현재 행에 대한 세션 상태를 반환하고 현재 행으로 새 세션을 시작합니다.

**쿼리 구문**

```sql
SESS_START_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{TIMESTAMP}` | 데이터 세트에 있는 타임스탬프 필드입니다. |
| `{TEST_EXPRESSION}` | 데이터의 필드를 확인할 표현식입니다. 예: `application.launches > 0`. |

`OVER()` 함수 내의 매개 변수에 대한 설명은 [window 함수 섹션](#window-functions)에 있습니다.

**예제 쿼리**

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

제공된 샘플 쿼리에 대한 결과는 `session` 열에 제공됩니다. `session` 열은 다음 구성 요소로 구성됩니다.

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| 매개 변수 | 설명 |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | 현재 레코드와 이전 레코드 간의 시간 차이(초)입니다. |
| `{NUM}` | 창 함수의 `PARTITION BY`에 정의된 키에 대한 고유 세션 번호(1부터 시작)입니다. |
| `{IS_NEW}` | 레코드가 세션의 첫 번째 레코드인지 여부를 식별하는 데 사용되는 부울입니다. |
| `{DEPTH}` | 세션 내 현재 레코드의 깊이입니다. |

### SESS_END_IF

이 쿼리는 현재 타임스탬프와 지정된 표현식을 기반으로 현재 행에 대한 세션 상태를 반환하고 현재 세션을 종료하고 다음 행에서 새 세션을 시작합니다.

**쿼리 구문**

```sql
SESS_END_IF({TIMESTAMP}, {TEST_EXPRESSION}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{TIMESTAMP}` | 데이터 세트에 있는 타임스탬프 필드입니다. |
| `{TEST_EXPRESSION}` | 데이터의 필드를 확인할 표현식입니다. 예: `application.launches > 0`. |

`OVER()` 함수 내의 매개 변수에 대한 설명은 [window 함수 섹션](#window-functions)에 있습니다.

**예제 쿼리**

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

제공된 샘플 쿼리에 대한 결과는 `session` 열에 제공됩니다. `session` 열은 다음 구성 요소로 구성됩니다.

```sql
({TIMESTAMP_DIFF}, {NUM}, {IS_NEW}, {DEPTH})
```

| 매개 변수 | 설명 |
| ---------- | ------------- |
| `{TIMESTAMP_DIFF}` | 현재 레코드와 이전 레코드 간의 시간 차이(초)입니다. |
| `{NUM}` | 창 함수의 `PARTITION BY`에 정의된 키에 대한 고유 세션 번호(1부터 시작)입니다. |
| `{IS_NEW}` | 레코드가 세션의 첫 번째 레코드인지 여부를 식별하는 데 사용되는 부울입니다. |
| `{DEPTH}` | 세션 내 현재 레코드의 깊이입니다. |


## 경로 지정

경로 지정을 사용하여 고객의 참여도를 이해하고, 경험의 의도된 단계가 설계대로 작동하는지 확인하고, 고객에게 영향을 미칠 수 있는 잠재적인 문제점을 식별할 수 있습니다.

다음 ADF는 이전 및 다음 관계에서 경로 지정 보기를 설정할 수 있도록 지원합니다. 이전 페이지와 다음 페이지를 만들거나 여러 이벤트를 단계별로 진행하여 경로 지정을 만들 수 있습니다.

### 이전 페이지

창 내에서 정의된 단계 수만큼 떨어진 특정 필드의 이전 값을 결정합니다. 예제에서 `WINDOW` 함수는 현재 행과 모든 후속 행을 보도록 ADF를 설정하는 `ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`의 프레임으로 구성됩니다.

**쿼리 구문**

```sql
PREVIOUS({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{KEY}` | 이벤트의 열 또는 필드. |
| `{SHIFT}` | (선택 사항) 현재 이벤트에서 벗어난 이벤트 수입니다. 기본값은 1입니다. |
| `{IGNORE_NULLS}` | (선택 사항) null `{KEY}` 값을 무시할지 여부를 나타내는 부울입니다. 기본적으로 값은 `false`입니다. |

`OVER()` 함수 내의 매개 변수에 대한 설명은 [window 함수 섹션](#window-functions)에 있습니다.

**예제 쿼리**

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

제공된 샘플 쿼리에 대한 결과는 `previous_page` 열에 제공됩니다. `previous_page` 열 내의 값은 ADF에 사용된 `{KEY}`을(를) 기반으로 합니다.

### 다음 페이지

정의된 단계 수만큼 떨어진 특정 필드의 다음 값을 결정합니다. 예제에서 `WINDOW` 함수는 현재 행과 모든 후속 행을 보도록 ADF를 설정하는 `ROWS BETWEEN CURRENT ROW AND UNBOUNDED FOLLOWING`의 프레임으로 구성됩니다.

**쿼리 구문**

```sql
NEXT({KEY}, {SHIFT}, {IGNORE_NULLS}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{KEY}` | 이벤트의 열 또는 필드. |
| `{SHIFT}` | (선택 사항) 현재 이벤트에서 벗어난 이벤트 수입니다. 기본값은 1입니다. |
| `{IGNORE_NULLS}` | (선택 사항) null `{KEY}` 값을 무시할지 여부를 나타내는 부울입니다. 기본적으로 값은 `false`입니다. |

`OVER()` 함수 내의 매개 변수에 대한 설명은 [window 함수 섹션](#window-functions)에 있습니다.

**예제 쿼리**

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

제공된 샘플 쿼리에 대한 결과는 `previous_page` 열에 제공됩니다. `previous_page` 열 내의 값은 ADF에 사용된 `{KEY}`을(를) 기반으로 합니다.

## 간격

간격(Time-between)을 사용하면 이벤트가 발생하기 전이나 후의 특정 기간 내에 잠재 고객 행동을 탐색할 수 있습니다.

### 이전 일치 항목 사이의 시간

이 쿼리는 이전 일치 이벤트가 표시된 이후 시간 단위를 나타내는 숫자를 반환합니다. 일치하는 이벤트가 없으면 null을 반환합니다.

**쿼리 구문**

```sql
TIME_BETWEEN_PREVIOUS_MATCH(
    {TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT})
    OVER ({PARTITION} {ORDER} {FRAME})
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{TIMESTAMP}` | 모든 이벤트에 채워진 데이터 세트에 있는 타임스탬프 필드입니다. |
| `{EVENT_DEFINITION}` | 이전 이벤트를 평가하는 표현식. |
| `{TIME_UNIT}` | 출력 단위입니다. 가능한 값에는 일, 시간, 분 및 초가 포함됩니다. 기본값은 초입니다. |

`OVER()` 함수 내의 매개 변수에 대한 설명은 [window 함수 섹션](#window-functions)에 있습니다.

**예제 쿼리**

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

제공된 샘플 쿼리에 대한 결과는 `average_minutes_since_registration` 열에 제공됩니다. `average_minutes_since_registration` 열 내의 값은 현재 이벤트와 이전 이벤트 간의 시간 차이입니다. 시간 단위는 `{TIME_UNIT}`에서 이전에 정의되었습니다.

### 다음 일치 사이의 시간

이 쿼리는 다음 일치 이벤트 이후의 시간 단위를 나타내는 음수를 반환합니다. 일치하는 이벤트를 찾을 수 없으면 null이 반환됩니다.

**쿼리 구문**

```sql
TIME_BETWEEN_NEXT_MATCH({TIMESTAMP}, {EVENT_DEFINITION}, {TIME_UNIT}) OVER ({PARTITION} {ORDER} {FRAME})
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `{TIMESTAMP}` | 모든 이벤트에 채워진 데이터 세트에 있는 타임스탬프 필드입니다. |
| `{EVENT_DEFINITION}` | 다음 이벤트를 평가하는 표현식. |
| `{TIME_UNIT}` | (선택 사항) 출력 단위입니다. 가능한 값에는 일, 시간, 분 및 초가 포함됩니다. 기본값은 초입니다. |

`OVER()` 함수 내의 매개 변수에 대한 설명은 [window 함수 섹션](#window-functions)에 있습니다.

**예제 쿼리**

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

제공된 샘플 쿼리에 대한 결과는 `average_minutes_until_order_confirmation` 열에 제공됩니다. `average_minutes_until_order_confirmation` 열 내의 값은 현재 이벤트와 다음 이벤트 간의 시간 차이입니다. 시간 단위는 `{TIME_UNIT}`에서 이전에 정의되었습니다.

## 다음 단계

여기에 설명된 함수를 사용하여 [!DNL Query Service]을(를) 사용하여 자신의 [!DNL Experience Event] 데이터 세트에 액세스하는 쿼리를 작성할 수 있습니다. [!DNL Query Service]에서 쿼리를 작성하는 방법에 대한 자세한 내용은 [쿼리 만들기](../best-practices/writing-queries.md)에 대한 설명서를 참조하십시오.

## 추가 리소스

다음 비디오는 Adobe Experience Platform 인터페이스 및 PSQL 클라이언트에서 쿼리를 실행하는 방법을 보여 줍니다. 또한 이 비디오에서는 Adobe 정의 함수 사용 및 CREATE TABLE AS SELECT(CTAS) 사용 시 XDM 개체의 개별 속성과 관련된 예제를 사용합니다.

>[!VIDEO](https://video.tv.adobe.com/v/32942?quality=12&learn=on&captions=kor)
