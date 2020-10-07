---
keywords: Experience Platform;home;popular topics;query service;Query service;Power BI;power bi;connect to query service;
solution: Experience Platform
title: Power BI과 연결
topic: connect
description: 이 문서에서는 Adobe Experience Platform 쿼리 서비스와 Power BI을 연결하는 단계를 안내합니다.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---


# 연결 [!DNL Power BI] (PC)

PC 사용자는 https://powerbi.microsoft.com/en-us/desktop/ [!DNL Power BI] 에서 설치할 수 [있습니다](https://powerbi.microsoft.com/en-us/desktop/).

## 설정 [!DNL Power BI]

설치한 후 PostgreSQL 커넥터를 지원하기 위해 필요한 구성 요소를 설정해야 [!DNL Power BI] 합니다. 다음 단계를 따르십시오.

- PowerBI에 연결하는 공식 방법인 PostgreSQL용 .NET 드라이버 패키지를 찾아 설치합니다. `npgsql`

- v4.0.10을 선택합니다(최신 버전이 있으면 오류가 발생함).

- 사용자 정의 설치 화면의 &quot;Npgsql GAC 설치&quot;에서 로컬 하드 드라이브에 설치됨 **[!UICONTROL 을 선택합니다]**. GAC를 설치하지 않으면 나중에 Power BI이 실패합니다.

- Windows를 다시 시작합니다.

- 데스크탑 [!DNL PowerBI] 평가 버전을 찾습니다.

## 연결 [!DNL Power BI] 을 [!DNL Query Service]

이러한 준비 단계를 수행한 후 다음 [!DNL Power BI] 에 연결할 수 있습니다 [!DNL Query Service].

- 열기 [!DNL Power BI].

- 상단 메뉴 **[!UICONTROL 리본에서 데이터]** 가져오기를 클릭합니다.

- [ **[!UICONTROL PostgreSQL 데이터베이스]**]를 선택한 다음 **[!UICONTROL Connect를 클릭합니다]**.

- 서버 및 데이터베이스 값을 입력합니다. **[!UICONTROL 서버가]** 연결 세부 정보 아래에 있는 호스트입니다. 프로덕션의 경우 호스트 문자열 끝 `:80` 에 포트를 추가합니다. **[!UICONTROL 데이터베이스는]** &quot;모두&quot; 또는 데이터 집합 테이블 이름일 수 있습니다. (CTAS에서 파생된 데이터 집합 중 하나를 사용해 보십시오.)

- 고급 옵션 **[!UICONTROL 을]**&#x200B;클릭한 다음 관계 열 **[!UICONTROL 포함의 선택을 취소합니다]**. 전체 계층 **[!UICONTROL 을 사용하여 탐색하기를 선택하지 마십시오]**.

- *(선택 사항이지만 데이터베이스에 대해 &quot;모두&quot;가 선언될 때 권장)* SQL 문을 입력하십시오.

>[!NOTE]
>
>SQL 문이 제공되지 않으면 데이터베이스의 모든 테이블을 미리 [!DNL Power BI] 봅니다. 계층 데이터의 경우 사용자 지정 SQL 문을 사용해야 합니다. 테이블 스키마가 평평하면 사용자 지정 SQL 문이 있거나 없는 상태로 작동합니다. 컴파운드 유형은 아직 지원되지 않습니다. 컴파운드 [!DNL Power BI] 유형에서 원시 유형을 가져오려면 SQL 문을 작성하여 파생해야 합니다.

```sql
SELECT web.webPageDetails.name AS Page_Name, 
SUM(web.webPageDetails.pageviews.value) AS Page_Views 
FROM _TABLE_ 
WHERE TIMESTAMP >= to_timestamp('2018-11-20')
GROUP BY web.webPageDetails.name 
ORDER BY SUM(web.webPageDetails.pageviews.value) DESC 
LIMIT 10
```

- &quot;[!UICONTROL DirectQuery]&quot; 또는 &quot;[!UICONTROL 가져오기]&quot; 모드를 선택합니다. DirectQuery  모드에서는 모든 쿼리가 실행되도록 [!DNL Query Service] 전송됩니다. 가져오기  모드에서 데이터를 가져옵니다 [!DNL Power BI].

- **[!UICONTROL 확인]**&#x200B;을 클릭합니다. 이제 [!DNL Power BI] 에 연결하여 오류가 [!DNL Query Service] 없는 경우 미리 보기를 생성합니다. 미리 보기 렌더링 숫자 열에 알려진 문제가 있습니다. 다음 단계로 진행합니다.

- 데이터 **[!UICONTROL 세트를]** 가져오려면 로드를 클릭합니다 [!DNL Power BI].
