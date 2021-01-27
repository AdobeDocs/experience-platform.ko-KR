---
keywords: Experience Platform;home;popular topics;query service;Query service;Aqua Data Studio;Aqua data studio;connect to query service;
solution: Experience Platform
title: Aqua Data Studio와 연결
topic: connect
description: 이 문서에서는 Aqua Data Studio와 Adobe Experience Platform 쿼리 서비스를 연결하는 단계를 안내합니다.
translation-type: tm+mt
source-git-commit: 9fbb6b829cd9ddec30f22b0de66874be7710e465
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---


# [!DNL Aqua Data Studio]에 연결

이 문서에서는 [!DNL Aqua Data Studio]과(와) Adobe Experience Platform [!DNL Query Service]을(를) 연결하는 단계를 안내합니다.

[!DNL Aqua Data Studio]을(를) 설치한 후 먼저 서버를 등록해야 합니다. 주 메뉴에서 **[!UICONTROL 서버]**&#x200B;를 클릭한 다음 **[!UICONTROL 서버 등록]**&#x200B;을 클릭합니다.

![](../images/clients/aqua-data-studio/register-server.png)

**[!UICONTROL 서버 등록]** 대화 상자가 나타납니다. **[!UICONTROL 일반]** 탭의 왼쪽 목록에서 **[!UICONTROL PostgreSQL]**&#x200B;을 선택합니다. 나타나는 대화 상자에서 서버 설정에 대해 다음 세부 정보를 제공합니다.

- **[!UICONTROL 이름]**:연결 이름입니다.
- **[!UICONTROL 로그인 이름 및 암호]**:사용할 로그인 자격 증명입니다. 사용자 이름은 `ORG_ID@AdobeOrg` 형식을 사용합니다.
- **[!UICONTROL 호스트 및 포트]**:호스트 끝점 및 해당 포트 [!DNL Query Service]입니다. [!DNL Query Service]에 연결하려면 포트 80을 사용해야 합니다.
- **[!UICONTROL 데이터베이스]:** 사용할 데이터베이스입니다.

>[!NOTE]
>
>로그인 자격 증명, 호스트, 포트 및 데이터베이스 이름을 찾는 방법에 대한 자세한 내용은 플랫폼](https://platform.adobe.com/query/configuration)의 [자격 증명 페이지를 참조하십시오. 자격 증명을 찾으려면 [!DNL Platform]에 로그인하고 **[!UICONTROL 쿼리]**&#x200B;를 클릭한 다음 **[!UICONTROL 자격 증명]**&#x200B;을 클릭합니다.

![](../images/clients/aqua-data-studio/register-server-general-tab.png)

**[!UICONTROL 드라이버]** 탭을 선택합니다. **[!UICONTROL 매개 변수]**&#x200B;에서 값을 `?sslmode=require`로 설정합니다.

![](../images/clients/aqua-data-studio/register-server-driver-tab.png)

연결 세부 사항을 입력한 후 **[!UICONTROL 연결 테스트]**&#x200B;를 클릭하여 자격 증명이 제대로 작동하는지 확인합니다. 연결이 성공하면 **[!UICONTROL 저장]**&#x200B;을 클릭하여 서버를 등록합니다. 등록이 완료되면 **대시보드**&#x200B;에 연결이 나타나 서버에 연결하고 해당 스키마 개체를 볼 수 있습니다.

## 다음 단계

[!DNL Query Service]에 연결되었으므로 [!DNL Aqua Data Studio] 내에 **[!UICONTROL 쿼리 분석기]**&#x200B;를 사용하여 SQL 문을 실행하고 편집할 수 있습니다. 쿼리를 작성하고 실행하는 방법에 대한 자세한 내용은 [쿼리 실행 안내서](../best-practices/writing-queries.md)를 참조하십시오.