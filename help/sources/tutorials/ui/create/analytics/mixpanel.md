---
title: UI에서 Mixpanel Source 연결 만들기
description: Adobe Experience Platform UI를 사용하여 Mixpanel 소스 연결을 만드는 방법을 알아봅니다.
exl-id: 2a02f6a4-08ed-468c-8052-f5b7be82d183
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 11%

---

# UI에서 [!DNL Mixpanel] 소스 연결 만들기

이 자습서에서는 Adobe Experience Platform Platform 사용자 인터페이스를 사용하여 [!DNL Mixpanel] 소스 연결을 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 다음 Experience Platform 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): [!DNL Experience Platform]에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

### 필요한 자격 증명 수집

[!DNL Mixpanel]을(를) 플랫폼에 연결하려면 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 | 예 |
| --- | --- | --- |
| 사용자 이름 | [!DNL Mixpanel] 계정에 해당하는 서비스 계정 사용자 이름입니다. 자세한 내용은 [[!DNL Mixpanel] 서비스 계정 설명서](https://developer.mixpanel.com/reference/service-accounts#authenticating-with-a-service-account)를 참조하세요. | `Test8.6d4ee7.mp-service-account` |
| 암호 | [!DNL Mixpanel] 계정에 해당하는 서비스 계정 암호입니다. | `dLlidiKHpCZtJhQDyN2RECKudMeTItX1` |
| 프로젝트 ID | [!DNL Mixpanel] 프로젝트 ID입니다. 이 ID는 소스 연결을 만드는 데 필요합니다. 자세한 내용은 [[!DNL Mixpanel] 프로젝트 설정 설명서](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) 및 프로젝트 만들기 및 관리에 대한 [[!DNL Mixpanel] 안내서](https://help.mixpanel.com/hc/en-us/articles/115004505106-Create-and-Manage-Projects)를 참조하십시오. | `2384945` |
| 시간대 | [!DNL Mixpanel] 프로젝트에 해당하는 시간대입니다. 소스 연결을 만들려면 시간대가 필요합니다. 자세한 내용은 [Mixpanel 프로젝트 설정 설명서](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings)를 참조하세요. | `Pacific Standard Time` |

[!DNL Mixpanel] 원본 인증에 대한 자세한 내용은 [[!DNL Mixpanel] 원본 개요](../../../../connectors/analytics/mixpanel.md)를 참조하세요.

## [!DNL Mixpanel] 계정 연결

Platform UI의 왼쪽 탐색 막대에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 [!UICONTROL 소스] 작업 영역에 액세스합니다. [!UICONTROL 카탈로그] 화면에 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

*Analytics* 범주에서 [!DNL Mixpanel]을(를) 선택한 다음 **[!UICONTROL 데이터 추가]**&#x200B;를 선택합니다.

![카탈로그](../../../../images/tutorials/create/mixpanel-export-events/catalog.png)

**[!UICONTROL Mixpanel 계정 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정을 사용하려면 새 데이터 흐름을 만들 [!DNL Mixpanel] 계정을 선택한 다음 **[!UICONTROL 다음]**&#x200B;을 선택하여 계속합니다.

![기존](../../../../images/tutorials/create/mixpanel-export-events/existing.png)

### 새 계정

새 계정을 만드는 경우 **[!UICONTROL 새 계정]**&#x200B;을(를) 선택한 다음 이름, 설명(선택 사항) 및 자격 증명을 제공합니다. 완료되면 **[!UICONTROL 소스에 연결]**&#x200B;을 선택한 다음 새 연결을 설정할 수 있는 시간을 허용하세요.

![새로 만들기](../../../../images/tutorials/create/mixpanel-export-events/new.png)

## 프로젝트 ID 및 시간대 선택 {#project-id-and-timezone}

>[!CONTEXTUALHELP]
>id="platform_sources_mixpanel_timezone"
>title="Mixpanel 수집 시간대 설정"
>abstract="플랫폼은 지정된 프로젝트 시간대를 사용하여 Mixpanel에서 관련 데이터를 수집하므로 시간대는 Mixpanel 프로필 시간대 설정과 같아야 합니다. 이벤트가 Mixpanel 데이터 저장소에 기록되기 전에 Mixpanel은 프로젝트 시간대에 맞게 시간대를 조정합니다."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/analytics/mixpanel.html?lang=ko#project-id-and-timezone" text="설명서에서 자세히 알아보기"

소스가 인증되면 프로젝트 ID와 시간대를 제공한 다음 **[!UICONTROL 선택]**&#x200B;을 선택합니다.

[!DNL Mixpanel] 데이터를 플랫폼으로 수집하기 전에 지정한 시간대는 [!DNL Mixpanel] 프로필 시간대 설정과 같아야 합니다. 데이터의 시간대에 대한 모든 변경 사항은 새 이벤트에만 적용되고 이전 이벤트는 이전에 지정한 시간대에 유지됩니다. [!DNL Mixpanel]은(는) 일광 절약 시간제를 수용하며 수집 타임스탬프를 적절하게 조정합니다. 시간대가 데이터에 미치는 영향에 대한 자세한 내용은 [프로젝트에 대한 시간대 관리](https://help.mixpanel.com/hc/en-us/articles/115004547203-Manage-Timezones-for-Projects-in-Mixpanel)에 대한 [!DNL Mixpanel] 가이드를 참조하십시오.

잠시 후 올바른 인터페이스가 미리보기 패널로 업데이트되어 데이터 흐름을 생성하기 전에 스키마를 검사할 수 있습니다. 완료되면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

![구성](../../../../images/tutorials/create/mixpanel-export-events/authentication-configuration.png)

## 다음 단계

이 자습서에 따라 [!DNL Mixpanel] 계정에 대한 연결을 설정했습니다. 이제 다음 자습서를 계속 진행하고 [분석 데이터를 플랫폼으로 가져오도록 데이터 흐름을 구성](../../dataflow/analytics.md)할 수 있습니다.

## 추가 리소스 {#additional-resources}

아래 섹션에서는 [!DNL Mixpanel] 소스를 사용할 때 참조할 수 있는 추가 리소스를 제공합니다.

### 유효성 검사 {#validation}

다음은 [!DNL Mixpanel] 원본과 [!DNL Mixpanel] 이벤트가 플랫폼에 수집되고 있는지 확인하기 위해 수행할 수 있는 단계입니다.

Platform UI의 왼쪽 탐색 막대에서 **[!UICONTROL 데이터 세트]**&#x200B;를 선택하여 [!UICONTROL 데이터 세트] 작업 영역에 액세스합니다. [!UICONTROL 데이터 집합 활동] 화면에 실행 세부 정보가 표시됩니다.

![dataset-activity](../../../../images/tutorials/create/mixpanel-export-events/dataset-activity.png)

그런 다음 보려는 데이터 흐름의 데이터 흐름 실행 ID를 선택하여 해당 데이터 흐름 실행에 대한 특정 세부 정보를 확인합니다.

![데이터 흐름 모니터링](../../../../images/tutorials/create/mixpanel-export-events/dataflow-monitoring.png)

마지막으로 **[!UICONTROL 데이터 집합 미리 보기]**&#x200B;를 선택하여 수집된 데이터를 표시합니다.

![미리 보기-데이터 세트](../../../../images/tutorials/create/mixpanel-export-events/preview-dataset.png)

[!DNL Mixpanel] > [!DNL Events] 페이지의 데이터에 대해 이 데이터를 확인할 수 있습니다. 자세한 내용은 [[!DNL Mixpanel] 이벤트에 대한 문서](https://help.mixpanel.com/hc/en-us/articles/4402837164948-Events-formerly-Live-View-)를 참조하세요.

![mixpanel-events](../../../../images/tutorials/create/mixpanel-export-events/mixpanel-events.png)

### Mixpanel 스키마

아래 표는 [!DNL Mixpanel]에 대해 설정해야 하는 지원되는 매핑을 보여 줍니다.

>[!TIP]
>
>API에 대한 자세한 내용은 [이벤트 내보내기 API > 다운로드](https://developer.mixpanel.com/reference/raw-event-export)를 참조하십시오.


| 소스 | 유형 |
|---|---|
| `distinct_id` | 문자열 |
| `event_name` | 문자열 |
| `import` | 부울 |
| `insert_id` | 문자열 |
| `item_id` | 문자열 |
| `item_name` | 문자열 |
| `item_price` | 문자열 |
| `mp_api_endpoint` | 문자열 |
| `mp_api_timestamp_ms` | 정수 |
| `mp_processing_time_ms` | 정수 |
| `time` | 정수 |

### 제한 {#limits}

* [API 속도 제한 내보내기](https://help.mixpanel.com/hc/en-us/articles/115004602563-Rate-Limits-for-API-Endpoints)에 표시된 대로 시간당 최대 100개의 동시 쿼리와 60개의 쿼리가 있습니다.
