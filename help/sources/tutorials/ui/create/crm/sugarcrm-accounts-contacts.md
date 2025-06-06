---
title: UI에서 SugarCRM 계정 및 연락처 소스 연결 만들기
description: Adobe Experience Platform UI를 사용하여 SugarCRM 계정 및 연락처 소스 연결을 만드는 방법을 알아봅니다.
exl-id: 45840d7e-4c19-4720-8629-be446347862d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 2%

---

# UI에서 [!DNL SugarCRM Accounts & Contacts] 소스 연결 만들기

이 자습서에서는 Adobe Experience Platform 사용자 인터페이스를 사용하여 [!DNL SugarCRM Accounts & Contacts] 소스 연결을 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): [!DNL Experience Platform]에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 유효한 [!DNL SugarCRM] 계정이 있는 경우 이 문서의 나머지 부분을 건너뛰고 [데이터 흐름 구성](../../dataflow/crm.md)에 대한 자습서로 진행할 수 있습니다.

### 필요한 자격 증명 수집

[!DNL SugarCRM Accounts & Contacts]을(를) Experience Platform에 연결하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 | 예 |
| --- | --- | --- |
| `Host` | 소스가 연결되는 SugarCRM API 엔드포인트. | `developer.salesfusion.com` |
| `Username` | SugarCRM 개발자 계정 사용자 이름입니다. | `abc.def@example.com@sugarmarketdemo000.com` |
| `Password` | SugarCRM 개발자 계정 암호입니다. | `123456789` |

### Experience Platform 스키마 만들기

[!DNL SugarCRM] 소스 연결을 만들기 전에 먼저 소스에 사용할 Experience Platform 스키마를 만들어야 합니다. 스키마를 만드는 방법에 대한 포괄적인 단계를 보려면 [Experience Platform 스키마 만들기](../../../../../xdm/schema/composition.md)에 대한 자습서를 참조하십시오.

[!DNL SugarCRM Accounts & Contacts]은(는) 여러 API를 지원합니다. 즉, 활용하는 객체 유형에 따라 별도의 스키마를 만들어야 합니다. 계정 및 연락처 스키마에 대해서는 아래 예를 참조하십시오.

>[!BEGINTABS]

>[!TAB 계정]

![계정의 예제 스키마를 보여 주는 Experience Platform UI 스크린샷](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarcrm-schema-accounts.png)

>[!TAB 연락처]

![연락처에 대한 예제 스키마를 보여 주는 Experience Platform UI 스크린샷](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarcrm-schema-contacts.png)

>[!ENDTABS]

## [!DNL SugarCRM Accounts & Contacts] 계정 연결

Experience Platform UI의 왼쪽 탐색 모음에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 [!UICONTROL 소스] 작업 영역에 액세스합니다. [!UICONTROL 카탈로그] 화면에 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

*CRM* 범주에서 **[!UICONTROL SugarCRM 계정 및 연락처]**&#x200B;를 선택한 다음 **[!UICONTROL 데이터 추가]**&#x200B;를 선택합니다.

![SugarCRM 계정 및 연락처 카드가 있는 카탈로그용 Experience Platform UI 스크린샷](../../../../images/tutorials/create/sugarcrm-accounts-contacts/catalog-sugarcrm-accounts-contacts.png)

**[!UICONTROL SugarCRM 계정 및 연락처 계정 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정을 사용하려면 새 데이터 흐름을 만들 [!DNL SugarCRM Accounts & Contacts] 계정을 선택한 다음 **[!UICONTROL 다음]**&#x200B;을 선택하여 계속합니다.

![기존 계정과 Connect SugarCRM 계정 및 연락처 계정용 Experience Platform UI 스크린샷](../../../../images/tutorials/create/sugarcrm-accounts-contacts/existing.png)

### 새 계정

새 계정을 만드는 경우 **[!UICONTROL 새 계정]**&#x200B;을(를) 선택한 다음 이름, 설명(선택 사항) 및 자격 증명을 제공합니다. 완료되면 **[!UICONTROL 소스에 연결]**&#x200B;을 선택한 다음 새 연결을 설정할 수 있는 시간을 허용하세요.

![새 계정과 Connect SugarCRM 계정 및 연락처 계정용 Experience Platform UI 스크린샷](../../../../images/tutorials/create/sugarcrm-accounts-contacts/new.png)

### 데이터 선택

마지막으로 Experience Platform으로 수집할 오브젝트 유형을 선택해야 합니다.

| 오브젝트 유형 | 설명 |
| --- | --- |
| `Accounts` | 조직이 관계를 맺고 있는 회사입니다. |
| `Contacts` | 조직이 관계를 수립한 개별 사용자입니다. |

>[!BEGINTABS]

>[!TAB 계정]

![계정 옵션이 선택된 구성을 보여주는 SugarCRM 계정 및 연락처용 Experience Platform UI 스크린샷](../../../../images/tutorials/create/sugarcrm-accounts-contacts/configuration-accounts.png)

>[!TAB 연락처]

![연락처 옵션이 선택된 구성을 보여주는 SugarCRM 계정 및 연락처용 Experience Platform UI 스크린샷](../../../../images/tutorials/create/sugarcrm-accounts-contacts/configuration-contacts.png)

>[!ENDTABS]

## 다음 단계

이 자습서에 따라 [!DNL SugarCRM Accounts & Contacts] 계정에 대한 연결을 설정했습니다. 이제 다음 자습서를 계속 진행하고 [데이터를 Experience Platform으로 가져오도록 데이터 흐름을 구성](../../dataflow/crm.md)할 수 있습니다.

## 추가 리소스

아래 섹션에서는 [!DNL SugarCRM] 소스를 사용할 때 참조할 수 있는 추가 리소스를 제공합니다.

### 가드레일 {#guardrails}

[!DNL SugarCRM] API 스로틀 속도는 분당 90회 호출 또는 일별 2,000회 호출 중 먼저 발생하는 호출입니다. 하지만 연결 사양에 매개 변수를 추가하여 속도 제한에 도달하지 않도록 요청 시간을 지연시킴으로써 이러한 제한을 피할 수 있습니다.

### 유효성 검사 {#validation}

원본을 올바르게 설정했는지 확인하고 [!DNL SugarCRM Accounts & Contacts] 데이터가 수집되고 있는지 확인하려면 아래 단계를 수행하십시오.

* Experience Platform UI에서 소스 카탈로그의 [!DNL SugarCRM Accounts & Contacts] 카드 메뉴 옆에 있는 **[!UICONTROL 데이터 흐름 보기]**&#x200B;를 선택합니다. 그런 다음 **[!UICONTROL 데이터 집합 미리 보기]**&#x200B;를 선택하여 수집된 데이터를 확인합니다.

* 작업 중인 개체 유형에 따라 아래 [!DNL SugarMarket] 계정 또는 연락처 페이지에 표시되는 카운트와 비교하여 집계된 데이터를 확인할 수 있습니다.

>[!BEGINTABS]

>[!TAB 계정]

![계정 목록을 표시하는 SugarMarket 계정 페이지의 스크린샷](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarmarket-accounts.png)

>[!TAB 연락처]

![연락처 목록을 표시하는 SugarMarket 연락처 페이지의 스크린샷](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarmarket-contacts.png)

>[!ENDTABS]

>[!NOTE]
>
>[!DNL SugarMarket] 페이지에 삭제된 개체 수가 포함되어 있지 않습니다. 그러나 이 소스를 통해 검색된 데이터에는 삭제된 카운트도 포함되며 이 카운트에는 삭제된 플래그가 표시됩니다.
