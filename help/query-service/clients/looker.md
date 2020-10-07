---
keywords: Experience Platform;home;popular topics;Query service;query service;Looker;looker;connect to query service;
solution: Experience Platform
title: 룩과 연결
topic: connect
description: 이 문서에서는 Looker와 Adobe Experience Platform 쿼리 서비스를 연결하는 단계를 안내합니다.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# 연결 대상 [!DNL Looker]

Adobe Experience Platform [!DNL Looker] 에서 [!DNL Query Service] 연결하려면 아래 단계를 따르십시오.

로그인한 후 관리 [!DNL Looker]를 **[!UICONTROL 클릭한]**&#x200B;다음 **[!UICONTROL 연결을 클릭합니다]**.

![](../images/clients/looker/click-admin-connections.png)

이 페이지에서 새 연결을 **클릭합니다**.

![](../images/clients/looker/click-new-connection.png)

여기에서 연결 설정에 대한 세부 정보를 입력할 수 있습니다.

![](../images/clients/looker/new-connection.png)

- **이름:** 연결 이름입니다.
- **방언:** SQL 데이터베이스에 사용되는 언어입니다. [!DNL Query Service] 를 사용합니다 **[!DNL PostgreSQL]**.
- **호스트 및 포트:** 호스트 끝점 및 해당 포트 [!DNL Query Service].
- **데이터베이스:** 사용할 데이터베이스입니다.
- **사용자 이름 및 암호:** 사용할 로그인 자격 증명입니다. 사용자 이름은 다음 형식으로 `ORG_ID@AdobeOrg`표시됩니다.

>[!NOTE]
>
>호스트 및 포트, 데이터베이스 이름 및 로그인 자격 증명을 찾는 방법에 대한 자세한 내용은 플랫폼의 [자격 증명 페이지를 참조하십시오](https://platform.adobe.com/query/configuration). 자격 증명을 찾으려면 로그인하고 쿼리 [!DNL Platform]를 **[!UICONTROL 클릭한 다음 자격 증명]**&#x200B;을 **[!UICONTROL 클릭합니다]**.

연결 세부 사항을 입력한 후 [ **[!UICONTROL 이 설정]** 테스트]를 클릭하여 자격 증명이 제대로 작동하는지 확인합니다. 이러한 경우 연결할 수 있다는 메시지가 아래에 표시됩니다. 연결이 성공적으로 완료되면 연결 **[!UICONTROL 추가를]** 클릭하여 연결을 만듭니다.

![](../images/clients/looker/click-test-connection.png)

## 다음 단계

이제 연결되었으므로 쿼리 [!DNL Query Service]를 작성할 수 [!DNL Looker] 있습니다. 쿼리를 작성하고 실행하는 방법에 대한 자세한 내용은 [실행 쿼리 안내서를 참조하십시오](../creating-queries/creating-queries.md).