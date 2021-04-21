---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;쿼리 쓰기;쿼리 쓰기;;home;popular topics service;query;
solution: Experience Platform
title: 쿼리 서비스에서 쿼리 실행에 대한 일반 지침
topic-legacy: queries
type: Tutorial
description: 이 문서에서는 Adobe Experience Platform 쿼리 서비스에서 쿼리를 작성할 때 알아야 할 중요한 세부 사항을 자세히 설명합니다.
exl-id: a7076c31-8f7c-455e-9083-cbbb029c93bb
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 3%

---

# [!DNL Query Service]에서 쿼리 실행에 대한 일반 지침

이 문서에서는 Adobe Experience Platform [!DNL Query Service]에서 쿼리를 작성할 때 알아야 할 중요한 세부 정보를 자세히 설명합니다.

[!DNL Query Service]에 사용된 SQL 구문에 대한 자세한 내용은 [SQL 구문 설명서](../sql/syntax.md)를 참조하십시오.

## 쿼리 실행 모델

Adobe Experience Platform [!DNL Query Service]에는 쿼리 실행 모델이 두 개 있습니다.인터랙티브한 요소와 비인터랙티브한 요소가 포함되어 있습니다. 대화형 실행은 비즈니스 인텔리전스 도구의 쿼리 개발 및 보고서 생성에 사용되는 반면, 비대화형 실행은 데이터 처리 워크플로의 일부로서 더 큰 작업과 운영 쿼리에 사용됩니다.

### 대화형 쿼리 실행

쿼리는 연결된 클라이언트](../clients/overview.md)를 통해 [!DNL Query Service] UI 또는 [를 통해 제출하여 대화식으로 실행할 수 있습니다. 연결된 클라이언트를 통해 [!DNL Query Service]을(를) 실행할 때 제출된 쿼리가 반환되거나 시간 초과될 때까지 클라이언트와 [!DNL Query Service] 사이에 활성 세션이 실행됩니다.

대화형 쿼리 실행에는 다음과 같은 제한이 있습니다.

| 매개 변수 | 제한 사항 |
| --------- | ---------- |
| 쿼리 시간 초과 | 10분 |
| 반환된 최대 행 수 | 50,000 |
| 최대 동시 쿼리 수 | 5 |

>[!NOTE]
>
>최대 행 제한을 무시하려면 쿼리에 `LIMIT 0`을(를) 포함하십시오. 쿼리 시간 초과(10분)는 여전히 적용됩니다.

기본적으로 대화형 쿼리의 결과는 클라이언트에 반환되며 **이(가) 지속되지 않습니다.** 결과를 [!DNL Experience Platform]의 데이터 집합으로 유지하려면 쿼리는 `CREATE TABLE AS SELECT` 구문을 사용해야 합니다.

### 비대화형 쿼리 실행

[!DNL Query Service] API를 통해 제출된 쿼리는 대화식으로 실행되지 않습니다. 비대화형 실행은 [!DNL Query Service]이(가) API 호출을 수신한 순서대로 쿼리를 실행함을 의미합니다. 비대화형 쿼리는 항상 결과를 받기 위해 [!DNL Experience Platform]에 새 데이터 세트를 만들거나 기존 데이터 세트에 새 행을 삽입하게 됩니다.

## 개체 내의 특정 필드에 액세스

쿼리의 개체 내의 필드에 액세스하려면 도트 표기법(`.`) 또는 대괄호 표기법(`[]`)을 사용할 수 있습니다. 다음 SQL 문은 도트 표기법을 사용하여 `endUserIds` 개체를 `mcid` 개체 아래로 탐색합니다.

```sql
SELECT endUserIds._experience.mcid
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

| 속성 | 설명 |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | 분석 테이블의 이름입니다. |

다음 SQL 문은 대괄호 표기법을 사용하여 `endUserIds` 개체를 `mcid` 개체 아래로 탐색합니다.

```sql
SELECT endUserIds['_experience']['mcid']
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

| 속성 | 설명 |
| -------- | ----------- |
| `{ANALYTICS_TABLE_NAME}` | 분석 테이블의 이름입니다. |

>[!NOTE]
>
>각 표기법 유형은 동일한 결과를 반환하므로 사용자가 선택하는 표기법은 사용자의 기본 설정에 따라 달라집니다.

위의 두 예제 쿼리 모두 단일 값이 아닌 분리된 객체를 반환합니다.

```console
              endUserIds._experience.mcid   
--------------------------------------------------------
 (48168239533518554367684086979667672499,"(ECID)",true)
(1 row)
```

반환된 `endUserIds._experience.mcid` 객체에는 다음 매개 변수에 해당하는 값이 포함되어 있습니다.

- `id`
- `namespace`
- `primary`

열을 객체로만 선언하면 전체 객체를 문자열로 반환합니다. ID만 보려면 다음을 사용합니다.

```sql
SELECT endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE endUserIds._experience.mcid IS NOT NULL
LIMIT 1
```

```console
     endUserIds._experience.mcid.id 
----------------------------------------
 48168239533518554367684086979667672499
(1 row)
```

## 따옴표

단일 따옴표, 큰따옴표 및 큰따옴표는 쿼리 서비스 쿼리 내에서 서로 다른 용도로 사용됩니다.

### 작은 따옴표

단일 따옴표(`'`)는 텍스트 문자열을 만드는 데 사용됩니다. 예를 들어 `SELECT` 문에서 이 값을 사용하여 결과의 정적 텍스트 값을 반환하고 `WHERE` 절에서 열의 컨텐츠를 평가할 수 있습니다.

다음 쿼리는 열에 대한 정적 텍스트 값(`'datasetA'`)을 선언합니다.

```sql
SELECT 
  'datasetA',
  timestamp,
  web.webPageDetails.name
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

다음 쿼리는 WHERE 절에 단일 인용 부호 문자열(`'homepage'`)을 사용하여 특정 페이지에 대한 이벤트를 반환합니다.

```sql
SELECT 
  timestamp,
  endUserIds._experience.mcid.id
FROM {ANALYTICS_TABLE_NAME}
WHERE web.webPageDetails.name = 'homepage'
LIMIT 10
```

### 큰따옴표

큰따옴표(`"`)는 공백이 있는 식별자를 선언하는 데 사용됩니다.

다음 쿼리는 한 열에 해당 식별자의 공백이 포함된 경우 지정된 열의 값을 반환하기 위해 큰따옴표를 사용합니다.

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
>이중 따옴표(**은(는) 도트 표기법 필드 액세스에는 사용할 수 없습니다.**)

### 인용 부호

도트 표기법 구문을 사용할 때 `` ` `` 뒤의 따옴표는 예약된 열 이름 **만**&#x200B;에서 escape하는 데 사용됩니다. 예를 들어 `order`은(는) SQL의 예약어이므로 `commerce.order` 필드에 액세스하려면 백 따옴표를 사용해야 합니다.

```sql
SELECT 
  commerce.`order`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

백따옴표 역시 숫자로 시작하는 필드에 액세스하는 데 사용됩니다. 예를 들어 필드 `30_day_value`에 액세스하려면 뒤에 따옴표 표기법을 사용해야 합니다.

```SQL
SELECT
    commerce.`30_day_value`
FROM {ANALYTICS_TABLE_NAME}
LIMIT 10
```

대괄호 표기법을 사용하는 경우 인용 부호는 **필요하지 않습니다.**

```sql
 SELECT
  commerce['order']
 FROM {ANALYTICS_TABLE_NAME}
 LIMIT 10
```

## 테이블 정보 보기

쿼리 서비스에 연결한 후 `\d` 또는 `SHOW TABLES` 명령을 사용하여 플랫폼에서 사용 가능한 모든 테이블을 볼 수 있습니다.

### 표준 표 보기

`\d` 명령은 테이블 나열을 위한 표준 PostgreSQL 보기를 보여줍니다. 이 명령 출력의 예는 아래에 나와 있습니다.

```sql
             List of relations
 Schema |       Name      | Type  |  Owner   
--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

### 세부 테이블 보기

`SHOW TABLES` command는 표에 대한 자세한 정보를 제공하는 사용자 정의 명령입니다. 이 명령 출력의 예는 아래에 나와 있습니다.

```sql
       name      |        dataSetId         |     dataSet    | description | resolved 
-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

### 스키마 정보

테이블 내의 스키마에 대한 자세한 정보를 보려면 `\d {TABLE_NAME}` 명령을 사용할 수 있습니다. 여기서 `{TABLE_NAME}`은 스키마 정보를 보려는 테이블의 이름입니다.

다음 예제에서는 `\d luma_midvalues`을 사용하여 볼 수 있는 `luma_midvalues` 테이블의 스키마 정보를 보여 줍니다.

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

또한 테이블 이름에 열 이름을 추가하여 특정 열에 대한 추가 정보를 얻을 수 있습니다. 이 형식은 `\d {TABLE_NAME}_{COLUMN}` 형식으로 작성됩니다.

다음 예제에서는 `web` 열에 대한 추가 정보를 보여 주고 다음 명령을 사용하여 호출할 수 있습니다.`\d luma_midvalues_web`:

```sql
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```

## 데이터 집합 참여

여러 데이터 세트를 함께 결합하여 쿼리에 다른 데이터 세트의 데이터를 포함할 수 있습니다.

다음 예제에서는 다음 두 데이터 집합(`your_analytics_table` 및 `custom_operating_system_lookup`)을 결합하고 페이지 보기 횟수로 상위 50개 운영 체제에 대한 `SELECT` 문을 만듭니다.

**쿼리**

```sql
SELECT 
  b.operatingsystem AS OperatingSystem,
  SUM(a.web.webPageDetails.pageviews.value) AS PageViews
FROM your_analytics_table a 
     JOIN custom_operating_system_lookup b 
      ON a._experience.analytics.environment.operatingsystemID = b.operatingsystemid 
WHERE TIMESTAMP >= ('2018-01-01') AND TIMESTAMP <= ('2018-12-31')
GROUP BY OperatingSystem 
ORDER BY PageViews DESC
LIMIT 50;
```

**결과**

| 운영 체제 | 페이지 보기 횟수 |
| --------------- | --------- |
| Windows 7 | 2781979.0 |
| Windows XP | 1669824.0 |
| Windows 8 | 420024.0 |
| Adobe AIR | 31,5032.0 |
| Windows Vista | 1735.66.0 |
| Mobile iOS 6.1.3 | 119069.0 |
| Linux | 56,516.0 |
| OSX 10.6.8 | 53,652.0 |
| Android 4.0.4 | 46,167.0 |
| Android 4.0.3 | 31,852.0 |
| Windows Server 2003 및 XP x64 Edition | 28,83.0 |
| Android 4.1.1 | 243.36.0 |
| Android 2.3.6 | 15,735.0 |
| OSX 10.6 | 13,357.0 |
| Windows Phone 7.5 | 11,054.0 |
| Android 4.3 | 921.0 |

## 중복 제거

쿼리 서비스는 데이터 중복 제거 또는 중복 행을 데이터에서 제거할 수 있도록 지원합니다. 데이터 중복 제거에 대한 자세한 내용은 [쿼리 서비스 데이터 중복 제거 안내서](./deduplication.md)를 참조하십시오.

## 다음 단계

이 문서를 읽으면 [!DNL Query Service]을(를) 사용하여 쿼리를 작성할 때 몇 가지 중요한 고려 사항을 알게 됩니다. SQL 구문을 사용하여 고유한 쿼리를 작성하는 방법에 대한 자세한 내용은 [SQL 구문 설명서](../sql/syntax.md)를 참조하십시오.

쿼리 서비스 내에서 사용할 수 있는 쿼리 샘플에 대한 자세한 내용은 [Adobe Analytics 샘플 쿼리](./adobe-analytics.md), [Adobe Target 샘플 쿼리](./adobe-target.md) 또는 [ExperienceEvent 샘플 쿼리](./experience-event-queries.md)에 대한 설명서를 참조하십시오.
