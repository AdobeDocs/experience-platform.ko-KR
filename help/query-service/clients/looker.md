---
keywords: Experience Platform;홈;인기 항목;쿼리 서비스;쿼리 서비스;조회;조회;쿼리 서비스에 연결
solution: Experience Platform
title: 조회 서비스에 연결
topic-legacy: connect
description: 이 문서에서는 Adobe Experience Platform 쿼리 서비스와 전환 확인을 연결하는 단계를 설명합니다.
exl-id: 806e9077-533a-4546-b5ca-8124751957f5
source-git-commit: 910a38ccb556ec427584d9b522e29f6877d1c987
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# [!DNL Looker]을 쿼리 서비스에 연결

이 문서에서는 [!DNL Looker]과 Adobe Experience Platform [!DNL Query Service]을 연결하는 단계를 설명합니다.

>[!NOTE]
>
> 이 안내서에서는 이미 [!DNL Looker]에 액세스할 수 있고 인터페이스를 탐색하는 방법을 잘 알고 있다고 가정합니다. [!DNL Looker]에 대한 자세한 내용은 [공식 [!DNL Looker] 설명서](https://docs.looker.com/)에서 확인할 수 있습니다.

[!DNL Looker]에 로그인한 후 **[!DNL Admin]**, **[!DNL Connections]**&#x200B;를 차례로 선택합니다.

![](../images/clients/looker/click-admin-connections.png)

이 페이지에서 **[!DNL New Connection]** 을 선택합니다.

![](../images/clients/looker/click-new-connection.png)

여기에서 연결 설정에 대한 세부 정보를 입력할 수 있습니다.

![](../images/clients/looker/new-connection.png)

- **[!DNL Name]:** 연결의 이름입니다.
- **[!DNL Dialect]** : SQL 데이터베이스에 사용되는 언어입니다. [!DNL Query Service] 사용  **[!DNL PostgreSQL]**.
- **[!DNL Host and Port]** : 호스트 엔드포인트와  [!DNL Query Service]포트입니다.
- **[!DNL Database]:** 사용할 데이터베이스입니다.
- **[!DNL Username and Password]:** 사용할 로그인 자격 증명입니다. 사용자 이름은 `ORG_ID@AdobeOrg` 형식입니다.

>[!NOTE]
>
>호스트 및 포트, 데이터베이스 이름 및 로그인 자격 증명을 찾는 방법에 대한 자세한 내용은 [자격 증명 안내서](../ui/credentials.md)를 참조하십시오. 자격 증명을 찾으려면 [!DNL Platform]에 로그인한 다음 **[!UICONTROL 쿼리]**, 자격 증명&#x200B;]**을 차례로 선택하십시오.**[!UICONTROL 

연결 세부 정보를 입력한 후 **[!DNL Test These Settings]**&#x200B;을 선택하여 자격 증명이 제대로 작동하는지 확인합니다. 연결된 경우 아래에 연결할 수 있다는 메시지가 표시됩니다. 연결이 실제로 성공하면 **[!DNL Add Connection]** 을 선택하여 연결을 만듭니다.

![](../images/clients/looker/click-test-connection.png)

## 다음 단계

이제 [!DNL Query Service]과 연결되었으므로 [!DNL Looker]을 사용하여 쿼리를 작성할 수 있습니다. 쿼리를 작성하고 실행하는 방법에 대한 자세한 내용은 [쿼리 실행 안내서](../best-practices/writing-queries.md)를 참조하십시오.
