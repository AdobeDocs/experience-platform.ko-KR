---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;쿼리 작성;쿼리 작성;
solution: Experience Platform
title: Query Service의 쿼리 실행에 대한 일반 지침
topic-legacy: queries
type: Tutorial
description: 이 문서에서는 Adobe Experience Platform Query Service에서 쿼리를 작성할 때 알아야 할 중요한 세부 정보에 대해 설명합니다.
exl-id: a7076c31-8f7c-455e-9083-cbbb029c93bb
source-git-commit: 9c450f340706040593dfea5292702c4b00dd9852
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 3%

---

# 의 쿼리 실행에 대한 일반 지침 [!DNL Query Service]

이 문서에서는 Adobe Experience Platform에서 쿼리를 작성할 때 알아야 할 중요한 세부 정보에 대해 자세히 설명합니다 [!DNL Query Service].

에서 사용되는 SQL 구문에 대한 자세한 내용은 [!DNL Query Service]을(를) 참조하십시오. [SQL 구문 설명서](../sql/syntax.md).

## 쿼리 실행 모델

Adobe Experience Platform [!DNL Query Service] 에는 쿼리 실행 모델이 두 개 있습니다. 대화형 및 비대화형. 대화형 실행은 비즈니스 인텔리전스 도구에서 쿼리 개발 및 보고서 생성에 사용되는 반면, 비대화형 실행은 데이터 처리 워크플로우의 일부로서 더 큰 작업 및 운영 쿼리에 사용됩니다.

### 대화형 쿼리 실행

쿼리는 를 통해 제출함으로써 상호 작용 방식으로 실행할 수 있습니다 [!DNL Query Service] UI 또는 [연결된 클라이언트 사용](../clients/overview.md). 실행 시 [!DNL Query Service] 연결된 클라이언트를 통해 클라이언트와 [!DNL Query Service] 제출된 쿼리가 반환되거나 시간 초과될 때까지

대화형 쿼리 실행에는 다음과 같은 제한 사항이 있습니다.

| 매개 변수 | 제한 사항 |
| --------- | ---------- |
| 쿼리 시간 초과 | 10분 |
| 반환된 최대 행 수 | 50,000 |
| 최대 동시 쿼리 | 5 |

>[!NOTE]
>
>최대 행 제한을 무시하려면 다음을 포함합니다 `LIMIT 0` 참조하십시오. 10분의 쿼리 시간 제한이 계속 적용됩니다.

기본적으로 대화형 쿼리의 결과는 클라이언트에 반환되고 **not** 지속됩니다. 결과를 의 데이터 세트로 유지하려면 [!DNL Experience Platform]를 채울 때는 `CREATE TABLE AS SELECT` 구문

### 비대화형 쿼리 실행

를 통해 제출된 쿼리 [!DNL Query Service] API는 대화식으로 실행되지 않습니다. 비대화형 실행은 [!DNL Query Service] 는 API 호출을 수신하고 수신된 순서로 쿼리를 실행합니다. 비대화형 쿼리는 항상 [!DNL Experience Platform] 를 입력하여 기존 데이터 세트에 새 행을 삽입하거나 결과를 수신합니다.

## 개체 내의 특정 필드에 액세스

쿼리의 개체 내에 필드에 액세스하려면 점 표기법(`.`) 또는 대괄호 표기법( )`[]`). 다음 SQL 문은 점 표기법을 사용하여 `endUserIds` 개체 아래로 `mcid` 개체.

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
| `{ANALYTICS_TABLE_NAME}` | 분석 테이블의 이름입니다. |

다음 SQL 문은 대괄호 표기법을 사용하여 `endUserIds` 개체 아래로 `mcid` 개체.

```sql
SELECT endUserIds['_experience']['mcid']
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
AND TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 1
```

| 속성 | 설명 |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | 분석 테이블의 이름입니다. |

>[!NOTE]
>
>각 표기법 유형은 동일한 결과를 반환하므로 사용자가 선택하는 표기법은 기본 설정에 따라 다릅니다.

위의 두 예제 쿼리는 모두 단일 값이 아닌 병합된 개체를 반환합니다.

```console
              endUserIds._experience.mcid   
--------------------------------------------------------
 (48168239533518554367684086979667672499,"(ECID)",true)
(1 row)
```

반환된 `endUserIds._experience.mcid` 객체에는 다음 매개 변수에 대한 해당 값이 포함되어 있습니다.

- `id`
- `namespace`
- `primary`

열을 객체로만 선언하면 전체 객체를 문자열로 반환합니다. ID만 보려면 다음을 사용합니다.

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

작은 따옴표, 큰 따옴표 및 작은 따옴표는 Query Service 쿼리 내에서 서로 다른 사용 방식을 사용합니다.

### 작은 따옴표

작은 따옴표(`'`)을 사용하여 텍스트 문자열을 만듭니다. 예를 들어 `SELECT` 결과에 정적 텍스트 값을 반환하고 `WHERE` 열의 내용을 평가하는 절

다음 쿼리는 정적 텍스트 값을 선언합니다(`'datasetA'`) 내의 아무 곳에나 삽입할 수 있습니다.

```sql
SELECT 
  'datasetA',
  timestamp,
  web.webPageDetails.name
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

다음 쿼리는 단일 인용 문자열(`'homepage'`)을 클릭하여 특정 페이지에 대한 이벤트를 반환합니다.

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

큰따옴표(`"`)은 공백이 있는 식별자를 선언하는 데 사용됩니다.

다음 쿼리는 한 열에 해당 식별자의 공백이 포함되어 있으면 지정된 열의 값을 반환하기 위해 큰따옴표를 사용합니다.

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
>큰따옴표 **사용할 수 없음** 점 표기법 필드 액세스와 함께 사용됩니다.

### 뒷따옴표

뒷따옴표 `` ` `` 예약된 열 이름을 이스케이프 처리하는 데 사용됩니다. **전용** 점 표기법 구문을 사용할 때 예를 들어 다음 이후 `order` 는 SQL에서 예약된 단어이므로, 뒷따옴표를 사용하여 필드에 액세스해야 합니다 `commerce.order`:

```sql
SELECT 
  commerce.`order`
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

역따옴표 는 숫자로 시작하는 필드에 액세스하는 데에도 사용됩니다. 예를 들어 필드에 액세스하려면 `30_day_value`이전 따옴표 표기법을 사용해야 합니다.

```SQL
SELECT
    commerce.`30_day_value`
FROM {ANALYTICS_TABLE_NAME}
WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
LIMIT 10
```

뒷따옴표 **not** 대괄호 표기법을 사용하는 경우 필요합니다.

```sql
 SELECT
  commerce['order']
 FROM {ANALYTICS_TABLE_NAME}
 WHERE TIMESTAMP = to_timestamp('{TARGET_YEAR}-{TARGET_MONTH}-{TARGET_DAY}')
 LIMIT 10
```

## 테이블 정보 보기

Query Service에 연결한 후에는 `\d` 또는 `SHOW TABLES` 명령.

### 표준 표 보기

다음 `\d` 명령은 표준 [!DNL PostgreSQL] 목록 테이블에 대한 보기. 이 명령의 출력의 예는 다음과 같습니다.

```sql
             List of relations
 Schema |       Name      | Type  |  Owner   
--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

### 자세한 테이블 보기

`SHOW TABLES` 명령은 테이블에 대한 자세한 정보를 제공하는 사용자 지정 명령입니다. 이 명령의 출력의 예는 다음과 같습니다.

```sql
       name      |        dataSetId         |     dataSet    | description | resolved 
-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

### 스키마 정보

테이블 내의 스키마에 대한 자세한 정보를 보려면 `\d {TABLE_NAME}` 명령, 위치 `{TABLE_NAME}` 는 스키마 정보를 보려는 테이블의 이름입니다.

다음 예제는 `luma_midvalues` 표. `\d luma_midvalues`:

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

또한 테이블 이름에 열 이름을 추가하여 특정 열에 대한 추가 정보를 얻을 수 있습니다. 형식으로 작성됩니다 `\d {TABLE_NAME}_{COLUMN}`.

다음 예제는 `web` 열, 및 는 다음 명령을 사용하여 호출됩니다. `\d luma_midvalues_web`:

```sql
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```

## 데이터 세트 가입

여러 데이터 세트를 함께 조인하여 쿼리에 다른 데이터 세트의 데이터를 포함할 수 있습니다.

다음 예제에서는 다음 두 데이터 세트(`your_analytics_table` 및 `custom_operating_system_lookup`)를 만들어 `SELECT` 페이지 보기 횟수별 상위 50개 운영 체제에 대한 문입니다.

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

| 운영 체제 | 페이지 보기 수 |
| --------------- | --------- |
| Windows 7 | 2781979.0 |
| Windows XP | 1669824.0 |
| Windows 8 | 420024.0 |
| Adobe AIR | 315032.0 |
| Windows Vista | 173566.0 |
| Mobile iOS 6.1.3 | 119069.0 |
| Linux | 56516.0 |
| OSX 10.6.8 | 53652.0 |
| Android 4.0.4 | 46167.0 |
| Android 4.0.3 | 31852.0 |
| Windows Server 2003 및 XP x64 Edition | 28883.0 |
| Android 4.1.1 | 24336.0 |
| Android 2.3.6 | 15735.0 |
| OSX 10.6 | 13357.0 |
| Windows Phone 7.5 | 11054.0 |
| Android 4.3 | 921.0 |

## 중복 제거

Query Service는 데이터 중복 제거를 지원하거나 데이터에서 중복 행을 제거할 수 있습니다. 중복 제거에 대한 자세한 내용은 [Query Service 중복 제거 안내서](./deduplication.md).

## 쿼리 서비스의 시간대 계산

Query Service는 UTC 타임스탬프 형식을 사용하여 Adobe Experience Platform에서 지속된 데이터를 표준화합니다. 표준 시간대 요구 사항을 UTC 타임스탬프로 변환하는 방법에 대한 자세한 내용은 다음을 참조하십시오 [FAQ 섹션: UTC 타임스탬프에서 시간대를 변경하는 방법](../troubleshooting-guide.md#How-do-I-change-the-time-zone-to-and-from-a-UTC-Timestamp?).

## 다음 단계

이 문서를 읽은 후에는 [!DNL Query Service]. SQL 구문을 사용하여 쿼리를 작성하는 방법에 대한 자세한 내용은 [SQL 구문 설명서](../sql/syntax.md).

Query Service에서 사용할 수 있는 쿼리 샘플을 더 보려면 다음 사용 사례 설명서를 참조하십시오.

- [Analytics 통찰력](../use-cases/analytics-insights.md)
- [Adobe Target을 사용한 활동 분석](../use-cases/activity-analysis-with-adobe-target.md)
- [ExperienceEvent 샘플 쿼리](../sample-queries/experience-event.md).
