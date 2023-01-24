---
title: UI에서 SugarCRM 이벤트 소스 연결 만들기
description: Adobe Experience Platform UI를 사용하여 SugarCRM 이벤트 소스 연결을 만드는 방법을 알아봅니다.
source-git-commit: 17d8a6517686ee2459955f766d75980b41851320
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 1%

---

# (베타) 만들기 [!DNL SugarCRM Events] UI의 소스 연결

>[!NOTE]
>
>다음 [!DNL SugarCRM Events] 소스가 베타 버전입니다. 자세한 내용은 [소스 개요](../../../../home.md#terms-and-conditions) 베타 레이블이 지정된 소스 사용에 대한 자세한 정보.

이 자습서에서는 을(를) 만드는 단계를 제공합니다 [!DNL SugarCRM Events] Adobe Experience Platform 사용자 인터페이스를 사용한 소스 연결.

## 시작하기

이 자습서에서는 Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): 표준화된 프레임워크 [!DNL Experience Platform] 고객 경험 데이터를 구성합니다.
   * [스키마 작성 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 빌딩 블록에 대해 알아봅니다.
   * [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아보십시오.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 유효한 [!DNL SugarCRM] account, 이 문서의 나머지 부분을 건너뛰고 다음 자습서를 진행할 수 있습니다. [데이터 흐름 구성](../../dataflow/crm.md).

### 필요한 자격 증명 수집

연결하려면 [!DNL SugarCRM Events] 플랫폼에 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 | 예 |
| --- | --- | --- |
| `Host` | 소스가 연결되는 SugarCRM API 끝점입니다. | `developer.salesfusion.com` |
| `Username` | SugarCRM 개발자 계정 사용자 이름입니다. | `abc.def@example.com@sugarmarketdemo000.com` |
| `Password` | SugarCRM 개발자 계정 암호입니다. | `123456789` |

### 용 플랫폼 스키마 만들기 [!DNL SugarCRM]

만들기 전 [!DNL SugarCRM] 소스 연결을 통해 소스에 사용할 Platform 스키마를 먼저 만들어야 합니다. 다음에서 자습서를 참조하십시오. [플랫폼 스키마 만들기](../../../../../xdm/schema/composition.md) 를 참조하십시오.

![SugarCRM 이벤트에 대한 예제 스키마를 보여주는 플랫폼 UI 스크린샷](../../../../images/tutorials/create/sugarcrm-events/sugarcrm-schema-events.png)

>[!WARNING]
>
>스키마를 매핑할 때는 필수를 매핑해야 합니다 `event_id` 및 `timestamp` 플랫폼에 필요한 필드입니다.

## 연결 [!DNL SugarCRM Events] account

플랫폼 UI에서 **[!UICONTROL 소스]** 왼쪽 탐색 모음에서 를 클릭하여 [!UICONTROL 소스] 작업 공간. 다음 [!UICONTROL 카탈로그] 화면에 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래에 *CRM* 카테고리, 선택 **[!UICONTROL SugarCRM 이벤트]**&#x200B;를 선택한 다음 을 선택합니다. **[!UICONTROL 데이터 추가]**.

![SugarCRM 이벤트 카드가 포함된 카탈로그의 Platform UI 스크린샷](../../../../images/tutorials/create/sugarcrm-events/catalog-sugarcrm-events.png)

다음 **[!UICONTROL SugarCRM 이벤트 계정 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정을 사용하려면 [!DNL SugarCRM Events] 새 데이터 흐름을 만들 계정을 선택한 다음 **[!UICONTROL 다음]** 계속 진행합니다.

![기존 계정과 SugarCRM 이벤트 계정을 연결하기 위한 플랫폼 UI 스크린샷](../../../../images/tutorials/create/sugarcrm-events/existing.png)

### 새 계정

새 계정을 만드는 경우 **[!UICONTROL 새 계정]**, 그런 다음 이름, 선택적 설명 및 자격 증명을 제공합니다. 완료되면 을 선택합니다 **[!UICONTROL 소스에 연결]** 그런 다음 새 연결이 설정될 시간을 허용합니다.

![새 계정과 SugarCRM 이벤트 계정을 연결하기 위한 플랫폼 UI 스크린샷](../../../../images/tutorials/create/sugarcrm-events/new.png)

## 다음 단계

이 자습서에 따라 [!DNL SugarCRM Events] 계정이 필요합니다. 이제 다음 자습서를 계속 진행하고 [데이터를 플랫폼으로 가져오도록 데이터 흐름 구성](../../dataflow/crm.md).

## 추가 리소스

아래 섹션에서는 를 사용할 때 참조할 수 있는 추가 리소스를 제공합니다. [!DNL SugarCRM] 소스.

### 가드레일 {#guardrails}

다음 [!DNL SugarCRM] API 스로틀 비율은 분당 90회 또는 하루에 2000회 호출(어느 쪽이든 먼저 발생함)입니다. 그러나 이 제한 사항은 연결 사양에 매개 변수를 추가하여 요청 시간을 지연시켜 비율 제한에 도달하지 않도록 했습니다.

### 유효성 검사 {#validation}

소스 및 [!DNL SugarCRM Events] 데이터를 수집하는 중입니다. 아래 단계를 수행하십시오.

* 플랫폼 UI에서 **[!UICONTROL 데이터 흐름 보기]** 옆에 [!DNL SugarCRM Events] 소스 카탈로그의 카드 메뉴. 다음 을 선택합니다. **[!UICONTROL 데이터 세트 미리 보기]** 수집된 데이터를 확인하려면

* 작업 중인 객체 유형에 따라, [!DNL SugarMarket] 아래의 이벤트 페이지:

![계정 목록을 표시하는 SugarMarket 계정 페이지의 스크린샷](../../../../images/tutorials/create/sugarcrm-events/sugarmarket-events.png)

>[!NOTE]
>
>다음 [!DNL SugarMarket] 페이지에 삭제된 개체 수가 포함되지 않습니다. 그러나 이 소스를 통해 검색된 데이터에는 삭제된 개수도 포함되며 삭제된 플래그가 표시됩니다.