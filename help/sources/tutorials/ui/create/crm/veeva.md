---
keywords: Experience Platform;홈;인기 항목;Veeva CRM;veeva
solution: Experience Platform
title: UI에서 Veeva CRM Source 연결 만들기
type: Tutorial
description: Adobe Experience Platform UI를 사용하여 Veeva CRM 소스 연결을 만드는 방법을 알아봅니다.
exl-id: 4ef76c28-9bd2-4e54-a3d6-dceb89162337
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 2%

---

# UI에서 [!DNL Veeva CRM] 소스 연결 만들기

Adobe Experience Platform의 Source 커넥터는 외부 소스 CRM 데이터를 일정에 따라 수집하는 기능을 제공합니다. 이 자습서에서는 [!DNL Experience Platform] 사용자 인터페이스를 사용하여 [!DNL Veeva CRM] 소스 커넥터를 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): [!DNL Experience Platform]에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 유효한 [!DNL Veeva CRM] 계정이 있는 경우 이 문서의 나머지 부분을 건너뛰고 [데이터 흐름 구성](../../dataflow/crm.md)에 대한 자습서로 진행할 수 있습니다.

### 필요한 자격 증명 수집

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `environmentUrl` | [!DNL Veeva CRM] 원본 인스턴스의 URL입니다. |
| `username` | [!DNL Veeva CRM] 사용자 계정의 사용자 이름입니다. |
| `password` | [!DNL Veeva CRM] 사용자 계정의 암호입니다. |
| `securityToken` | [!DNL Veeva CRM] 사용자 계정의 보안 토큰입니다. |

시작하기에 대한 자세한 내용은 이 [[!DNL Veeva CRM] 문서](https://developer.veevacrm.com/doc/Content/rest-api.htm)를 참조하세요.

## [!DNL Veeva CRM] 계정 연결

필요한 자격 증명을 수집했으면 아래 단계에 따라 [!DNL Veeva CRM] 계정을 [!DNL Experience Platform]에 연결할 수 있습니다.

Experience Platform UI의 왼쪽 탐색 모음에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 [!UICONTROL 소스] 작업 영역에 액세스합니다. [!UICONTROL 카탈로그] 화면에 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

[!UICONTROL CRM] 범주에서 **[!UICONTROL Veeva CRM]**&#x200B;을 선택한 다음 **[!UICONTROL 데이터 추가]**&#x200B;를 선택합니다.

![카탈로그](../../../../images/tutorials/create/veeva/catalog.png)

**[!UICONTROL Veeva CRM 계정 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정을 사용하려면 새 데이터 흐름을 만들 [!DNL Veeva CRM] 계정을 선택한 다음 **[!UICONTROL 다음]**&#x200B;을 선택하여 계속합니다.

![기존](../../../../images/tutorials/create/veeva/existing.png)

### 새 계정

새 계정을 만드는 경우 **[!UICONTROL 새 계정]**&#x200B;을(를) 선택한 다음 이름, 선택적 설명 및 [!DNL Veeva CRM] 자격 증명을 제공합니다. 완료되면 **[!UICONTROL 소스에 연결]**&#x200B;을 선택한 다음 새 연결을 설정할 수 있는 시간을 허용하세요.

![새로 만들기](../../../../images/tutorials/create/veeva/new.png)

## 다음 단계

이 자습서에 따라 [!DNL Veeva CRM] 계정에 대한 연결을 설정했습니다. 이제 다음 자습서를 계속 진행하고 [데이터를 Experience Platform으로 가져오도록 데이터 흐름을 구성](../../dataflow/crm.md)할 수 있습니다.
