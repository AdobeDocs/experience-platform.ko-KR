---
keywords: Experience Platform;home;popular topics;Query Service;Looker;looker;Connect to query service;;home;popular topics service;query service;looker;query service;
solution: Experience Platform
title: 쿼리 서비스에 연결 보기
topic-legacy: connect
description: 이 문서에서는 Looker와 Adobe Experience Platform 쿼리 서비스를 연결하는 단계를 안내합니다.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# 쿼리 서비스에 [!DNL Looker] 연결

이 문서에서는 [!DNL Looker]과(와) Adobe Experience Platform [!DNL Query Service]을(를) 연결하는 단계를 다룹니다.

>[!NOTE]
>
> 이 안내서에서는 사용자가 이미 [!DNL Looker]에 액세스할 수 있으며 인터페이스를 탐색하는 방법에 익숙하다고 가정합니다. [!DNL Looker]에 대한 자세한 내용은 [공식 [!DNL Looker] 설명서](https://docs.looker.com/)에서 확인할 수 있습니다.

[!DNL Looker]에 로그인한 후 **[!DNL Admin]**&#x200B;을 선택하고 **[!DNL Connections]**&#x200B;를 차례로 선택합니다.

![](../images/clients/looker/click-admin-connections.png)

이 페이지에서 **[!DNL New Connection]**&#x200B;을 선택합니다.

![](../images/clients/looker/click-new-connection.png)

여기에서 연결 설정에 대한 세부 정보를 입력할 수 있습니다.

![](../images/clients/looker/new-connection.png)

- **[!DNL Name]:** 연결 이름입니다.
- **[!DNL Dialect]:** SQL 데이터베이스에 사용되는 언어입니다. [!DNL Query Service] 를 사용합니다 **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]:** 호스트 끝점과 해당 포트 [!DNL Query Service]입니다.
- **[!DNL Database]** : 사용할 데이터베이스입니다.
- **[!DNL Username and Password]** : 사용할 로그인 자격 증명입니다. 사용자 이름은 `ORG_ID@AdobeOrg` 형식입니다.

>[!NOTE]
>
>호스트 및 포트, 데이터베이스 이름 및 로그인 자격 증명을 찾는 방법에 대한 자세한 내용은 플랫폼](https://platform.adobe.com/query/configuration)의 [자격 증명 페이지를 참조하십시오. 자격 증명을 찾으려면 [!DNL Platform]에 로그인한 다음 **[!UICONTROL Queries]** 뒤에 **[!UICONTROL Credentials]**&#x200B;를 선택합니다.

연결 세부 사항을 입력한 후 자격 증명이 제대로 작동하는지 확인하려면 **[!DNL Test These Settings]**&#x200B;을 선택합니다. 이러한 경우 연결할 수 있다는 메시지가 아래에 표시됩니다. 연결이 성공적으로 완료되면 **[!DNL Add Connection]**&#x200B;을 선택하여 연결을 만듭니다.

![](../images/clients/looker/click-test-connection.png)

## 다음 단계

이제 [!DNL Query Service]에 연결되었으므로 [!DNL Looker]를 사용하여 쿼리를 작성할 수 있습니다. 쿼리를 작성하고 실행하는 방법에 대한 자세한 내용은 [쿼리 실행 안내서](../best-practices/writing-queries.md)를 참조하십시오.
