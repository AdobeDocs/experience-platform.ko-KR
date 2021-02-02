---
keywords: Experience Platform;홈;인기 항목;Microsoft Dynamics;microsoft dynamics;Dynamics;Dynamics
solution: Experience Platform
title: UI에서 Microsoft Dynamics 소스 커넥터 만들기
topic: overview
type: Tutorial
description: 이 자습서에서는 플랫폼 사용자 인터페이스를 사용하여 Microsoft Dynamics(이하 "Dynamics") 소스 커넥터를 만드는 단계를 제공합니다.
translation-type: tm+mt
source-git-commit: 4241e00fd444969e5a40c8b34dd7786b1a3c6dcb
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 0%

---


# UI에 [!DNL Microsoft Dynamics] 소스 커넥터 만들기

이 자습서에서는 플랫폼 사용자 인터페이스를 사용하여 [!DNL Microsoft Dynamics](이하 &quot;[!DNL Dynamics]&quot;) 소스 커넥터를 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md):Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md):스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 블록에 대해 알아봅니다.
   * [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md):스키마 편집기 UI를 사용하여 사용자 정의 스키마를 생성하는 방법을 알아봅니다.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 유효한 [!DNL Dynamics] 계정이 있는 경우 이 문서의 나머지 부분을 건너뛰고 CRM 소스](../../dataflow/crm.md)에 대한 데이터 흐름 구성의 자습서로 진행할 수 있습니다.[

### 필요한 자격 증명 수집

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `serviceUri` | [!DNL Dynamics] 인스턴스의 서비스 URL입니다. |
| `username` | [!DNL Dynamics] 사용자 계정의 사용자 이름입니다. |
| `password` | [!DNL Dynamics] 계정의 암호입니다. |
| `servicePrincipalId` | [!DNL Dynamics] 계정의 클라이언트 ID. 이 ID는 서비스 주체와 키 기반 인증을 사용할 때 필요합니다. |
| `servicePrincipalKey` | 서비스 주체 비밀 키입니다. 이 자격 증명은 서비스 주체 및 키 기반 인증을 사용하는 경우에 필요합니다. |

시작하는 방법에 대한 자세한 내용은 [이 [!DNL Dynamics] document](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)를 참조하십시오.

## [!DNL Dynamics] 계정 연결

필요한 자격 증명을 수집했으면 아래 단계에 따라 [!DNL Dynamics] 계정을 플랫폼에 연결할 수 있습니다.

[Adobe Experience Platform](https://platform.adobe.com)에 로그인한 다음 왼쪽 탐색 막대에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 [!UICONTROL 소스] 작업 영역에 액세스합니다. **[!UICONTROL 카탈로그]** 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면의 왼쪽에 있는 카탈로그에서 적절한 범주를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

**[!UICONTROL CRM]** 범주에서 **[!UICONTROL Microsoft Dynamics]**&#x200B;을 선택합니다. 이 커넥터를 처음 사용하는 경우 **[!UICONTROL 구성]**&#x200B;을 선택합니다. 그렇지 않은 경우 **[!UICONTROL 데이터 추가]**&#x200B;를 선택하여 새 [!DNL Dynamics] 커넥터를 만듭니다.

![카탈로그](../../../../images/tutorials/create/ms-dynamics/catalog.png)

**[!UICONTROL Connect to Dynamics]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명이나 기존 자격 증명을 사용할 수 있습니다.

### 새 계정

새 자격 증명을 사용 중인 경우 **[!UICONTROL 새 계정]**&#x200B;을 선택합니다. 표시되는 입력 양식에서 새 [!DNL Dynamics] 계정에 대한 이름과 선택적 설명을 입력합니다.

[!DNL Dynamics] 커넥터는 액세스할 수 있는 다른 인증 유형을 제공합니다. 암호 기반 자격 증명을 사용하려면 [!UICONTROL 계정 인증] 아래에서 **[!UICONTROL 기본 인증]**&#x200B;을 선택합니다.

완료되면 **[!UICONTROL 소스 연결]**&#x200B;을 선택한 다음 새 계정이 설정될 때까지 잠시 기다려 주십시오.

![기본 인증](../../../../images/tutorials/create/ms-dynamics/basic-auth.png)

또는 **[!UICONTROL 서비스 주체와 키 인증]**&#x200B;을 선택하고 [!UICONTROL 서비스 주체 ID] 및 [!UICONTROL 서비스 주 키]의 조합을 사용하여 [!DNL Dynamics] 계정을 연결할 수 있습니다.

>[!IMPORTANT]
>
> [!DNL Dynamics]의 기본 인증은 현재 플랫폼에서 지원되지 않는 2단계 인증에 의해 차단될 수 있습니다. 이 경우 키 기반 인증을 사용하여 [!DNL Dynamics]을(를) 사용하여 소스 커넥터를 만드는 것이 좋습니다.

![키 기반 인증](../../../../images/tutorials/create/ms-dynamics/key-based-auth.png)

| 자격 증명 | 설명 |
| ---------- | ----------- |
| [!UICONTROL 서비스 주체 ID] | [!DNL Dynamics] 계정의 클라이언트 ID. 이 ID는 서비스 주체와 키 기반 인증을 사용할 때 필요합니다. |
| [!UICONTROL 서비스 주체 키] | 서비스 주체 비밀 키입니다. 이 자격 증명은 서비스 주체 및 키 기반 인증을 사용하는 경우에 필요합니다. |

### 기존 계정

기존 계정을 연결하려면 연결할 [!DNL Dynamics] 계정을 선택한 다음, 계속하려면 오른쪽 위 모서리에서 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

![기존](../../../../images/tutorials/create/ms-dynamics/existing.png)

## 다음 단계

이 자습서를 따라 [!DNL Dynamics] 계정에 대한 연결을 설정했습니다. 이제 다음 튜토리얼로 계속 이동하여 [데이터 흐름을 구성하여 Platform](../../dataflow/crm.md)으로 데이터를 가져올 수 있습니다.