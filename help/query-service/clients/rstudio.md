---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;RStudio;rstudio;쿼리 서비스에 연결;
solution: Experience Platform
title: RStudio를 쿼리 서비스에 연결
description: 이 문서에서는 R Studio를 Adobe Experience Platform 쿼리 서비스와 연결하는 단계를 안내합니다.
exl-id: 8dd82bad-6ffb-4536-9c27-223f471a49c6
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# 쿼리 서비스에 [!DNL RStudio] 연결

이 문서는 [!DNL RStudio]을(를) Adobe Experience Platform [!DNL Query Service]과(와) 연결하는 단계를 안내합니다.

>[!NOTE]
>
> [!DNL RStudio]이(가) 이제 [!DNL Posit]&#x200B;(으)로 다시 브랜딩되었습니다. [!DNL RStudio] 제품의 이름이 [!DNL Posit Connect], [!DNL Posit Workbench], [!DNL Posit Package] 관리자, [!DNL Posit Cloud] 및 [!DNL Posit Academy]&#x200B;(으)로 바뀌었습니다.
>
> 이 안내서에서는 사용자가 이미 [!DNL RStudio]에 액세스할 수 있고 사용 방법을 잘 알고 있다고 가정합니다. [!DNL RStudio]에 대한 자세한 내용은 [공식 [!DNL RStudio] 설명서](https://rstudio.com/products/rstudio/)에서 확인할 수 있습니다.
> 
> 또한 쿼리 서비스에 [!DNL RStudio]을(를) 사용하려면 [!DNL PostgreSQL] JDBC 4.2 드라이버를 설치해야 합니다. [[!DNL PostgreSQL] 공식 사이트](https://jdbc.postgresql.org/download/)에서 JDBC 드라이버를 다운로드할 수 있습니다.

## [!DNL RStudio] 인터페이스에서 [!DNL Query Service] 연결 만들기

[!DNL RStudio]을(를) 설치한 후 RJDBC 패키지를 설치해야 합니다. [명령줄을 통해 데이터베이스를 연결](https://solutions.posit.co/connections/db/best-practices/drivers/#connecting-to-a-database-in-r)하는 방법에 대한 지침은 공식 Position 문서에서 확인할 수 있습니다.

Mac OS를 사용하는 경우 메뉴 표시줄에서 **[!UICONTROL 도구]**&#x200B;를 선택한 다음 드롭다운 메뉴에서 **[!UICONTROL 패키지 설치]**&#x200B;를 선택할 수 있습니다. 또는 RStudio UI에서 **[!DNL Packages]** 탭을 선택하고 **[!DNL Install]**&#x200B;을(를) 선택합니다.

팝업이 표시되어 **[!DNL Install Packages]** 화면이 표시됩니다. **[!DNL Install from]** 섹션에 대해 **[!DNL Repository (CRAN)]**&#x200B;을(를) 선택했는지 확인하십시오. **[!DNL Packages]**&#x200B;의 값은 `RJDBC`이어야 합니다. **[!DNL Install dependencies]**&#x200B;을(를) 선택했는지 확인하십시오. 모든 값이 올바른지 확인한 후 **[!DNL Install]**&#x200B;을(를) 선택하여 패키지를 설치하십시오. RJDBC 패키지가 설치되었으므로 [!DNL RStudio]을(를) 다시 시작하여 설치 프로세스를 완료합니다.

[!DNL RStudio]을(를) 다시 시작하면 이제 쿼리 서비스에 연결할 수 있습니다. **[!DNL Packages]** 창에서 **[!DNL RJDBC]** 패키지를 선택하고 콘솔에 다음 명령을 입력합니다.

```console
pgsql <- JDBC("org.postgresql.Driver", "{PATH TO THE POSTGRESQL JDBC JAR}", "`")
```

여기서 `{PATH TO THE POSTGRESQL JDBC JAR}`은(는) 컴퓨터에 설치된 [!DNL PostgreSQL] JDBC JAR에 대한 경로를 나타냅니다.

이제 쿼리 서비스에 대한 연결을 만들 수 있습니다. 콘솔에 다음 명령을 입력합니다.

```console
qsconnection <- dbConnect(pgsql, "jdbc:postgresql://{HOSTNAME}:{PORT}/{DATABASE_NAME}?user={USERNAME}&password={PASSWORD}&sslmode=require")
```

>[!IMPORTANT]
>
>Adobe Experience Platform 쿼리 서비스에 대한 서드파티 연결에 대한 SSL 지원 및 `verify-full` SSL 모드를 사용하여 연결하는 방법에 대한 자세한 내용은 [[!DNL Query Service] SSL 설명서](./ssl-modes.md)를 참조하세요.

데이터베이스 이름, 호스트, 포트 및 로그인 자격 증명을 찾는 방법에 대한 자세한 내용은 [자격 증명 안내서](../ui/credentials.md)를 참조하십시오. 자격 증명을 찾으려면 [!DNL Experience Platform]에 로그인한 다음 **[!UICONTROL 쿼리]**, **[!UICONTROL 자격 증명]**&#x200B;을 선택하십시오.

콘솔 출력의 메시지가 쿼리 서비스에 대한 연결을 확인합니다.

## 쿼리 작성

[!DNL Query Service]에 연결했으므로 쿼리를 작성하여 SQL 문을 실행하고 편집할 수 있습니다. 예를 들어 `dbGetQuery(con, sql)`을(를) 사용하여 쿼리를 실행할 수 있습니다. 여기서 `sql`은(는) 실행하려는 SQL 쿼리입니다.

다음 쿼리는 [경험 이벤트](../../xdm/classes/experienceevent.md)가 포함된 데이터 세트를 사용하며, 장치의 화면 높이에 따라 웹 사이트의 페이지 보기 수에 대한 히스토그램을 만듭니다.

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
