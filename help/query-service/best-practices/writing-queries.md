---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;쿼리 작성;쿼리 작성;
solution: Experience Platform
title: 쿼리 서비스의 쿼리 실행에 대한 일반 지침
type: Tutorial
description: 이 문서에서는 Adobe Experience Platform 쿼리 서비스에서 쿼리를 작성할 때 알아야 할 중요한 세부 사항에 대해 간략하게 설명합니다.
exl-id: a7076c31-8f7c-455e-9083-cbbb029c93bb
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 2%

---

# [!DNL Query Service]의 쿼리 실행에 대한 일반 지침

이 문서에서는 Adobe Experience Platform [!DNL Query Service]에서 쿼리를 작성할 때 알아야 할 중요한 세부 정보를 자세히 설명합니다.

[!DNL Query Service]에 사용된 SQL 구문에 대한 자세한 내용은 [SQL 구문 설명서](../sql/syntax.md)를 참조하십시오.

## 쿼리 실행 모델

Adobe Experience Platform [!DNL Query Service]에는 대화형 및 비대화형 두 가지 쿼리 실행 모델이 있습니다. 대화형 실행은 비즈니스 인텔리전스 도구에서 쿼리 개발 및 보고서 생성에 사용되며, 비대화형 실행은 데이터 처리 워크플로우의 일부로 더 큰 작업 및 운영 쿼리에 사용됩니다.

### 대화형 쿼리 실행

쿼리는 [!DNL Query Service] UI를 통해 제출하거나 [연결된 클라이언트를 통해 제출](../clients/overview.md)하여 대화식으로 실행할 수 있습니다. 연결된 클라이언트를 통해 [!DNL Query Service]을(를) 실행하는 경우 제출된 쿼리가 반환되거나 시간이 초과될 때까지 클라이언트와 [!DNL Query Service] 간에 활성 세션이 실행됩니다.

대화형 쿼리 실행에는 다음과 같은 제한 사항이 있습니다.

| 매개변수 | 제한 사항 |
| --------- | ---------- |
| 쿼리 시간 제한 | 10분 |
| 반환된 최대 행 수 | 50,000 |
| 최대 동시 쿼리 | 5 |

>[!NOTE]
>
>최대 행 제한을 재정의하려면 쿼리에 `LIMIT 0`을(를) 포함합니다. 쿼리 제한 시간 10분이 계속 적용됩니다.

기본적으로 대화형 쿼리의 결과는 클라이언트에 반환되고 **지속되지 않습니다**. [!DNL Experience Platform]에서 결과를 데이터 집합으로 유지하려면 쿼리에서 `CREATE TABLE AS SELECT` 구문을 사용해야 합니다.

### 비대화형 쿼리 실행

[!DNL Query Service] API를 통해 제출된 쿼리는 비대화식으로 실행됩니다. 비대화형 실행은 [!DNL Query Service]이(가) API 호출을 수신하고 쿼리를 받은 순서대로 실행함을 의미합니다. 비대화형 쿼리는 항상 결과를 받기 위해 [!DNL Experience Platform]에서 새 데이터 집합을 생성하거나 기존 데이터 집합에 새 행을 삽입합니다.

## 객체 내의 특정 필드 액세스

쿼리의 개체 내에 있는 필드에 액세스하려면 점 표기법(`.`) 또는 대괄호 표기법(`[]`)을 사용할 수 있습니다. 다음 SQL 문은 점 표기법을 사용하여 `endUserIds` 개체를 `mcid` 개체로 내보냅니다.

>[!NOTE]
>
>ECID(Experience Cloud ID)는 MCID라고도 하며 네임스페이스에서 계속 사용됩니다.

```sql
SELECT endUserIds._experience.mcid
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 1
```

| 속성 | 설명 |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | Analytics 테이블의 이름입니다. |

다음 SQL 문은 대괄호 표기법을 사용하여 `endUserIds` 개체를 `mcid` 개체로 내보냅니다.

```sql
SELECT endUserIds['_experience']['mcid']
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 1
```

| 속성 | 설명 |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | Analytics 테이블의 이름입니다. |

>[!NOTE]
>
>각 표기법 유형은 동일한 결과를 반환하므로 사용자가 선택하는 것은 사용자 환경 설정에 따라 다릅니다.

위의 두 예제 쿼리는 모두 단일 값이 아닌 병합된 개체를 반환합니다.

```console
              endUserIds._experience.mcid   
--------------------------------------------------------
 (48168239533518554367684086979667672499,"(ECID)",true)
(1 row)
```

반환된 `endUserIds._experience.mcid` 개체에 다음 매개 변수에 해당하는 값이 포함되어 있습니다.

- `id`
- `namespace`
- `primary`

열이 개체 아래로 선언된 경우에만 전체 개체가 문자열로 반환됩니다. ID만 보려면 다음을 사용합니다.

```sql
SELECT endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 1
```

```console
     endUserIds._experience.mcid.id 
----------------------------------------
 48168239533518554367684086979667672499
(1 row)
```

## 따옴표

작은따옴표, 큰따옴표 및 큰따옴표는 쿼리 서비스 쿼리 내에서 사용하는 용도가 다릅니다.

### 작은 따옴표

작은 따옴표(`'`)를 사용하여 텍스트 문자열을 만듭니다. 예를들어, `SELECT` 문에서는 결과에 정적 텍스트 값을 반환하고 `WHERE` 절에서는 열의 내용을 평가하는 데 사용할 수 있습니다.

다음 쿼리는 열에 대한 정적 텍스트 값(`'datasetA'`)을 선언합니다.

```sql
SELECT 
  'datasetA',
  timestamp,
  web.webPageDetails.name
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

다음 쿼리는 WHERE 절에서 작은따옴표 문자열(`'homepage'`)을 사용하여 특정 페이지에 대한 이벤트를 반환합니다.

```sql
SELECT 
  timestamp,
  endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE web.webPageDetails.name = 'homepage'
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

### 큰따옴표

큰따옴표(`"`)를 사용하여 식별자를 공백으로 선언합니다.

다음 쿼리는 하나의 열에 식별자에 공백이 있을 때 큰따옴표를 사용하여 지정된 열의 값을 반환합니다.

```sql
SELECT
  no_space_column,
  "space column"
FROM
( SELECT 
    'column1' as no_space_column,
    'column2' as "space column"
)
```

>[!NOTE]
>
>점 표기법 필드 액세스에는 큰따옴표 **을(를) 사용할 수 없습니다**.

### 역따옴표

점 표기법 구문을 사용할 때 **only** 예약된 열 이름을 이스케이프 처리하는 데 역따옴표 `` ` ``이(가) 사용됩니다. 예를 들어 `order`은(는) SQL에서 예약어이므로 `commerce.order` 필드에 액세스하려면 역따옴표를 사용해야 합니다.

```sql
SELECT 
  commerce.`order`
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

역따옴표는 숫자로 시작하는 필드에 액세스하는 데에도 사용됩니다. 예를 들어 `30_day_value` 필드에 액세스하려면 역따옴표 표기법을 사용해야 합니다.

```SQL
SELECT
    commerce.`30_day_value`
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

대괄호 표기법을 사용하는 경우 **not**&#x200B;이 필요합니다.

```sql
 SELECT
  commerce['order']
 FROM {ANALYTICS_TABLE_NAME}
 WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
 LIMIT 10
```

## 테이블 정보 보기

쿼리 서비스에 연결한 후 `\d` 또는 `SHOW TABLES` 명령을 사용하여 플랫폼에서 사용 가능한 모든 테이블을 볼 수 있습니다.

### 표준 테이블 보기

`\d` 명령은 목록 테이블에 대한 표준 [!DNL PostgreSQL] 보기를 표시합니다. 이 명령의 출력 예는 다음과 같습니다.

```sql
             List of relations
 Schema |       Name      | Type  |  Owner   
--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

### 자세한 테이블 보기

`SHOW TABLES` 명령은 테이블에 대한 자세한 정보를 제공하는 사용자 지정 명령입니다. 이 명령의 출력 예는 다음과 같습니다.

```sql
       name      |        dataSetId         |     dataSet    | description | resolved 
-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

### 스키마 정보

테이블 내의 스키마에 대한 자세한 정보를 보려면 `\d {TABLE_NAME}` 명령을 사용할 수 있습니다. 여기서 `{TABLE_NAME}`은(는) 보려는 스키마 정보가 있는 테이블의 이름입니다.

다음 예제에서는 `\d luma_midvalues`을(를) 사용하여 표시되는 `luma_midvalues` 테이블에 대한 스키마 정보를 보여 줍니다.

```sql
                         Table "public.luma_midvalues"
      Column       |             Type            | Collation | Nullable | Default 
-------------------+-----------------------------+-----------+----------+---------
 timestamp         | timestamp                   |           |          | 
 _id               | text                        |           |          | 
 productlistitems  | anyarray                    |           |          | 
 commerce          | luma_midvalues_commerce     |           |          | 
 receivedtimestamp | timestamp                   |           |          | 
 enduserids        | luma_midvalues_enduserids   |           |          | 
 datasource        | datasource                  |           |          | 
 web               | luma_midvalues_web          |           |          | 
 placecontext      | luma_midvalues_placecontext |           |          | 
 identitymap       | anymap                      |           |          | 
 marketing         | marketing                   |           |          | 
 environment       | luma_midvalues_environment  |           |          | 
 _experience       | luma_midvalues__experience  |           |          | 
 device            | device                      |           |          | 
 search            | search                      |           |          | 
```

또한 테이블 이름에 열의 이름을 추가하여 특정 열에 대한 추가 정보를 얻을 수 있습니다. 이 형식은 `\d {TABLE_NAME}_{COLUMN}` 형식으로 작성됩니다.

다음 예제에서는 `web` 열에 대한 추가 정보를 보여 주며 다음 명령을 사용하여 호출됩니다. `\d luma_midvalues_web`:

```sql
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```

## 데이터 세트 연결

여러 데이터 세트를 함께 연결하여 쿼리에 다른 데이터 세트의 데이터를 포함할 수 있습니다.

다음 예제에서는 다음 두 데이터 세트(`your_analytics_table` 및 `custom_operating_system_lookup`)를 결합하고 페이지 보기 수로 상위 50개 운영 체제에 대한 `SELECT` 문을 만듭니다.

**쿼리**

```sql
SELECT 
  b.operatingsystem AS OperatingSystem,
  SUM(a.web.webPageDetails.pageviews.value) AS PageViews
FROM your_analytics_table a 
     JOIN custom_operating_system_lookup b 
      ON a._experience.analytics.environment.operatingsystemID = b.operatingsystemid 
WHERE TIMESTAMP >= TO_TIMESTAMP('2018-01-01') AND TIMESTAMP <= TO_TIMESTAMP('2018-12-31')
GROUP BY OperatingSystem 
ORDER BY PageViews DESC
LIMIT 50;
```

**결과**

| 운영 체제 | PageViews |
| --------------- | --------- |
| 윈도우 | 2781979.0 |
| 윈도 | 1669824.0 |
| 윈도우 | 420024.0 |
| Adobe AIR | 315032.0 |
| 윈도우 비스타 | 173566.0 |
| Mobile iOS 6.1.3 | 119069.0 |
| Linux | 56516.0 |
| OSX 10.6.8 | 53652.0 |
| Android 4.0.4 | 46167.0 |
| Android 4.0.3 | 31852.0 |
| Windows Server 2003 및 XP x64 Edition | 28883.0 |
| Android 4.1.1 | 24336.0 |
| Android 2.3.6 | 15735.0 |
| OSX 10.6 | 13357.0 |
| 윈도우 폰 . | 11054.0 |
| Android 4.3 | 9221.0 |

## 중복 제거

쿼리 서비스는 데이터 중복 제거 또는 데이터에서 중복 행 제거를 지원합니다. 중복 제거에 대한 자세한 내용은 [쿼리 서비스 중복 제거 안내서](../key-concepts/deduplication.md)를 참조하십시오.

## 쿼리 서비스의 시간대 계산

쿼리 서비스는 UTC 타임스탬프 형식을 사용하여 Adobe Experience Platform의 지속 데이터를 표준화합니다. 표준 시간대 요구 사항을 UTC 타임스탬프와 주고받는 방법에 대한 자세한 내용은 표준 시간대를 UTC 타임스탬프와 주고받는 방법에 대한 [FAQ 섹션](../troubleshooting-guide.md#How-do-I-change-the-time-zone-to-and-from-a-UTC-Timestamp?)을 참조하십시오.

## 다음 단계

이 문서를 읽으면 [!DNL Query Service]을(를) 사용하여 쿼리를 작성할 때 몇 가지 중요한 고려 사항을 알게 됩니다. SQL 구문을 사용하여 고유한 쿼리를 작성하는 방법에 대한 자세한 내용은 [SQL 구문 설명서](../sql/syntax.md)를 참조하십시오.

Query Service 내에서 사용할 수 있는 쿼리의 더 많은 샘플은 다음 사용 사례 설명서를 참조하십시오.

- [Analytics 인사이트](../use-cases/analytics-insights.md)
- [이벤트의 트렌드 보고서 만들기](../use-cases/trended-report-of-events.md)
- [방문자의 롤업 보고서 보기](../use-cases/roll-up-report-of-a-visitor.md)
- [사용자의 페이지 보기 나열](../use-cases/list-visitor-sessions.md)
- [페이지 보기 횟수별 방문자 나열](../use-cases/visitors-by-number-of-page-views.md)
