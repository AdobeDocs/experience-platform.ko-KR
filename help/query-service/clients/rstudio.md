---
keywords: Experience Platform;home;popular topics;Query service;query service;RStudio;rstudio;connect to query service;
solution: Experience Platform
title: RStudio와 연결
topic: connect
description: 이 문서에서는 R Studio와 Adobe Experience Platform 쿼리 서비스를 연결하는 단계를 안내합니다.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 2%

---


# 연결 대상 [!DNL RStudio]

이 문서는 R Studio와 Adobe Experience Platform을 연결하는 단계를 안내합니다 [!DNL Query Service].

설치 후 [!DNL RStudio]나타나는 *콘솔* 화면에서 사용할 R 스크립트를 먼저 준비해야 [!DNL PostgreSQL]합니다.

```r
install.packages("RPostgreSQL")
install.packages("rstudioapi")
require("RPostgreSQL")
require("rstudioapi")
```

사용할 R 스크립트를 준비하면 [!DNL PostgreSQL]이제 [!DNL RStudio] 드라이버를 로드하여 [!DNL Query Service] [!DNL PostgreSQL] 연결할 수 있습니다.

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
| `{HOST_NUMBER` 및 `{PORT_NUMBER}` | 쿼리 서비스에 대한 호스트 끝점 및 포트입니다. |
| `{USERNAME}` 및 `{PASSWORD}` | 사용할 로그인 자격 증명입니다. 사용자 이름은 형식을 사용합니다 `ORG_ID@AdobeOrg`. |

>[!NOTE]
>
>데이터베이스 이름, 호스트, 포트 및 로그인 자격 증명을 찾는 방법에 대한 자세한 내용은 플랫폼의 [자격 증명 페이지를 참조하십시오](https://platform.adobe.com/query/configuration). 자격 증명을 찾으려면 로그인하고 쿼리 [!DNL Platform]를 **[!UICONTROL 클릭한 다음 자격 증명]**&#x200B;을 **[!UICONTROL 클릭합니다]**.

## 다음 단계

이제 연결되어 있으므로 쿼리를 작성하여 SQL 문 [!DNL Query Service]을 실행하고 편집할 수 있습니다. 예를 들어 쿼리 `dbGetQuery(con, sql)` 를 실행하는 데 사용할 수 있습니다. 여기서 `sql` 는 실행할 SQL 쿼리입니다.

다음 쿼리는 ExperienceEvents가 [포함된](../creating-queries/experience-event-queries.md) 데이터 세트를 사용하고 장치의 화면 높이로 인해 웹 사이트의 페이지 보기 막대 그래프를 만듭니다.

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

쿼리를 작성하고 실행하는 방법에 대한 자세한 내용은 [실행 쿼리 안내서를 참조하십시오](../creating-queries/creating-queries.md).