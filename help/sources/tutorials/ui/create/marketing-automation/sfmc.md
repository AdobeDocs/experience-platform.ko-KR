---
title: UI를 통해 Salesforce Marketing Cloud(V2) 계정을 Experience Platform에 연결합니다
description: UI를 통해 Salesforce Marketing Cloud(V2) 계정을 Experience Platform에 연결하는 방법을 알아봅니다.
source-git-commit: 91bf8bf6e6f7030574d693484ce9797800c2d5dd
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 1%

---

# Experience Platform에 [!DNL Salesforce Marketing Cloud] 연결

Experience Platform 사용자 인터페이스의 소스 작업 영역을 사용하여 [!DNL Salesforce Marketing Cloud] 계정을 Adobe Experience Platform에 연결하는 방법에 대해 알아보려면 이 안내서를 참조하십시오.

## 시작하기

이 자습서에서는 Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): [!DNL Experience Platform]에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

### 필요한 자격 증명 수집

인증에 대한 자세한 내용은 [[!DNL Salesforce Marketing Cloud] 개요](../../../../connectors/marketing-automation/sfmc.md#prerequisites)를 읽어 보십시오.

## 소스 카탈로그 탐색

Experience Platform UI의 왼쪽 탐색에서 **[!UICONTROL Sources]**&#x200B;을(를) 선택하여 *[!UICONTROL Sources]* 작업 영역에 액세스합니다. 카테고리를 선택하거나 검색 창을 사용하여 소스를 찾습니다.

[!DNL Salesforce Marketing Cloud]에 연결하려면 *[!UICONTROL Marketing Automation]* 범주로 이동하여 **[!UICONTROL (V2) Salesforce Marketing Cloud]** 원본 카드를 선택한 다음 **[!UICONTROL Set up]**&#x200B;을(를) 선택하십시오.

>[!TIP]
>
>지정된 소스에 아직 인증된 계정이 없는 경우 소스 카탈로그의 소스에 **[!UICONTROL Set up]** 옵션이 표시됩니다. 인증된 계정이 만들어지면 이 옵션이 **[!UICONTROL Add data]**(으)로 변경됩니다.

![Salesforce Marketing Cloud 소스가 있는 소스 카탈로그를 선택했습니다.](../../../../images/tutorials/create/sfmc/catalog.png)

## 기존 계정 사용 {#existing}

기존 계정을 사용하려면 **[!UICONTROL Existing account]**&#x200B;을(를) 선택한 다음 사용할 [!DNL Salesforce Marketing Cloud] 계정을 선택하십시오.

![원본 워크플로의 기존 계정 인터페이스](../../../../images/tutorials/create/sfmc/existing.png)

## 새 계정 만들기 {#new}

새 계정을 만들려면 **[!UICONTROL New account]**&#x200B;을(를) 선택하고 [!UICONTROL Source connection details] 아래에 이름과 설명을 입력하십시오. 그런 다음 [!UICONTROL Account authentication]에서 **클라이언트 ID**, **클라이언트 암호** 및 **기본 끝점**&#x200B;에 대한 값을 제공합니다. 자격 증명에 대한 자세한 내용은 [인증 가이드](../../../../connectors/marketing-automation/sfmc.md#gather-required-credentials)를 참조하십시오. 완료되면 **[!UICONTROL Connect to source]**&#x200B;을(를) 선택하고 몇 초 동안 연결을 설정하십시오.

![원본 워크플로의 새 계정 인터페이스입니다.](../../../../images/tutorials/create/sfmc/new.png)

## 데이터 선택

[!DNL Salesforce Marketing Cloud] 원본은 [!DNL Salesforce Marketing Cloud] 데이터 확장에서만 데이터 수집을 지원합니다.

[!UICONTROL Select data] 인터페이스를 사용하여 [!DNL Salesforce Marketing Cloud] 인스턴스에서 수집할 데이터 확장을 선택합니다. 데이터 확장을 선택하면 계속하기 전에 미리 보기 패널을 사용하여 데이터 세트에 예상 필드가 포함되어 있는지 확인할 수 있습니다.

![원본 워크플로의 데이터 선택 단계](../../../../images/tutorials/create/sfmc/select-data.png)

## 데이터 세트 및 데이터 흐름 세부 정보

그런 다음 데이터 세트 및 데이터 흐름에 대한 정보를 제공해야 합니다. 이 단계에서는 기존 데이터 세트를 사용하거나 새 데이터 세트를 만들 수 있습니다. 또한 이 단계 중에 실시간 고객 프로필에 수집하기 위한 데이터 세트를 선택적으로 활성화할 수 있습니다.

![원본 워크플로의 데이터 집합 및 데이터 흐름 세부 정보 단계입니다.](../../../../images/tutorials/create/sfmc/dataset-details.png)

## 매핑

[!DNL Salesforce Marketing Cloud]에서 데이터 확장은 표준 개체로 간주되지 않습니다. 따라서 Experience Platform 스키마에 사전 정의되거나 고정된 매핑 필드가 없습니다. Experience Platform의 데이터 준비는 [!DNL Salesforce Marketing Cloud]의 소스 필드와 대상 XDM(Experience Data Model) 스키마 간에 최적의 정렬을 수행하지만 매핑되지 않았거나 잘못된 필드를 해결하기 위해 수동으로 검토하거나 조정해야 하는 경우가 있을 수 있습니다.

![원본 워크플로의 매핑 단계입니다.](../../../../images/tutorials/create/sfmc/mapping.png)

## 데이터 흐름 예약

이제 매핑이 완료되면 데이터 흐름에 대한 수집 일정을 구성할 수 있습니다. [!UICONTROL Frequency]을(를) `Once`(으)로 설정하여 일회성 수집 실행을 구성합니다. 증분 수집의 경우 [!UICONTROL Frequency]을(를) `Hour`, `Day` 또는 `Week`(으)로 설정할 수 있습니다. 증분 수집을 사용할 때는 수집 실행 사이에 발생하는 시간을 정의하도록 [!UICONTROL Interval]을(를) 구성해야 합니다. 예를 들어 수집 빈도를 `Day`(으)로 설정하고 간격을 `15`(으)로 설정하면 데이터 흐름이 15일마다 데이터를 수집하도록 예약됩니다.

>[!TIP]
>
> [!DNL Salesforce Marketing Cloud] 원본에는 분당 수집 빈도를 사용할 수 없습니다. 선택할 수 있는 가장 빈번한 일정은 시간별입니다. 데이터 새로 고침 요구 사항과 일치하는 일정을 선택하십시오. 더 자주 일정을 선택하면 컴퓨팅 비용이 증가한다는 점을 명심하십시오.

증분 동기화를 사용하려면 데이터 세트에서 델타(날짜/시간) 필드를 선택해야 합니다. 데이터 세트에 적절한 델타 필드가 포함되어 있지 않으면 데이터 흐름을 만들 수 없습니다.

![원본 워크플로의 예약 단계입니다.](../../../../images/tutorials/create/sfmc/schedule.png)

## 검토

수집 일정을 구성한 상태에서 [!UICONTROL Review] 인터페이스를 사용하여 데이터 흐름의 세부 정보를 확인합니다. **[!UICONTROL Finish]**&#x200B;을(를) 선택하여 설정을 완료하고 데이터 흐름을 시작할 수 있도록 잠시 기다려 주십시오.

![원본 워크플로의 검토 단계입니다.](../../../../images/tutorials/create/sfmc/review.png)

## 모니터

데이터 흐름을 선택하면 지정된 일정에 따라 데이터의 일회성 채우기 및 후속 증분 동기화가 수행됩니다. 데이터 흐름으로 이동하여 동기화 상태를 모니터링할 수 있습니다. 자세한 내용은 [UI에서 원본 데이터 흐름 모니터링](../../../../../dataflows/ui/monitor-sources.md)에 대한 안내서를 참조하십시오.

## 다음 단계

이 자습서에서는 사용자 인터페이스를 사용하여 [!DNL Salesforce Marketing Cloud]&#x200B;(V2) 계정을 Experience Platform에 연결하는 방법을 안내했습니다. 소스 계정을 선택 또는 만들고, 필요한 자격 증명을 제공하고, 수집할 데이터 확장을 선택하고, 데이터 세트 및 데이터 흐름 세부 정보를 지정하고, 데이터를 매핑하고, 데이터 수집을 위한 일정을 설정하고, 데이터 흐름을 모니터링하는 방법을 배웠습니다. 이러한 단계를 따라 활성화 및 분석을 위해 [!DNL Salesforce Marketing Cloud] 데이터를 Experience Platform과 통합했습니다.

자세한 내용은 다음 설명서를 참조하십시오.

* [소스 개요](../../../../home.md)
* [Real-Time CDP B2B Edition](../../../../../rtcdp/b2b-overview.md)

