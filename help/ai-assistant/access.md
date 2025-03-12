---
title: Experience Platform에서 AI Assistant 액세스
description: Experience Cloud UI에서 AI Assistant에 액세스하는 방법을 알아봅니다.
exl-id: c4cdff25-512c-4b4c-be91-ad9360067a0a
source-git-commit: 9010f430f432c5ead708c1cb01803abd7ffd86b3
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 0%

---

# Experience Platform에서 AI Assistant 액세스

Adobe Experience Cloud의 여러 애플리케이션에서 AI Assistant에 액세스할 수 있습니다.

>[!IMPORTANT]
>
>AI Assistant에 대한 액세스 권한을 얻으려면 먼저 조직이 추가 법률 약관에 동의해야 한다는 것을 알리는 팝업 메시지를 권한 UI에 수신하면 Adobe 계정 팀에 문의하여 이러한 약관에 대한 지침을 확인하십시오.

## 시작하기 {#get-started}

AI Assistant에 액세스하려면 먼저 두 가지 전제 조건 단계를 완료해야 합니다.

1. 조직은 먼저 법률 약관에 동의해야 합니다. 자세한 내용은 Adobe 계정 팀에 문의하십시오.
2. 관리자는 AI Assistant에 액세스할 수 있는 충분한 권한을 부여해야 합니다.

이 두 가지 전제 조건 단계 중 하나를 완료하지 않은 경우 Experience Platform UI에서 AI Assistant 채팅 아이콘을 선택하면 다음 메시지가 표시됩니다.

>[!BEGINTABS]

>[!TAB 조직에서 AI 도우미를 사용할 수 없습니다]

AI Assistant를 사용할 수 있는 법적 자격이 없는 조직을 사용하는 경우 다음과 같은 메시지가 표시됩니다. 이 시나리오에서는 Adobe 계정 팀에 연락하여 액세스를 해결해야 합니다.

![조직에서 AI 도우미를 사용할 수 없는 경우 Experience Platform UI에 표시되는 팝업 메시지입니다.](./images/access/modal-one.png)

>[!TAB 권한이 없습니다]

귀사에서 AI Assistant를 합법적으로 사용할 수 있는 자격이 있지만 기능에 액세스할 수 없는 경우 Experience Platform UI에 다음과 같은 메시지가 표시됩니다. 이 시나리오는 기능에 액세스할 수 있는 충분한 권한이 없으며 관리자에게 문의하여 권한을 해결해야 함을 의미합니다.

![AI Assistant에 필요한 권한이 없는 경우 Experience Platform UI에 표시되는 팝업 메시지입니다.](./images/access/modal-two.png)

>[!ENDTABS]

## AI Assistant 액세스

AI Assistant에 대한 액세스는 다음 매개 변수에 의해 제어됩니다.

* **응용 프로그램에 액세스:** Adobe Experience Platform, Adobe Real-Time CDP, Adobe Journey Optimizer 및 [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/ai-assistant)에서 AI Assistant에 액세스할 수 있습니다.
<!-- * **Contractual access:** Your company must agree to certain [!DNL GenAI]-related legal terms before your organization can use AI Assistant. Contact your organization's administrator or your Adobe Account Team if you are not able to access AI Assistant.  -->
* **권한:** [권한 UI](../access-control/abac/ui/permissions.md)를 사용하여 조직의 AI Assistant에 대한 액세스 권한을 부여하거나 취소할 수 있습니다. AI Assistant를 사용하려면 지정된 사용자가 **AI Assistant 활성화** 및 **Operational Insights 보기** 권한으로 프로비저닝된 역할에 속해야 합니다.
   * 관리자는 해당 역할에 **AI Assistant 사용**&#x200B;을 추가하고 해당 역할에 사용자를 추가하여 조직의 AI Assistant에 액세스할 수 있도록 할 수 있습니다. **참고**: 이 권한은 해당 사용자가 AI Assistant에 액세스할 수 있도록 허용하며, 다른 사용자에게 AI Assistant에 대한 액세스 권한을 부여할 수 있는 관리 기능은 부여하지 않습니다.
   * 관리자는 해당 역할에 **View Operational Insights**&#x200B;를 추가하고 해당 역할에 사용자를 추가하여 AI Assistant의 Operational Insights 기능을 사용할 수 있습니다. Operational Insights 는 현재 Beta 버전입니다.

[권한 UI](../access-control/abac/ui/roles.md)를 사용하여 Experience Platform 및 Journey Optimizer에서 AI Assistant를 사용할 수 있는 권한을 부여합니다. Customer Journey Analytics에서 AI Assistant에 액세스하는 방법에 대한 자세한 내용 [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/ai-assistant)에서 설명서를 읽어 보십시오.

![지정된 역할에 포함된 AI Assistant 사용 및 Operational Insights 보기 권한이 있는 권한 UI 페이지입니다.](./images/access/access-permissions.png)

필요한 권한이 있으면 사용 중인 애플리케이션 상단 헤더에 있는 AI Assistant 아이콘을 선택하여 AI Assistant에 액세스할 수 있습니다.

처음 사용자 경험이 있는 ![AI 길잡이](./images/access/access-home.png)

다음 비디오를 통해 조직 및 사용자를 위한 AI Assistant 액세스를 구성하는 방법에 대해 알아보십시오.

>[!VIDEO](https://video.tv.adobe.com/v/3436470/?learn=on)

## 다음 단계

AI Assistant에 대한 완전한 액세스 권한을 보유하고 나면 워크플로우에서 기능을 계속 사용할 수 있습니다. 자세한 내용은 [AI Assistant UI 안내서](./ui-guide.md)를 참조하십시오.
