---
description: Adobe Experience Platform은 데이터 수집 프로세스를 가속화하는 데 사용할 수 있는 사전 구성된 템플릿을 제공합니다. 템플릿에는 소스에서 Experience Platform으로 데이터를 가져올 때 사용할 수 있는 스키마, 데이터 세트, 매핑 규칙, ID, ID 네임스페이스 및 데이터 흐름과 같이 자동으로 생성된 자산이 포함됩니다.
title: (베타) UI에서 템플릿을 사용하여 소스 데이터 흐름 만들기
badge1: "Beta"
hide: true
hidefromtoc: true
exl-id: 48aa36ca-656d-4b9d-954c-48c8da9df1e9
source-git-commit: c4cb3783cbbab6f9bf25ffaa5b27a200c555b181
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 0%

---

# (베타) UI에서 템플릿을 사용하여 소스 데이터 흐름 만들기

>[!IMPORTANT]
>
>템플릿은 베타에 있으며 다음 소스에서 지원됩니다.
>
>* [[!DNL Marketo Engage]](../../connectors/adobe-applications/marketo/marketo.md)
>* [[!DNL Microsoft Dynamics]](../../connectors/crm/ms-dynamics.md)
>* [[!DNL Salesforce]](../../connectors/crm/salesforce.md)
>
>설명서 및 기능은 변경될 수 있습니다.

Adobe Experience Platform은 데이터 수집 프로세스를 가속화하는 데 사용할 수 있는 사전 구성된 템플릿을 제공합니다. 템플릿에는 소스에서 Experience Platform으로 데이터를 가져올 때 사용할 수 있는 스키마, 데이터 세트, ID, 매핑 규칙, ID 네임스페이스 및 데이터 흐름과 같이 자동으로 생성된 자산이 포함됩니다.

템플릿을 사용하면 다음 작업을 수행할 수 있습니다.

* 템플릿 기반의 자산 생성 가속화를 통해 수집 시간을 단축합니다.
* 수동 데이터 수집 프로세스 중에 발생할 수 있는 오류를 최소화합니다.
* 사용 사례에 맞게 자동 생성된 자산을 언제든지 업데이트합니다.

다음 자습서에서는 플랫폼 UI에서 템플릿을 사용하는 방법에 대한 단계를 제공합니다.

## 시작하기

이 자습서에서는 Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../home.md): Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [[!DNL Experience Data Model (XDM)] 시스템](../../../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
* [샌드박스](../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

## 플랫폼 UI에서 템플릿 사용 {#use-templates-in-the-platform-ui}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_accounttype"
>title="비즈니스 유형 선택"
>abstract="사용 사례에 적합한 비즈니스 유형을 선택합니다. 액세스 권한은 Real-time Customer Data Platform 구독 계정에 따라 달라질 수 있습니다."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/overview.html?lang=ko" text="Real-Time CDP 개요"

플랫폼 UI에서 **[!UICONTROL 소스]** 왼쪽 탐색에서 로 이동하여 [!UICONTROL 소스] 작업 공간 및 Experience Platform에서 사용할 수 있는 소스 카탈로그를 참조하십시오.

를 사용하십시오 *[!UICONTROL 카테고리]* 메뉴를 사용하여 범주별로 소스를 필터링합니다. 또는 검색 막대에 소스 이름을 입력하여 카탈로그에서 특정 소스를 찾습니다.

로 이동합니다. [!UICONTROL Adobe 애플리케이션] 카테고리를 클릭하여 [!DNL Marketo Engage] 소스 카드를 선택한 다음 [!UICONTROL 데이터 추가] 을 가리키도록 업데이트하는 것이 좋습니다.

![Marketo Engage 소스가 강조 표시된 소스 작업 공간의 카탈로그.](../../images/tutorials/templates/catalog.png)

템플릿을 찾아보거나 기존 스키마 및 데이터 세트를 사용할 수 있는 옵션이 표시된 팝업 창이 나타납니다.

* **템플릿 찾아보기**: 소스 템플릿은 매핑 규칙을 사용하여 스키마, ID, 데이터 세트 및 데이터 흐름을 자동으로 만듭니다. 필요에 따라 이러한 자산을 사용자 지정할 수 있습니다.
* **기존 자산 사용**: 생성한 기존 데이터 세트 및 스키마를 사용하여 데이터를 수집하십시오. 필요한 경우 새 데이터 세트 및 스키마를 생성할 수도 있습니다.

자동 생성된 자산을 사용하려면 **[!UICONTROL 템플릿 찾아보기]** 그런 다음 **[!UICONTROL 선택]**.

![템플릿을 찾아보거나 기존 자산을 사용할 수 있는 옵션이 있는 팝업 창입니다.](../../images/tutorials/templates/browse-templates.png)

### 인증

새 계정을 만들거나 기존 계정을 사용하라는 인증 단계가 나타납니다.

>[!BEGINTABS]

>[!TAB 기존 계정 사용]

기존 계정을 사용하려면 [!UICONTROL 기존 계정] 그런 다음 나타나는 목록에서 사용할 계정을 선택합니다.

![액세스할 수 있는 기존 계정 목록이 있는 기존 계정의 선택 페이지입니다.](../../images/tutorials/templates/existing-account.png)

>[!TAB 새 계정 만들기]

새 계정을 만들려면 **[!UICONTROL 새 계정]**&#x200B;소스 연결 세부 사항 및 계정 인증 자격 증명을 제공합니다. 완료되면 을 선택합니다 **[!UICONTROL 소스에 연결]** 새 연결이 설정될 때까지 잠시 기다려 주십시오.

![소스 연결 세부 정보 및 계정 인증 자격 증명이 있는 새 계정에 대한 인증 페이지입니다.](../../images/tutorials/templates/new-account.png)

>[!ENDTABS]

### 템플릿 선택

선택한 비즈니스 유형에 따라 템플릿 목록이 나타납니다. 미리 보기 아이콘을 선택합니다 ![미리 보기 아이콘](../../images/tutorials/templates/preview-icon.png) 템플릿 이름 옆에 있는 를 사용하여 템플릿의 샘플 데이터를 미리 볼 수 있습니다.

![미리 보기 아이콘이 강조 표시된 템플릿 목록입니다.](../../images/tutorials/templates/templates.png)

템플릿의 샘플 데이터를 탐색하고 검사할 수 있는 미리 보기 창이 나타납니다. 완료되면 을 선택합니다 **[!UICONTROL 알겠습니다]**.

![샘플 데이터 미리 보기 창.](../../images/tutorials/templates/preview-sample-data.png)

다음으로 목록에서 사용할 템플릿을 선택합니다. 여러 템플릿을 선택하고 한 번에 여러 데이터 흐름을 만들 수 있습니다. 그러나 템플릿은 계정당 한 번만 사용할 수 있습니다. 템플릿을 선택하면 **[!UICONTROL 완료]** 자산을 생성할 수 있도록 잠시 허용합니다.

사용 가능한 템플릿 목록에서 하나 또는 일부 항목을 선택하는 경우 스키마 간에 B2B 관계가 올바르게 구성되도록 모든 B2B 스키마와 ID 네임스페이스가 생성됩니다.

>[!NOTE]
>
>이미 사용된 템플릿은 선택 시 비활성화됩니다.

![Opportunity Contact Role 템플릿을 선택한 템플릿 목록입니다.](../../images/tutorials/templates/select-template.png)

### 일정 설정

다음 [!DNL Microsoft Dynamics] 그리고 [!DNL Salesforce] 두 소스 모두 데이터 흐름 예약을 지원합니다.

예약 인터페이스를 사용하여 데이터 흐름의 수집 일정을 구성합니다. 수집 빈도를 로 설정합니다. **한 번** 를 클릭하여 일회성 수집을 생성합니다.

![Dynamics 및 Salesforce 템플릿에 대한 예약 인터페이스입니다.](../../images/tutorials/templates/schedule.png)

또는 수집 빈도를 로 설정할 수 있습니다 **분**, **시간**, **일**, 또는 **주**. 데이터 흐름을 여러 수집으로 예약하는 경우 각 수집 사이의 시간대를 설정하려면 간격을 설정해야 합니다. 예를 들어 수집 빈도가 **시간** 그리고 **15** 은(는) 데이터 양이 모든 데이터를 수집하도록 예약되어 있음을 의미합니다 **15시간**.

이 단계 동안 다음을 활성화할 수도 있습니다 **채우기** 데이터를 증분 수집하기 위한 열을 정의합니다. 채우기(Backfill)는 이전 데이터를 수집하는 데 사용되는 반면 증분 수집에 대해 정의하는 열에서 새 데이터를 기존 데이터와 구별할 수 있습니다.

수집 일정 구성을 완료했으면 을 선택합니다 **[!UICONTROL 완료]**.

![채우기 기능이 활성화된 Dynamics 및 Salesforce 템플릿에 대한 예약 인터페이스입니다.](../../images/tutorials/templates/backfill.png)

### 자산 검토 {#review-assets}

>[!CONTEXTUALHELP]
>id="platform_sources_templates_review"
>title="자동 생성된 자산 검토"
>abstract="모든 자산을 생성하는 데 최대 5분이 걸릴 수 있습니다. 페이지에서 나가도록 선택하면 자산이 완료되면 반환되는 알림이 표시됩니다. 자산이 생성되면 자산을 검토하고 언제든지 데이터 플로우에 추가 구성을 만들 수 있습니다."

다음 [!UICONTROL 템플릿 자산 검토] 페이지에 템플릿의 일부로 자동 생성된 자산이 표시됩니다. 이 페이지에서는 소스 연결과 연결된 자동 생성된 스키마, 데이터 세트, ID 네임스페이스 및 데이터 흐름을 볼 수 있습니다. 모든 자산을 생성하는 데 최대 5분이 걸릴 수 있습니다. 페이지에서 나가도록 선택하면 자산이 완료되면 반환되는 알림이 표시됩니다. 자산이 생성되면 자산을 검토하고 언제든지 데이터 플로우에 추가 구성을 만들 수 있습니다.

자동 생성된 데이터 흐름은 기본적으로 활성화되어 있습니다. 줄임표(`...`)을 데이터 흐름 이름 옆에 둔 다음 을 선택합니다 **[!UICONTROL 미리 보기 매핑]** 데이터 플로우에 대해 생성된 매핑 세트를 확인합니다.

![미리 보기 매핑 옵션이 선택된 드롭다운 창입니다.](../../images/tutorials/templates/preview.png)

소스 데이터 필드와 대상 스키마 필드 간의 매핑 관계를 검사할 수 있는 미리 보기 페이지가 나타납니다. 데이터 흐름의 매핑을 보고 선택 **[!UICONTROL 알았어]**

![매핑 미리 보기 창입니다.](../../images/tutorials/templates/preview-mappings.png)

실행 후 언제든지 데이터 흐름을 업데이트할 수 있습니다. 줄임표(`...`)을 데이터 흐름 이름 옆에 둔 다음 을 선택합니다 **[!UICONTROL 데이터 흐름 업데이트]**. 데이터 흐름 페이지가 표시됩니다. 이 페이지에서 데이터 흐름 세부 정보(부분 수집, 오류 진단, 경고 알림 및 데이터 흐름 매핑 설정)를 업데이트할 수 있습니다.

스키마 편집기 보기를 사용하여 자동 생성된 스키마를 업데이트할 수 있습니다. 안내서의 방문 [스키마 편집기 사용](../../../xdm/tutorials/create-schema-ui.md) 추가 정보.

![데이터 흐름 업데이트 옵션이 선택된 드롭다운 창입니다.](../../images/tutorials/templates/update.png)

## 다음 단계

이제 이 자습서를 따라 템플릿을 사용하여 스키마, 데이터 세트 및 ID 네임스페이스와 같은 자산과 데이터 흐름을 만들었습니다. 소스에 대한 일반적인 정보를 보려면 [소스 개요](../../home.md).

## 부록

다음 섹션에서는 템플릿에 대한 추가 정보를 제공합니다.

### 알림 패널을 사용하여 검토 페이지로 돌아갑니다

템플릿은 Adobe Experience Platform 경고에서 지원되며, 알림 패널을 사용하여 자산 상태에 대한 업데이트를 받을 수 있고 검토 페이지로 다시 이동할 수도 있습니다.

Platform UI의 상단 헤더에서 알림 아이콘을 선택한 다음 상태 경고를 선택하여 검토할 자산을 확인합니다.

![실패한 데이터 흐름이 강조 표시되어 있음을 알리는 알림이 포함된 Platform UI의 알림 패널입니다.](../../images/tutorials/templates/notifications.png)
