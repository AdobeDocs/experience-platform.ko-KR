---
keywords: Experience Platform;홈;인기 항목;Microsoft Dynamics;microsoft dynamics;Dynamics;Dynamics;dynamics
solution: Experience Platform
title: UI에서 Microsoft Dynamics 소스 연결 만들기
type: Tutorial
description: Adobe Experience Platform UI를 사용하여 Microsoft Dynamics 소스 연결을 만드는 방법을 알아봅니다.
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
source-git-commit: d22c71fb77655c401f4a336e339aaf8b3125d1b6
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

# 만들기 [!DNL Microsoft Dynamics] UI의 소스 연결

이 튜토리얼에서는 [!DNL Microsoft Dynamics] (이하 &quot;라고 한다)[!DNL Dynamics]&quot;) Adobe Experience Platform UI를 사용하는 소스 연결.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 정의 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 소스의 집계 데이터를 기반으로 통합 실시간 소비자 프로필을 제공합니다.

이미 유효한 을(를) 가지고 있는 경우 [!DNL Dynamics] 계정, 이 문서의 나머지 부분을 건너뛰고 다음에 대한 자습서로 진행할 수 있습니다. [crm 소스에 대한 데이터 흐름 구성](../../dataflow/crm.md).

### 필요한 자격 증명 수집

을(를) 인증하려면 [!DNL Dynamics] source에서 다음 연결 속성에 대한 값을 제공해야 합니다.

>[!BEGINTABS]

>[!TAB 기본 인증]

| 자격 증명 | 설명 |
| --- | --- |
| `serviceUri` | 의 서비스 URL [!DNL Dynamics] 인스턴스. |
| `username` | 의 사용자 이름 [!DNL Dynamics] 사용자 계정입니다. |
| `password` | 에 대한 암호 [!DNL Dynamics] 계정입니다. |

>[!TAB 서비스 주체 및 키 인증]

| 자격 증명 | 설명 |
| --- | --- |
| `servicePrincipalId` | 에 대한 클라이언트 ID [!DNL Dynamics] 계정입니다. 서비스 주체 및 키 기반 인증을 사용할 때 이 ID가 필요합니다. |
| `servicePrincipalKey` | 서비스 주체 비밀 키. 서비스 주체 및 키 기반 인증을 사용할 때 이 자격 증명이 필요합니다. |

>[!ENDTABS]

시작하기에 대한 자세한 내용은 [이 [!DNL Dynamics] 문서](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

## 연결 [!DNL Dynamics] account

Platform UI에서 를 선택합니다. **[!UICONTROL 소스]** 을(를) 왼쪽 탐색에서 [!UICONTROL 소스] 작업 영역. 다음 [!UICONTROL 카탈로그] 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래 [!UICONTROL CRM] 범주, 선택 **[!UICONTROL Microsoft Dynamics]**&#x200B;을 선택한 다음 을 선택합니다 **[!UICONTROL 데이터 추가]**.

![Microsoft Dynamics가 선택된 소스 카탈로그입니다.](../../../../images/tutorials/create/ms-dynamics/catalog.png)

다음 **[!UICONTROL Microsoft Dynamics 계정 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정을 사용하려면 [!DNL Dynamics] 사용할 계정을 선택한 다음 **[!UICONTROL 다음]** 오른쪽 상단 모서리에서 을 참조하십시오.

![기존 계정 인터페이스.](../../../../images/tutorials/create/ms-dynamics/existing.png)

### 새 계정

>[!TIP]
>
>만든 후에는 의 인증 유형을 변경할 수 없습니다. [!DNL Dynamics] 기본 연결. 인증 유형을 변경하려면 새 기본 연결을 만들어야 합니다.

새 계정을 만들려면 다음을 선택합니다. **[!UICONTROL 새 계정]**&#x200B;을 클릭하고 새 항목의 이름과 설명(선택 사항)을 입력합니다 [!DNL Dynamics] 계정입니다.

![새 계정 생성 인터페이스.](../../../../images/tutorials/create/ms-dynamics/new.png)

다음을 만들 때 기본 인증 또는 서비스 주체 및 키 인증을 사용할 수 있습니다. [!DNL Dynamics] 계정입니다.

>[!BEGINTABS]

>[!TAB 기본 인증]

을(를) 만들려면 [!DNL Dynamics] 기본 인증을 가진 계정에서 다음을 선택합니다. [!UICONTROL 기본 인증] 그런 다음 의 값을 제공합니다. [!UICONTROL 서비스 URI], [!UICONTROL 사용자 이름], 및 [!UICONTROL 암호]. **참고**: 의 기본 인증 [!DNL Dynamics] 는 현재 Platform에서 지원하지 않는 이중 인증에 의해 차단될 수 있습니다. 이 경우 를 사용하여 소스 커넥터를 만들려면 키 기반 인증을 사용하는 것이 좋습니다. [!DNL Dynamics].

완료되면 다음을 선택합니다. **[!UICONTROL 소스에 연결]** 그런 다음 새 계정을 설정하는 데 시간이 걸릴 수 있습니다.

![기본 인증 인터페이스입니다.](../../../../images/tutorials/create/ms-dynamics/basic-authentication.png)

>[!TAB 서비스 주체 및 키 인증]

을(를) 만들려면 [!DNL Dynamics] 서비스 주체 및 키 인증이 있는 계정에서 다음을 선택합니다. **[!UICONTROL 서비스 주체 및 키 인증]** 그런 다음 의 값을 제공합니다. [!UICONTROL 서비스 사용자 ID] 및 [!UICONTROL 서비스 주체 키].

완료되면 다음을 선택합니다. **[!UICONTROL 소스에 연결]** 그런 다음 새 계정을 설정하는 데 시간이 걸릴 수 있습니다.

![서비스 주체 키 인증 인터페이스입니다.](../../../../images/tutorials/create/ms-dynamics/service-principal.png)

>[!ENDTABS]

## 다음 단계

이 자습서를 따라 [!DNL Dynamics] 계정입니다. 이제 다음 튜토리얼을 계속 진행하여 [데이터를 Platform으로 가져오는 데이터 흐름 구성](../../dataflow/crm.md).
