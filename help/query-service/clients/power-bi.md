---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;Power BI;power bi;쿼리 서비스에 연결
solution: Experience Platform
title: 쿼리 서비스에 Power BI 연결
topic-legacy: connect
description: 이 문서에서는 Adobe Experience Platform Query Service와 Power BI을 연결하는 단계를 안내합니다.
exl-id: 8fcd3056-aac7-4226-a354-ed7fb8fe9ad7
source-git-commit: 2109abd02b9c6c321c21a8fe3826509d22b1c2e2
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 1%

---

# [!DNL Power BI]을 쿼리 서비스(PC)에 연결

이 문서에서는 Adobe Experience Platform 쿼리 서비스와 Power BI을 연결하는 단계를 설명합니다.

>[!NOTE]
>
> 이 안내서에서는 이미 [!DNL Power BI]에 액세스할 수 있고 인터페이스를 탐색하는 방법을 잘 알고 있다고 가정합니다. [!DNL Power BI]에 대한 자세한 내용은 [공식 [!DNL Power BI] 설명서](https://docs.microsoft.com/ko-ko/power-bi/)에서 확인할 수 있습니다.
>
> 또한 Power BI은 **Windows 장치에서 사용할 수 있는**&#x200B;뿐입니다.

Power BI을 설치한 후에는 PostgreSQL용 .NET 드라이버 패키지인 `Npgsql`을 설치해야 합니다. Npgsql에 대한 자세한 내용은 [Npgsql 설명서](https://www.npgsql.org/doc/index.html)에서 확인할 수 있습니다.

>[!IMPORTANT]
>
>최신 버전에서 오류가 발생하므로 v4.0.10 이하를 다운로드해야 합니다.

사용자 지정 설정 화면의 &quot;[!DNL Npgsql GAC Installation]&quot;에서 **[!DNL Will be installed on local hard drive]**&#x200B;을 선택합니다.

npgsql이 제대로 설치되어 있는지 확인하려면 다음 단계로 진행하기 전에 컴퓨터를 다시 시작하십시오.

## [!DNL Power BI]을 [!DNL Query Service]에 연결

[!DNL Power BI]을 [!DNL Query Service]에 연결하려면 [!DNL Power BI]를 열고 위쪽 메뉴 리본에서 **[!DNL Get Data]**&#x200B;을 선택합니다.

![](../images/clients/power-bi/open-power-bi.png)

**[!DNL PostgreSQL database]** 을 선택하고 **[!DNL Connect]** 을 선택합니다.

![](../images/clients/power-bi/get-data.png)

이제 서버와 데이터베이스의 값을 입력할 수 있습니다. 데이터베이스 이름, 호스트, 포트 및 로그인 자격 증명을 찾는 방법에 대한 자세한 내용은 Platform](https://platform.adobe.com/query/configuration)의 [자격 증명 페이지를 참조하십시오. 자격 증명을 찾으려면 [!DNL Platform]에 로그인한 다음 **[!UICONTROL 쿼리]**, 자격 증명&#x200B;]**을 차례로 선택하십시오.**[!UICONTROL 

**[!DNL Server]** 은 연결 세부 정보에서 찾은 호스트입니다. 프로덕션의 경우 호스트 문자열 끝에 포트 `:80`을 추가합니다. **[!DNL Database]** &quot;모두&quot; 또는 데이터 집합 테이블 이름일 수 있습니다.

또한 **[!DNL Data Connectivity mode]**&#x200B;을 선택할 수 있습니다. **[!DNL Import]** 을 선택하여 사용 가능한 모든 테이블 목록을 표시하거나 **[!DNL DirectQuery]** 을 선택하여 쿼리를 직접 만듭니다.

**[!DNL Import]** 모드에 대한 자세한 내용은 [표 미리 보기 및 가져오기](#preview)의 섹션을 참조하십시오. **[!DNL DirectQuery]** 모드에 대한 자세한 내용은 [SQL 문 만들기](#create)의 섹션을 참조하십시오. 데이터베이스 세부 정보를 확인한 후 **[!DNL OK]**&#x200B;을 선택합니다.

![](../images/clients/power-bi/connectivity-mode.png)

사용자 이름, 암호 및 애플리케이션 설정을 묻는 메시지가 나타납니다. 이러한 세부 사항을 입력한 다음 **[!DNL Connect]** 을 선택하여 다음 단계로 진행합니다.

![](../images/clients/power-bi/import-mode.png)

## 표 미리 보기 및 가져오기 {#preview}

**[!DNL Import]** 모드를 선택하면 사용 가능한 모든 테이블의 목록이 표시되는 대화 상자가 나타납니다. 미리 보려는 테이블을 선택하고 **[!DNL Load]** 을 선택하여 데이터 세트를 [!DNL Power BI]로 가져옵니다.

![](../images/clients/power-bi/preview-table.png)

이제 표를 Power BI으로 가져옵니다.

![](../images/clients/power-bi/import-table.png)

## SQL 문 만들기 {#create}

**[!DNL DirectQuery]** 모드를 선택한 경우 만들려는 SQL 쿼리로 고급 옵션 섹션을 입력해야 합니다.

**[!DNL SQL statement]** 아래에 만들 SQL 쿼리를 삽입합니다. **[!DNL Include relationship columns]** 확인란을 선택해야 합니다. 쿼리를 작성했으면 **[!DNL OK]**&#x200B;을 선택하여 계속하십시오.

![](../images/clients/power-bi/direct-query-mode.png)

쿼리의 미리 보기가 나타납니다. **[!DNL Load]** 을 선택하여 쿼리 결과를 확인합니다.

![](../images/clients/power-bi/preview-direct-query.png)

## 다음 단계

이제 [!DNL Query Service]과 연결되었으므로 [!DNL Power BI]을 사용하여 쿼리를 작성할 수 있습니다. 쿼리를 작성하고 실행하는 방법에 대한 자세한 내용은 [쿼리 실행](../best-practices/writing-queries.md)에 대한 안내서를 참조하십시오.
