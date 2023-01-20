---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;RStudio;rstudio;쿼리 서비스에 연결
solution: Experience Platform
title: RStudio를 쿼리 서비스에 연결
description: 이 문서에서는 R Studio와 Adobe Experience Platform 쿼리 서비스를 연결하는 단계를 안내합니다.
exl-id: 8dd82bad-6ffb-4536-9c27-223f471a49c6
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# Connect [!DNL RStudio] 쿼리 서비스

이 문서는 연결 단계를 안내합니다 [!DNL RStudio] Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> [!DNL RStudio] 이제 은(는) [!DNL Posit]. [!DNL RStudio] products가 [!DNL Posit Connect], [!DNL Posit Workbench], [!DNL Posit Package] 관리자, [!DNL Posit Cloud], 및 [!DNL Posit Academy].
>
> 이 안내서에서는 사용자가 이미 [!DNL RStudio] 사용 방법도 잘 알고 있습니다. 에 대한 추가 정보 [!DNL RStudio] 은 [공식 [!DNL RStudio] 설명서](https://rstudio.com/products/rstudio/).
> 
> 또한 [!DNL RStudio] 쿼리 서비스를 사용하는 경우 [!DNL PostgreSQL] JDBC 4.2 드라이버. JDBC 드라이버를 [[!DNL PostgreSQL] 공식 현장](https://jdbc.postgresql.org/download/).

## 만들기 [!DNL Query Service] 연결 위치 [!DNL RStudio] 인터페이스

설치 후 [!DNL RStudio]를 눌러 RJDBC 패키지를 설치해야 합니다. 방법에 대한 지침 [명령줄을 통해 데이터베이스 연결](https://solutions.posit.co/connections/db/best-practices/drivers/#connecting-to-a-database-in-r) 공식 예금 설명서에서 찾을 수 있습니다.

Mac OS를 사용하는 경우 **[!UICONTROL 도구]** 메뉴 모음에서 **[!UICONTROL 패키지 설치]** 드롭다운 메뉴에서 을 클릭합니다. 또는 을(를) 선택합니다 **[!DNL Packages]** Studio UI에서 탭을 선택하고 **[!DNL Install]**.

팝업이 나타나고 **[!DNL Install Packages]** 화면. 확인 **[!DNL Repository (CRAN)]** 에 대해 이(가) 선택되어 있습니다 **[!DNL Install from]** 섹션을 참조하십시오. 에 대한 값 **[!DNL Packages]** 다음과 같습니다. `RJDBC`. 확인 **[!DNL Install dependencies]** 이 선택되어 있습니다. 모든 값이 올바른지 확인한 후 을(를) 선택합니다 **[!DNL Install]** 패키지를 설치하려면 다음을 수행하십시오. 이제 RJDBC 패키지가 설치되었으므로 다시 시작합니다 [!DNL RStudio] 를 클릭하여 설치 프로세스를 완료합니다.

후 [!DNL RStudio] 다시 시작되었으므로 이제 Query Service에 연결할 수 있습니다. 을(를) 선택합니다 **[!DNL RJDBC]** 패키지 **[!DNL Packages]** 창을 열고 콘솔에 다음 명령을 입력합니다.

```console
pgsql <- JDBC("org.postgresql.Driver", "{PATH TO THE POSTGRESQL JDBC JAR}", "`")
```

위치 `{PATH TO THE POSTGRESQL JDBC JAR}` 는 [!DNL PostgreSQL] 컴퓨터에 설치된 JDBC JAR입니다.

이제 Query Service에 대한 연결을 만들 수 있습니다. 콘솔에 다음 명령을 입력합니다.

```console
qsconnection <- dbConnect(pgsql, "jdbc:postgresql://{HOSTNAME}:{PORT}/{DATABASE_NAME}?user={USERNAME}&password={PASSWORD}&sslmode=require")
```

>[!IMPORTANT]
>
>자세한 내용은 [[!DNL Query Service] SSL 설명서](./ssl-modes.md) Adobe Experience Platform Query Service에 대한 타사 연결에 대한 SSL 지원 및 `verify-full` SSL 모드.

데이터베이스 이름, 호스트, 포트 및 로그인 자격 증명을 찾는 방법에 대한 자세한 내용은 [자격 증명 안내서](../ui/credentials.md). 자격 증명을 찾으려면 [!DNL Platform]를 선택하고 을 선택합니다. **[!UICONTROL 쿼리]**, 그 다음 **[!UICONTROL 자격 증명]**.

콘솔 출력에 있는 메시지가 Query Service에 대한 연결을 확인합니다.

## 쿼리 쓰기

이제 [!DNL Query Service]를 사용하여 쿼리를 작성하여 SQL 문을 실행하고 편집할 수 있습니다. 예를 들어 `dbGetQuery(con, sql)` 쿼리를 실행하려면 `sql` 실행할 SQL 쿼리입니다.

다음 쿼리는 [경험 이벤트](../../xdm/classes/experienceevent.md) 장치의 화면 높이에 따라 웹 사이트의 페이지 보기 히스토그램을 만듭니다.

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

쿼리를 작성하고 실행하는 방법에 대한 자세한 내용은 [쿼리 실행](../best-practices/writing-queries.md).
