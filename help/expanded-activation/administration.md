---
title: 활성화 계정 관리 확장
description: 확장 활성화 계정에서 라이선스 사용 모니터링 및 올바른 권한 할당과 같은 관리 작업을 수행하는 방법에 대해 알아봅니다.
source-git-commit: 5bc8d6c7173f221c2830a9b15c8ec6241e8bc59d
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---


# 계정 관리

Audience Manager에서 대상을 수집하여 소셜 및 광고 대상으로 활성화하려면 먼저 확장된 활성화 사용자 계정을 만들고 계정을 올바른 권한 역할에 할당해야 합니다.

이 페이지에서는 Admin Console에서 사용자 계정을 만들고 확장된 활성화에 대한 올바른 권한을 할당하는 방법에 대해 설명합니다.

## 사용자 계정 만들기 {#create-users}

을(를) 사용하기 전에 [!DNL Audience Manager Expanded Activation], 사용자 계정을 만들어야 합니다.

다음에 대한 사용자 계정을 만들려면 [!DNL Expanded Activation]에서 사용자 관리에 대한 지침을 따릅니다. [Adobe Admin Console](https://helpx.adobe.com/kr/enterprise/using/manage-users-individually.html) 설명서를 참조하십시오.

## 권한 역할에 사용자 추가 {#permissions}

사용자 계정을 만든 후에는 [!DNL Expanded Activation] 권한 역할, [!DNL Expanded Activation] 사용자 인터페이스.

다음으로 이동 **[!UICONTROL 관리]** -> **[!UICONTROL 권한]** -> **[!UICONTROL 역할]**&#x200B;을(를) 클릭하고 **[!UICONTROL 확장된 활성화 기본 역할]**.

![역할 페이지를 보여주는 확장된 활성화 사용자 인터페이스 이미지입니다.](assets/expanded-activation-role.png)

로 이동 **[!UICONTROL 사용자]** 탭하고 선택 **[!UICONTROL 사용자 추가]**.

![사용자 페이지를 보여주는 확장된 활성화 사용자 인터페이스 이미지입니다.](assets/add-users.png)

사용 가능한 목록에서 새로 생성된 사용자를 선택하고 **[!UICONTROL 저장]**.

![사용자 추가 페이지를 보여주는 확장된 활성화 사용자 인터페이스 이미지입니다.](assets/add-user.png)

이제 사용자 계정이 만들어지고 올바른 역할에 할당됩니다. 이제 액세스할 준비가 되었습니다. **[!UICONTROL 확장된 활성화]** 사용자 인터페이스.

## 라이선스 사용 모니터링 {#license-usage}

사용자 [!DNL Audience Manager Expanded Activation] contract는 계정에 수집할 수 있는 해시된 이메일의 최대 수를 지정합니다.

다음 위치로 이동하여 이 정보를 찾을 수 있습니다. **[!UICONTROL 관리]** -> **[!UICONTROL 라이선스 사용]** 페이지를 가리키도록 업데이트하는 중입니다.

![라이선스 사용 화면을 표시하는 확장된 활성화 사용자 인터페이스 이미지입니다.](assets/license-usage.png)

이 페이지에서 다음 정보를 찾을 수 있습니다.

* **[!UICONTROL 제품]**: 라이선스가 부여된 Adobe 제품입니다. 항상 다음과 같습니다. **[!UICONTROL Audience Manager 확장 활성화]**.
* **[!UICONTROL 기본 지표]**: 사용을 위해 추적 중인 지표의 이름입니다. 항상 다음과 같습니다. **[!UICONTROL 대응 가능 대상]**.
* **[!UICONTROL 라이선스 금액]**: 수집에 라이선스가 부여된 최대 해시된 이메일 수입니다.

  >[!TIP]
  >
  >다음을 통해 해시된 이메일을 수집합니다. [Audience Manager 소스 커넥터](../sources/connectors/adobe-applications/audience-manager.md). 다음에서 설명서를 참조하십시오. [대상자를 활성화하는 방법](activate-audiences.md) 을 참조하십시오.

* **[!UICONTROL 사용]**: 수집한 해시된 이메일 수입니다.
* **[!UICONTROL 사용량 %]**: 사용한 라이선스 금액의 백분율입니다.

Experience Platform에서 라이선스 사용에 대한 자세한 내용은 [라이선스 사용 설명서](../dashboards/guides/license-usage.md).

## 다음 단계 {#next-steps}

확장 활성화에 대한 올바른 액세스 권한을 가진 사용자 계정을 하나 이상 구성했으므로 이제 다음 작업을 위해 계정을 사용할 수 있습니다. [대상자 활성화](activate-audiences.md).
