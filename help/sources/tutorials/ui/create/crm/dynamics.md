---
keywords: Experience Platform;홈;인기 항목;Microsoft Dynamics;microsoft dynamics;Dynamics;dynamics;dynamics
solution: Experience Platform
title: UI에서 Microsoft Dynamics Source 연결 만들기
type: Tutorial
description: Adobe Experience Platform UI를 사용하여 Microsoft Dynamics 소스 연결을 만드는 방법을 알아봅니다.
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 1%

---

# UI에서 [!DNL Microsoft Dynamics] 소스 연결 만들기

이 자습서에서는 Adobe Experience Platform UI를 사용하여 [!DNL Microsoft Dynamics]&#x200B;(이하 &quot;[!DNL Dynamics]&quot;) 소스 연결을 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): Experience Platform에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 유효한 [!DNL Dynamics] 계정이 있는 경우 이 문서의 나머지 부분을 건너뛰고 [CRM 원본에 대한 데이터 흐름을 구성하는 중](../../dataflow/crm.md)에 대한 자습서로 진행할 수 있습니다.

### 필요한 자격 증명 수집

[!DNL Dynamics] 원본을 인증하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

>[!BEGINTABS]

>[!TAB 기본 인증]

| 자격 증명 | 설명 |
| --- | --- |
| `serviceUri` | [!DNL Dynamics] 인스턴스의 서비스 URL. |
| `username` | [!DNL Dynamics] 사용자 계정의 사용자 이름입니다. |
| `password` | [!DNL Dynamics] 계정의 암호입니다. |

>[!TAB 서비스 주체 및 키 인증]

| 자격 증명 | 설명 |
| --- | --- |
| `servicePrincipalId` | [!DNL Dynamics] 계정의 클라이언트 ID. 서비스 주체 및 키 기반 인증을 사용할 때 이 ID가 필요합니다. |
| `servicePrincipalKey` | 서비스 주체 비밀 키. 서비스 주체 및 키 기반 인증을 사용할 때 이 자격 증명이 필요합니다. |

>[!ENDTABS]

시작하기에 대한 자세한 내용은 [이 [!DNL Dynamics] 문서](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)를 참조하세요.

## [!DNL Dynamics] 계정 연결

Experience Platform UI의 왼쪽 탐색에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 [!UICONTROL 소스] 작업 영역에 액세스합니다. [!UICONTROL 카탈로그] 화면에 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

[!UICONTROL CRM] 범주에서 **[!UICONTROL Microsoft Dynamics]**&#x200B;을 선택한 다음 **[!UICONTROL 데이터 추가]**&#x200B;를 선택합니다.

![Microsoft Dynamics이 포함된 소스 카탈로그를 선택했습니다.](../../../../images/tutorials/create/ms-dynamics/catalog.png)

**[!UICONTROL Microsoft Dynamics 계정 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정을 사용하려면 사용할 [!DNL Dynamics] 계정을 선택한 다음 오른쪽 상단에서 **[!UICONTROL 다음]**&#x200B;을(를) 선택하여 계속하십시오.

![기존 계정 인터페이스](../../../../images/tutorials/create/ms-dynamics/existing.png)

### 새 계정

>[!TIP]
>
>만든 후에는 [!DNL Dynamics] 기본 연결의 인증 유형을 변경할 수 없습니다. 인증 유형을 변경하려면 새 기본 연결을 만들어야 합니다.

새 계정을 만들려면 **[!UICONTROL 새 계정]**&#x200B;을(를) 선택한 다음 새 [!DNL Dynamics] 계정에 대한 이름과 선택적 설명을 입력하십시오.

![새 계정 만들기 인터페이스입니다.](../../../../images/tutorials/create/ms-dynamics/new.png)

[!DNL Dynamics] 계정을 만들 때 기본 인증이나 서비스 주체 및 키 인증을 사용할 수 있습니다.

>[!BEGINTABS]

>[!TAB 기본 인증]

기본 인증을 사용하여 [!DNL Dynamics] 계정을 만들려면 [!UICONTROL 기본 인증]을 선택한 다음 [!UICONTROL 서비스 URI], [!UICONTROL 사용자 이름] 및 [!UICONTROL 암호]에 대한 값을 제공하십시오. **참고**: [!DNL Dynamics]의 기본 인증은 현재 Experience Platform에서 지원하지 않는 이중 인증에 의해 차단될 수 있습니다. 이 경우 [!DNL Dynamics]을(를) 사용하여 소스 커넥터를 만들려면 키 기반 인증을 사용하는 것이 좋습니다.

완료되면 **[!UICONTROL 소스에 연결]**&#x200B;을 선택한 다음 새 계정을 설정할 시간을 허용하세요.

![기본 인증 인터페이스](../../../../images/tutorials/create/ms-dynamics/basic-authentication.png)

>[!TAB 서비스 주체 및 키 인증]

서비스 주체 및 키 인증을 사용하여 [!DNL Dynamics] 계정을 만들려면 **[!UICONTROL 서비스 주체 및 키 인증]**&#x200B;을 선택한 다음 [!UICONTROL 서비스 주체 ID] 및 [!UICONTROL 서비스 주체 키]에 대한 값을 제공하십시오.

완료되면 **[!UICONTROL 소스에 연결]**&#x200B;을 선택한 다음 새 계정을 설정할 시간을 허용하세요.

![서비스 주체 키 인증 인터페이스입니다.](../../../../images/tutorials/create/ms-dynamics/service-principal.png)

>[!ENDTABS]

## 다음 단계

이 자습서에 따라 [!DNL Dynamics] 계정에 대한 연결을 설정했습니다. 이제 다음 자습서를 계속 진행하고 [데이터를 Experience Platform으로 가져오도록 데이터 흐름을 구성](../../dataflow/crm.md)할 수 있습니다.
