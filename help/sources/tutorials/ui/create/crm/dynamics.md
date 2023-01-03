---
keywords: Experience Platform;홈;인기 항목;Microsoft Dynamics;microsoft dynamics;Dynamics;Dynamics
solution: Experience Platform
title: UI에서 Microsoft Dynamics 소스 연결 만들기
topic-legacy: overview
type: Tutorial
description: Adobe Experience Platform UI를 사용하여 Microsoft Dynamics 소스 연결을 만드는 방법을 알아봅니다.
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 1%

---

# 만들기 [!DNL Microsoft Dynamics] UI의 소스 연결

이 자습서에서는 을(를) 만드는 단계를 제공합니다 [!DNL Microsoft Dynamics] (이하 &quot;라 한다)[!DNL Dynamics]&quot;) Adobe Experience Platform UI를 사용하여 소스를 연결할 수 있습니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 작성 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 빌딩 블록에 대해 알아봅니다.
   * [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아보십시오.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 유효한 [!DNL Dynamics] account, 이 문서의 나머지 부분을 건너뛰고 다음 자습서를 진행할 수 있습니다. [CRM 소스에 대한 데이터 흐름 구성](../../dataflow/crm.md).

### 필요한 자격 증명 수집

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `serviceUri` | 서비스 URL입니다 [!DNL Dynamics] 인스턴스. |
| `username` | 사용자의 사용자 이름 [!DNL Dynamics] 사용자 계정. |
| `password` | 사용자 [!DNL Dynamics] 계정이 필요합니다. |
| `servicePrincipalId` | 사용자의 클라이언트 ID [!DNL Dynamics] 계정이 필요합니다. 이 ID는 서비스 주체 및 키 기반 인증을 사용할 때 필요합니다. |
| `servicePrincipalKey` | 서비스 주 비밀 키입니다. 이 자격 증명은 서비스 주 및 키 기반 인증을 사용할 때 필요합니다. |

시작하는 방법에 대한 자세한 내용은 [이 [!DNL Dynamics] 문서](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## 연결 [!DNL Dynamics] account

필요한 자격 증명을 수집하면 아래 단계에 따라 를 연결할 수 있습니다 [!DNL Dynamics] Platform에 계정을 설정합니다.

에 로그인합니다. [Adobe Experience Platform](https://platform.adobe.com) 그런 다음 **[!UICONTROL 소스]** 왼쪽 탐색 모음에서 를 클릭하여 [!UICONTROL 소스] 작업 공간. 다음 **[!UICONTROL 카탈로그]** 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래에 **[!UICONTROL CRM]** 카테고리, 선택 **[!UICONTROL Microsoft Dynamics]**. 이 커넥터를 처음 사용하는 경우 **[!UICONTROL 구성]**. 그렇지 않으면 을 선택합니다. **[!UICONTROL 데이터 추가]** 새 [!DNL Dynamics] 커넥터.

![카탈로그](../../../../images/tutorials/create/ms-dynamics/catalog.png)

다음 **[!UICONTROL Dynamics에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 새 계정

새 자격 증명을 사용하는 경우 **[!UICONTROL 새 계정]**. 표시되는 입력 양식에서 새 페이지의 이름과 선택적 설명을 제공합니다 [!DNL Dynamics] 계정이 필요합니다.

다음 [!DNL Dynamics] 커넥터는 액세스를 위한 다양한 인증 유형을 제공합니다. 아래 [!UICONTROL 계정 인증] 선택 **[!UICONTROL 기본 인증]** 암호 기반 자격 증명을 사용하려면

완료되면 을 선택합니다 **[!UICONTROL 소스에 연결]** 그런 다음 새 계정이 설정될 시간을 허용합니다.

![기본 인증](../../../../images/tutorials/create/ms-dynamics/basic-auth.png)

또는 다음을 선택할 수 있습니다 **[!UICONTROL 서비스 주체 및 키 인증]** 연결 [!DNL Dynamics] 의 조합을 사용한 계정 [!UICONTROL 서비스 주체 ID] 및 [!UICONTROL 서비스 사용자 키].

>[!IMPORTANT]
>
> 의 기본 인증 [!DNL Dynamics] 이중 인증으로 차단될 수 있으며, 현재 Platform에서 지원하지 않습니다. 이 경우 키 기반 인증을 사용하여 [!DNL Dynamics].

![키 기반 인증](../../../../images/tutorials/create/ms-dynamics/key-based-auth.png)

| 자격 증명 | 설명 |
| ---------- | ----------- |
| [!UICONTROL 서비스 주체 ID] | 사용자의 클라이언트 ID [!DNL Dynamics] 계정이 필요합니다. 이 ID는 서비스 주체 및 키 기반 인증을 사용할 때 필요합니다. |
| [!UICONTROL 서비스 사용자 키] | 서비스 주 비밀 키입니다. 이 자격 증명은 서비스 주 및 키 기반 인증을 사용할 때 필요합니다. |

### 기존 계정

기존 계정을 연결하려면 [!DNL Dynamics] 연결할 계정을 선택한 다음 **[!UICONTROL 다음]** 오른쪽 위 모서리에서 진행하십시오.

![기존](../../../../images/tutorials/create/ms-dynamics/existing.png)

## 다음 단계

이 자습서에 따라 [!DNL Dynamics] 계정이 필요합니다. 이제 다음 자습서를 계속 진행하고 [데이터를 플랫폼으로 가져오도록 데이터 흐름 구성](../../dataflow/crm.md).
