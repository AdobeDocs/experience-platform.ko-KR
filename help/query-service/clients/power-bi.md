---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;Power BI;power bi;쿼리 서비스에 연결;;home;popular topics service;query service;;power bi;connect to query service;
solution: Experience Platform
title: 쿼리 서비스에 Power BI 연결
topic-legacy: connect
description: 이 문서에서는 Adobe Experience Platform 쿼리 서비스에 Power BI을 연결하는 단계를 안내합니다.
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 0%

---

# 쿼리 서비스에 [!DNL Power BI] 연결(PC)

이 문서에서는 Adobe Experience Platform 쿼리 서비스에 Power BI을 연결하는 단계를 다룹니다.

>[!NOTE]
>
> 이 안내서에서는 사용자가 이미 [!DNL Power BI]에 액세스할 수 있으며 인터페이스를 탐색하는 방법에 익숙하다고 가정합니다. [!DNL Power BI]에 대한 자세한 내용은 [공식 [!DNL Power BI] 설명서](https://docs.looker.com/)에서 확인할 수 있습니다.
>
> 또한 Power BI은 **Windows 장치에서**&#x200B;만 사용할 수 있습니다.

Power BI을 설치한 후 PostgreSQL용 .NET 드라이버 패키지인 `Npgsql`을(를) 설치해야 합니다. Npgsql에 대한 자세한 내용은 [Npgsql 설명서](https://www.npgsql.org/doc/index.html)에서 확인할 수 있습니다.

>[!IMPORTANT]
>
>최신 버전이 오류를 일으키므로 v4.0.10 이상을 다운로드해야 합니다.

사용자 정의 설정 화면의 &quot;[!DNL Npgsql GAC Installation]&quot;에서 **[!DNL Will be installed on local hard drive]**&#x200B;을 선택합니다.

npgsql이 제대로 설치되었는지 확인하려면 다음 단계로 진행하기 전에 컴퓨터를 다시 시작하십시오.

## [!DNL Power BI]을(를) [!DNL Query Service]에 연결

[!DNL Power BI]을 [!DNL Query Service]에 연결하려면 [!DNL Power BI]를 열고 위쪽 메뉴 리본에서 **[!DNL Get Data]**&#x200B;을 선택합니다.

![](../images/clients/power-bi/open-power-bi.png)

**[!DNL PostgreSQL database]** 뒤에 **[!DNL Connect]**&#x200B;를 선택합니다.

![](../images/clients/power-bi/get-data.png)

이제 서버 및 데이터베이스의 값을 입력할 수 있습니다. 데이터베이스 이름, 호스트, 포트 및 로그인 자격 증명을 찾는 방법에 대한 자세한 내용은 플랫폼](https://platform.adobe.com/query/configuration)의 [자격 증명 페이지를 참조하십시오. 자격 증명을 찾으려면 [!DNL Platform]에 로그인한 다음 **[!UICONTROL Queries]** 뒤에 **[!UICONTROL Credentials]**&#x200B;를 선택합니다.

**[!DNL Server]** 은 연결 세부 사항 아래에 있는 호스트입니다. 프로덕션의 경우 호스트 문자열 끝에 `:80` 포트를 추가합니다. **[!DNL Database]** &quot;all&quot; 또는 데이터 집합 테이블 이름을 사용할 수 있습니다.

또한 **[!DNL Data Connectivity mode]**&#x200B;을 선택할 수도 있습니다. 사용 가능한 모든 테이블 목록을 표시하려면 **[!DNL Import]**&#x200B;을 선택하고 쿼리를 직접 만들려면 **[!DNL DirectQuery]**&#x200B;을 선택합니다.

**[!DNL Import]** 모드에 대한 자세한 내용을 보려면 [표 미리 보기 및 가져오기](#preview)의 섹션을 참조하십시오. **[!DNL DirectQuery]** 모드에 대한 자세한 내용은 [SQL 문 만들기](#create)의 섹션을 참조하십시오. 데이터베이스 세부 사항을 확인한 후 **[!DNL OK]**&#x200B;을 선택합니다.

![](../images/clients/power-bi/connectivity-mode.png)

사용자 이름, 암호 및 애플리케이션 설정을 묻는 메시지가 나타납니다. 이러한 세부 사항을 입력한 다음 **[!DNL Connect]**&#x200B;을 선택하여 다음 단계로 계속 진행합니다.

![](../images/clients/power-bi/import-mode.png)

## {#preview} 표 미리 보기 및 가져오기

**[!DNL Import]** 모드를 선택하면 사용 가능한 모든 테이블 목록이 표시된 대화 상자가 나타납니다. 미리 보려는 테이블을 선택하고 **[!DNL Load]**&#x200B;을 클릭하여 데이터 세트를 [!DNL Power BI]로 가져옵니다.

![](../images/clients/power-bi/preview-table.png)

이제 표를 Power BI으로 가져옵니다.

![](../images/clients/power-bi/import-table.png)

## SQL 문 만들기 {#create}

**[!DNL DirectQuery]** 모드를 선택한 경우 만들려는 SQL 쿼리를 사용하여 고급 옵션 섹션을 작성해야 합니다.

**[!DNL SQL statement]** 아래에서 만들려는 SQL 쿼리를 삽입합니다. **[!DNL Include relationship columns]** 확인란이 선택되어 있는지 확인합니다. 쿼리를 작성했으면 **[!DNL OK]**&#x200B;을 선택하여 계속 진행합니다.

![](../images/clients/power-bi/direct-query-mode.png)

쿼리의 미리 보기가 나타납니다. 쿼리 결과를 보려면 **[!DNL Load]**&#x200B;을 선택합니다.

![](../images/clients/power-bi/preview-direct-query.png)

## 다음 단계

이제 [!DNL Query Service]에 연결되었으므로 [!DNL Power BI]를 사용하여 쿼리를 작성할 수 있습니다. 쿼리를 작성하고 실행하는 방법에 대한 자세한 내용은 [쿼리 실행](../best-practices/writing-queries.md)에 대한 안내서를 참조하십시오.
