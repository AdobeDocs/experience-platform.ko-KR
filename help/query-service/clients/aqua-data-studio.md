---
keywords: Experience Platform;home;popular topics;query service;Query service;Aqua Data Studio;Aqua data studio;connect to query service;
solution: Experience Platform
title: Aqua Data Studio와 연결
topic: connect
description: 이 문서에서는 Aqua Data Studio와 Adobe Experience Platform 쿼리 서비스를 연결하는 단계를 안내합니다.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---


# 연결 대상 [!DNL Aqua Data Studio]

이 문서는 Adobe Experience Platform [!DNL Aqua Data Studio] 와 연결하는 단계를 안내합니다 [!DNL Query Service].

설치 [!DNL Aqua Data Studio]후 먼저 서버를 등록해야 합니다. 주 메뉴에서 **[!UICONTROL 서버]**&#x200B;를 클릭한 다음 서버 **[!UICONTROL 등록을 클릭합니다]**.

![](../images/clients/aqua-data-studio/register-server.png)

[서버 **[!UICONTROL 등록]** ] 대화 상자가 나타납니다. [ **[!UICONTROL 일반]** ] 탭 **[!UICONTROL 의 왼쪽]** 목록에서 PostgreSQL을 선택합니다. 나타나는 대화 상자에서 서버 설정에 대해 다음과 같은 세부 정보를 제공합니다.

- **[!UICONTROL 이름]**:연결 이름입니다.
- **[!UICONTROL 로그인 이름 및 암호]**:사용할 로그인 자격 증명입니다. 사용자 이름은 형식을 사용합니다 `ORG_ID@AdobeOrg`.
- **[!UICONTROL 호스트 및 포트]**:호스트 끝점 및 해당 포트 [!DNL Query Service]. 에 연결하려면 포트 80을 사용해야 합니다 [!DNL Query Service].
- **[!UICONTROL 데이터베이스]:** 사용할 데이터베이스입니다.

>[!NOTE]
>
>로그인 자격 증명, 호스트, 포트 및 데이터베이스 이름을 찾는 방법에 대한 자세한 내용은 플랫폼의 [자격 증명 페이지를 참조하십시오](https://platform.adobe.com/query/configuration). 자격 증명을 찾으려면 로그인하고 쿼리 [!DNL Platform]를 **[!UICONTROL 클릭한 다음 자격 증명]**&#x200B;을 **[!UICONTROL 클릭합니다]**.

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

Select the **[!UICONTROL Driver]** tab. 매개 **[!UICONTROL 변수에서]**&#x200B;값을 `?sslmode=require`

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

연결 세부 사항을 입력한 후 연결 **[!UICONTROL 테스트를]** 클릭하여 자격 증명이 제대로 작동하는지 확인합니다. 연결이 성공하면 [ **[!UICONTROL 저장]** ]을 클릭하여 서버를 등록합니다. 등록이 완료되면 **대시보드** (dashboard)에 연결이 나타나 서버에 연결하여 스키마 개체를 볼 수 있음을 확인합니다.

## 다음 단계

연결한 다음 [!DNL Query Service]에 **[!UICONTROL 쿼리 분석기를]** 사용하여 SQL 문을 실행하고 편집할 수 있습니다 [!DNL Aqua Data Studio] . 쿼리를 작성하고 실행하는 방법에 대한 자세한 내용은 [실행 쿼리 안내서를 참조하십시오](../creating-queries/creating-queries.md).