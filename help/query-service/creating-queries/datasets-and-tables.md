---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 데이터 세트와 테이블 및 스키마 비교
topic: queries
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# 데이터 세트와 테이블 및 스키마 비교

Adobe Experience Platform UI에서 사용할 수 [있는](https://platform.adobe.com/datasets)데이터 집합 목록을 검토하여 데이터 집합 이름을 확인합니다.
>[!NOTE] 일부 데이터 집합 이름에는 공백이 있으며 SQL 안전하지 않을 수 있습니다.

![](../images/queries/datasets-and-tables/dataset-names.png)


데이터 집합 테이블의 스키마 이름을 클릭하여 UI에서 데이터 집합 스키마의 계층 구조를 검토합니다.

![](../images/queries/datasets-and-tables/schema-information.png)

PSQL 명령줄을 열고 다음에서 연결 세부 정보를 사용합니다.https://platform.adobe.com/query/configuration [](https://platform.adobe.com/query/configuration).

![](../images/clients/psql/connect-bi.png)

SQL이 있는 플랫폼에서 사용 가능한 테이블을 보려면 `\d` 또는 를 사용할 수 `SHOW TABLES;`있습니다.


`\d` 표준 PostgreSQL 보기를 표시합니다.

```
             List of relations
 Schema |       Name      | Type  |  Owner   
--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

`SHOW TABLES;` 는 보다 자세한 보기를 제공하고 표를 표시하는 사용자 지정 명령이며 플랫폼 UI에 있는 데이터 세트 이름을 나타냅니다.

```
       name      |        dataSetId         |     dataSet    | description | resolved 
-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

테이블의 루트 스키마를 보려면 `\d table_name` 명령을 사용합니다.

>[!NOTE] 표시된 스키마는 대부분 복잡한 루트 필드를 데이터 집합 스키마 UI에서 개체 유형이라고 합니다.

`\d luma_midvalues`

```
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

스키마로 더 자세히 이동하려면 밑줄(`_`)을 사용하여 설명하려는 테이블의 열을 선언합니다. 예, `\d table_name_column`

`\d luma_midvalues_web`

```
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```
