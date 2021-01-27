---
keywords: Experience Platform;home;popular topics;Query service;query service;RStudio;rstudio;connect to query service;
solution: Experience Platform
title: 오디오 연결
topic: connect
description: 이 문서에서는 Adobe Experience Platform 쿼리 서비스와 R Studio를 연결하는 단계를 안내합니다.
translation-type: tm+mt
source-git-commit: 9fbb6b829cd9ddec30f22b0de66874be7710e465
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 2%

---


# [!DNL RStudio]에 연결

이 문서에서는 Adobe Experience Platform [!DNL Query Service]에 R Studio를 연결하는 단계를 안내합니다.

[!DNL RStudio]을(를) 설치한 후 나타나는 *콘솔* 화면에서 먼저 [!DNL PostgreSQL]을(를) 사용할 R 스크립트를 준비해야 합니다.

```r
install.packages("RPostgreSQL")
install.packages("rstudioapi")
require("RPostgreSQL")
require("rstudioapi")
```

[!DNL PostgreSQL]을 사용하도록 R 스크립트를 준비했으면 [!DNL PostgreSQL] 드라이버를 로드하여 [!DNL RStudio]을 [!DNL Query Service]에 연결할 수 있습니다.

```r
drv <- dbDriver("PostgreSQL")
con <- dbConnect(drv, 
 dbname = "{DATABASE_NAME}",
 host="{HOST_NUMBER}",
 port={PORT_NUMBER},
 user="{USERNAME}",
 password="{PASSWORD}")
```

| 속성 | 설명 |
| -------- | ----------- |
| `{DATABASE_NAME}` | 사용할 데이터베이스의 이름입니다. |
| `{HOST_NUMBER` 및 `{PORT_NUMBER}` | 쿼리 서비스에 대한 호스트 끝점과 포트입니다. |
| `{USERNAME}` 및 `{PASSWORD}` | 사용할 로그인 자격 증명입니다. 사용자 이름은 `ORG_ID@AdobeOrg` 형식을 사용합니다. |

>[!NOTE]
>
>데이터베이스 이름, 호스트, 포트 및 로그인 자격 증명을 찾는 방법에 대한 자세한 내용은 플랫폼](https://platform.adobe.com/query/configuration)의 [자격 증명 페이지를 참조하십시오. 자격 증명을 찾으려면 [!DNL Platform]에 로그인하고 **[!UICONTROL 쿼리]**&#x200B;를 클릭한 다음 **[!UICONTROL 자격 증명]**&#x200B;을 클릭합니다.

## 다음 단계

이제 [!DNL Query Service]에 연결되었으므로 쿼리를 작성하여 SQL 문을 실행하고 편집할 수 있습니다. 예를 들어 `dbGetQuery(con, sql)`을 사용하여 쿼리를 실행할 수 있습니다. 여기서 `sql`은 실행하려는 SQL 쿼리입니다.

다음 쿼리는 [ExperienceEvents](../best-practices/experience-event-queries.md)를 포함하는 데이터 세트를 사용하고 장치의 화면 높이에 따라 웹 사이트의 페이지 보기 막대 그래프를 만듭니다.

```sql
df_pageviews <- dbGetQuery(con,
"SELECT t.range AS buckets, 
 Count(*) AS pageviews 
FROM (SELECT CASE 
 WHEN device.screenheight BETWEEN 0 AND 99 THEN '0 - 99' 
 WHEN device.screenheight BETWEEN 100 AND 199 THEN '100-199' 
 WHEN device.screenheight BETWEEN 200 AND 299 THEN '200-299' 
 WHEN device.screenheight BETWEEN 300 AND 399 THEN '300-399' 
 WHEN device.screenheight BETWEEN 400 AND 499 THEN '400-499' 
 WHEN device.screenheight BETWEEN 500 AND 599 THEN '500-599' 
 ELSE '600-699' 
 end AS range 
 FROM aa_post_vals_3) t 
GROUP BY t.range 
ORDER BY buckets 
LIMIT 1000000")
```

성공적인 응답은 쿼리 결과를 반환합니다.

```r
df_pageviews
 buckets pageviews
1 0 - 99 198985
2 500-599 67138
3 300-399 2147
4 200-299 354
5 400-499 6947
6 100-199 4415
7 600-699 3097040
```

쿼리를 작성하고 실행하는 방법에 대한 자세한 내용은 [쿼리 실행 안내서](../best-practices/writing-queries.md)를 참조하십시오.