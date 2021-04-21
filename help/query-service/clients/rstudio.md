---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;RStudio;rstudio;쿼리 서비스에 연결
solution: Experience Platform
title: 오디오를 쿼리 서비스에 연결
topic-legacy: connect
description: 이 문서에서는 Adobe Experience Platform 쿼리 서비스와 R Studio를 연결하는 단계를 안내합니다.
exl-id: 8dd82bad-6ffb-4536-9c27-223f471a49c6
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 0%

---

# 쿼리 서비스에 [!DNL RStudio] 연결

이 문서에서는 [!DNL RStudio]과(와) Adobe Experience Platform [!DNL Query Service]을(를) 연결하는 단계를 안내합니다.

>[!NOTE]
>
> 이 안내서에서는 사용자가 이미 [!DNL RStudio]에 액세스할 수 있으며 이 기능을 사용하는 방법에 익숙하다고 가정합니다. [!DNL RStudio]에 대한 자세한 내용은 [공식 [!DNL RStudio] 설명서](https://rstudio.com/products/rstudio/)에서 확인할 수 있습니다.
> 
> 또한 쿼리 서비스에서 RStudio를 사용하려면 PostgreSQL JDBC 4.2 드라이버를 설치해야 합니다. [PostgreSQL 공식 사이트](https://jdbc.postgresql.org/download.html)에서 JDBC 드라이버를 다운로드할 수 있습니다.

## [!DNL RStudio] 인터페이스에서 [!DNL Query Service] 연결 만들기

[!DNL RStudio]을(를) 설치한 후 RJDBC 패키지를 설치해야 합니다. **[!DNL Packages]** 창으로 이동하여 **[!DNL Install]**&#x200B;을 선택합니다.

![](../images/clients/rstudio/install-package.png)

**[!DNL Install Packages]** 화면이 표시된 팝업이 나타납니다. **[!DNL Install from]** 섹션에 대해 **[!DNL Repository (CRAN)]**&#x200B;이(가) 선택되어 있는지 확인합니다. **[!DNL Packages]**&#x200B;의 값은 `RJDBC`이어야 합니다. **[!DNL Install dependencies]**&#x200B;이(가) 선택되었는지 확인합니다. 모든 값이 올바른지 확인한 후 **[!DNL Install]**&#x200B;을 선택하여 패키지를 설치합니다.

![](../images/clients/rstudio/install-jrdbc.png)

이제 RJDBC 패키지가 설치되었으므로 RStuto를 다시 시작하여 설치 프로세스를 완료합니다.

이제 RStudio를 다시 시작한 후 쿼리 서비스에 연결할 수 있습니다. **[!DNL Packages]** 창에서 **[!DNL RJDBC]** 패키지를 선택하고 콘솔에 다음 명령을 입력합니다.

```console
pgsql <- JDBC("org.postgresql.Driver", "{PATH TO THE POSTGRESQL JDBC JAR}", "`")
```

여기서 {PATH TO THE POSTGRESQL JDBC JAR}은 컴퓨터에 설치된 PostgreSQL JDBC JAR의 경로를 나타냅니다.

이제 콘솔에서 다음 명령을 입력하여 쿼리 서비스에 대한 연결을 만들 수 있습니다.

```console
qsconnection <- dbConnect(pgsql, "jdbc:postgresql://{HOSTNAME}:{PORT}/{DATABASE_NAME}?user={USERNAME}&password={PASSWORD}&sslmode=require")
```

>[!NOTE]
>
>데이터베이스 이름, 호스트, 포트 및 로그인 자격 증명을 찾는 방법에 대한 자세한 내용은 플랫폼](https://platform.adobe.com/query/configuration)의 [자격 증명 페이지를 참조하십시오. 자격 증명을 찾으려면 [!DNL Platform]에 로그인한 다음 **[!UICONTROL Queries]** 뒤에 **[!UICONTROL Credentials]**&#x200B;를 선택합니다.

![](../images/clients/rstudio/connection-rjdbc.png)

## 쿼리 쓰기

이제 [!DNL Query Service]에 연결되었으므로 쿼리를 작성하여 SQL 문을 실행하고 편집할 수 있습니다. 예를 들어 `dbGetQuery(con, sql)`을 사용하여 쿼리를 실행할 수 있습니다. 여기서 `sql`은 실행하려는 SQL 쿼리입니다.

다음 쿼리는 [경험 이벤트](../best-practices/experience-event-queries.md)를 포함하는 데이터 세트를 사용하고 장치의 화면 높이에 따라 웹 사이트의 페이지 보기 막대 그래프를 만듭니다.

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

## 다음 단계

쿼리를 작성하고 실행하는 방법에 대한 자세한 내용은 [쿼리 실행](../best-practices/writing-queries.md)에 대한 안내서를 참조하십시오.
