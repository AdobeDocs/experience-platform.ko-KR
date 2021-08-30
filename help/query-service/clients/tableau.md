---
keywords: Experience Platform;홈;인기 항목;타블로;쿼리 서비스;쿼리 서비스;쿼리 서비스에 연결;
solution: Experience Platform
title: 쿼리 서비스에 타블로 연결
topic-legacy: connect
description: 이 문서에서는 Tableau와 Adobe Experience Platform 쿼리 서비스를 연결하는 단계를 설명합니다.
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: 910a38ccb556ec427584d9b522e29f6877d1c987
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 3%

---

# [!DNL Tableau]을 쿼리 서비스에 연결

이 문서에서는 Tableau와 Adobe Experience Platform [!DNL Query Service]을 연결하는 단계를 설명합니다.

>[!NOTE]
>
> 이 안내서에서는 이미 [!DNL Tableau]에 액세스할 수 있고 인터페이스를 탐색하는 방법을 잘 알고 있다고 가정합니다. [!DNL Tableau]에 대한 자세한 내용은 [공식 [!DNL Tableau] 설명서](https://help.tableau.com/current/pro/desktop/en-us/default.htm)에서 확인할 수 있습니다.

[!DNL Tableau]을 [!DNL Query Service]에 연결하려면 [!DNL Tableau]를 열고 **[!DNL To a Server]** 섹션에서 **[!DNL More]** 다음에 **[!DNL PostgreSQL]**&#x200B;를 선택하십시오

![](../images/clients/tableau/open-connection.png)

이제 Adobe Experience Platform에 연결할 값을 입력할 수 있습니다. 데이터베이스 이름, 호스트, 포트 및 로그인 자격 증명을 찾는 방법에 대한 자세한 내용은 [자격 증명 안내서](../ui/credentials.md)를 참조하십시오. 자격 증명을 찾으려면 [!DNL Platform]에 로그인한 다음 **[!UICONTROL 쿼리]**, 자격 증명&#x200B;]**을 차례로 선택하십시오.**[!UICONTROL 

연결을 시도하기 전에 **[!UICONTROL SSL Required]** 상자를 선택했는지 확인합니다.

모든 자격 증명을 입력한 후 **[!DNL Sign In]**&#x200B;을 선택하여 계속하십시오.

![](../images/clients/tableau/sign-in.png)

이제 Adobe Experience Platform과 연결되었으며 테이블 목록이 측면에 표시됩니다.

![](../images/clients/tableau/connected.png)

## 다음 단계

이제 [!DNL Query Service]과 연결되었으므로 [!DNL Tableau]을 사용하여 쿼리를 작성할 수 있습니다. 쿼리를 작성하고 실행하는 방법에 대한 자세한 내용은 [쿼리 실행](../best-practices/writing-queries.md)에 대한 안내서를 참조하십시오.
