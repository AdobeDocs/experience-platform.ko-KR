---
title: 활성화 계정 관리 확장
description: 확장 활성화 계정에서 라이선스 사용 모니터링 및 올바른 권한 할당과 같은 관리 작업을 수행하는 방법에 대해 알아봅니다.
exl-id: ee0ec4b9-a083-447b-b7a7-e1307e90c646
source-git-commit: 2222e9fbf75f3082d331868f820247e0c0ce3ba2
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# 계정 관리

Audience Manager에서 대상을 수집하여 소셜 및 광고 대상으로 활성화하려면 먼저 확장된 활성화 사용자 계정을 만들고 계정을 올바른 권한 역할에 할당해야 합니다.

이 페이지에서는 Admin Console에서 사용자 계정을 만들고 확장된 활성화에 대한 올바른 권한을 할당하는 방법에 대해 설명합니다.

## 사용자 계정 만들기 {#create-users}

[!DNL Audience Manager Expanded Activation]을(를) 사용하려면 먼저 사용자 계정을 만들어야 합니다.

[!DNL Expanded Activation]의 사용자 계정을 만들려면 [Adobe Admin Console](https://helpx.adobe.com/kr/enterprise/using/manage-users-individually.html) 설명서에서 사용자 관리에 대한 지침을 따르십시오.

## 권한 역할에 사용자 추가 {#permissions}

사용자 계정을 만든 후에는 [!DNL Expanded Activation] 사용자 인터페이스의 [!DNL Expanded Activation] 권한 역할에 추가해야 합니다.

**[!UICONTROL 관리]** -> **[!UICONTROL 권한]** -> **[!UICONTROL 역할]**(으)로 이동한 다음 **[!UICONTROL 확장된 활성화 기본 역할]**&#x200B;을 선택합니다.

![역할 페이지를 표시하는 확장된 활성화 사용자 인터페이스 이미지입니다.](assets/expanded-activation-role.png)

**[!UICONTROL 사용자]** 탭으로 이동하여 **[!UICONTROL 사용자 추가]**&#x200B;를 선택합니다.

![사용자 페이지를 표시하는 확장된 활성화 사용자 인터페이스 이미지입니다.](assets/add-users.png)

사용 가능한 목록에서 새로 만든 사용자를 선택하고 **[!UICONTROL 저장]**&#x200B;을(를) 선택합니다.

![사용자 추가 페이지를 표시하는 확장된 활성화 사용자 인터페이스 이미지입니다.](assets/add-user.png)

이제 사용자 계정이 만들어지고 올바른 역할에 할당됩니다. 이제 **[!UICONTROL 확장된 활성화]** 사용자 인터페이스에 액세스할 준비가 되었습니다.

## 라이선스 사용 모니터링 {#license-usage}

[!DNL Audience Manager Expanded Activation] 계약에서 계정에 수집할 수 있는 해시된 이메일의 최대 수를 지정합니다.

**[!UICONTROL 관리]** -> **[!UICONTROL 라이선스 사용량]** 페이지로 이동하여 이 정보를 찾을 수 있습니다.

![라이선스 사용 화면을 표시하는 확장된 활성화 사용자 인터페이스 이미지입니다.](assets/license-usage.png)

이 페이지에서 다음 정보를 찾을 수 있습니다.

* **[!UICONTROL 제품]**: 라이선스가 부여된 Adobe 제품입니다. 항상 **[!UICONTROL Audience Manager 확장 활성화]**&#x200B;입니다.
* **[!UICONTROL 기본 지표]**: 사용을 위해 추적 중인 지표의 이름입니다. 이 값은 항상 **[!UICONTROL 주소 지정 가능 대상]**&#x200B;입니다.
* **[!UICONTROL 라이선스 양]**: 수집하도록 라이선스가 부여된 최대 해시된 이메일 수입니다.

  >[!TIP]
  >
  >[Audience Manager 원본 커넥터](../sources/connectors/adobe-applications/audience-manager.md)를 통해 해시된 전자 메일을 수집합니다. 자세한 내용은 [대상자를 활성화하는 방법](activate-audiences.md)에 대한 설명서를 참조하십시오.

* **[!UICONTROL 사용량]**: 수집한 해시된 이메일 수입니다.
* **[!UICONTROL 사용량 %]**: 사용한 라이선스 금액의 비율입니다.

Experience Platform의 라이선스 사용에 대한 자세한 내용은 [라이선스 사용 설명서](../dashboards/guides/license-usage.md)를 참조하세요.

## 다음 단계 {#next-steps}

확장 활성화에 대한 올바른 액세스 권한을 가진 사용자 계정을 하나 이상 구성했으므로, 이제 계정을 사용하여 [대상을 활성화](activate-audiences.md)할 수 있습니다.
