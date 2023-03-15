---
keywords: Experience Platform;홈;인기 항목;소스;커넥터;소스 커넥터;소스 sdk;sdk;SDK
title: (베타 ) UI에서 Mixpanel 소스 연결 만들기
description: Adobe Experience Platform UI를 사용하여 Mixpanel 소스 연결을 만드는 방법을 알아봅니다.
exl-id: 2a02f6a4-08ed-468c-8052-f5b7be82d183
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 3%

---

# (Beta) [!DNL Mixpanel] UI의 소스 연결

>[!NOTE]
>
>다음 [!DNL Mixpanel] 소스는 베타 버전입니다. 다음을 참조하십시오. [소스 개요](../../../../home.md#terms-and-conditions) beta 레이블 소스를 사용하는 방법에 대한 자세한 내용.

이 자습서에서는 다음을 만드는 단계를 제공합니다 [!DNL Mixpanel] Adobe Experience Platform Platform 사용자 인터페이스를 사용한 소스 연결.

## 시작하기

이 자습서에서는 다음 Experience Platform 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): 표준화된 프레임워크 [!DNL Experience Platform] 고객 경험 데이터를 구성합니다.
   * [스키마 컴포지션 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 정의 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 소스의 집계 데이터를 기반으로 통합 실시간 소비자 프로필을 제공합니다.

### 필요한 자격 증명 수집

연결하려면 [!DNL Mixpanel] 플랫폼에 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 | 예 |
| --- | --- | --- |
| 사용자 이름 | 에 해당하는 서비스 계정 사용자 이름 [!DNL Mixpanel] 계정입니다. 다음을 참조하십시오. [[!DNL Mixpanel] 서비스 계정 설명서](https://developer.mixpanel.com/reference/service-accounts#authenticating-with-a-service-account) 추가 정보. | `Test8.6d4ee7.mp-service-account` |
| 암호 | 에 해당하는 서비스 계정 암호 [!DNL Mixpanel] 계정입니다. | `dLlidiKHpCZtJhQDyN2RECKudMeTItX1` |
| 프로젝트 ID | 사용자 [!DNL Mixpanel] 프로젝트 ID. 이 ID는 소스 연결을 만드는 데 필요합니다. 다음을 참조하십시오. [[!DNL Mixpanel] 프로젝트 설정 설명서](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) 및 [[!DNL Mixpanel] 프로젝트 만들기 및 관리에 대한 안내서](https://help.mixpanel.com/hc/en-us/articles/115004505106-Create-and-Manage-Projects) 추가 정보. | `2384945` |
| 표준 시간대 | 에 해당하는 시간대 [!DNL Mixpanel] 프로젝트. 소스 연결을 만들려면 시간대가 필요합니다. 다음을 참조하십시오. [Mixpanel 프로젝트 설정 설명서](https://help.mixpanel.com/hc/en-us/articles/115004490503-Project-Settings) 추가 정보. | `Pacific Standard Time` |

인증에 대한 자세한 내용 [!DNL Mixpanel] source, 다음 참조: [[!DNL Mixpanel] 소스 개요](../../../../connectors/analytics/mixpanel.md).

## 연결 [!DNL Mixpanel] account

Platform UI에서 를 선택합니다. **[!UICONTROL 소스]** 왼쪽 탐색 모음에서 다음 위치에 액세스: [!UICONTROL 소스] 작업 영역. 다음 [!UICONTROL 카탈로그] 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래 *분석* 범주, 선택 [!DNL Mixpanel]을 선택한 다음 을 선택합니다 **[!UICONTROL 데이터 추가]**.

![카탈로그](../../../../images/tutorials/create/mixpanel-export-events/catalog.png)

다음 **[!UICONTROL Mixpanel 계정 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정을 사용하려면 [!DNL Mixpanel] 새 데이터 흐름을 만들 계정 을 선택합니다. **[!UICONTROL 다음]** 계속합니다.

![기존](../../../../images/tutorials/create/mixpanel-export-events/existing.png)

### 새 계정

새 계정을 만드는 경우 다음을 선택합니다 **[!UICONTROL 새 계정]**&#x200B;을 누르고 이름, 설명(선택 사항) 및 자격 증명을 제공합니다. 완료되면 다음을 선택합니다. **[!UICONTROL 소스에 연결]** 그런 다음 새 연결을 설정하는 데 시간이 걸릴 수 있습니다.

![신규](../../../../images/tutorials/create/mixpanel-export-events/new.png)

## 프로젝트 ID 및 시간대 선택 {#project-id-and-timezone}

>[!CONTEXTUALHELP]
>id="platform_sources_mixpanel_timezone"
>title="Mixpanel 수집에 대한 시간대 설정"
>abstract="Platform은 지정된 프로젝트 시간대를 사용하여 Mixpanel에서 관련 데이터를 수집하므로 시간대는 Mixpanel 프로필 시간대 설정과 같아야 합니다. Mixpanel은 이벤트를 Mixpanel 데이터 저장소에 기록하기 전에 프로젝트 시간대와 조정되도록 시간대를 조정합니다."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/sources/ui-tutorials/create/analytics/mixpanel.html?lang=en#project-id-and-timezone" text="설명서에서 자세히 알아보기"

소스가 인증되면 프로젝트 ID와 시간대를 제공한 다음 을 선택합니다. **[!UICONTROL 선택]**.

수집하기 전에 지정하는 시간대 [!DNL Mixpanel] 플랫폼에 대한 데이터는 와(과) 동일해야 합니다. [!DNL Mixpanel] 프로필 시간대 설정입니다. 데이터의 시간대에 대한 모든 변경 사항은 새 이벤트에만 적용되고 이전 이벤트는 이전에 지정한 시간대에 유지됩니다. [!DNL Mixpanel] 일광 절약 시간제를 수용하고 수집 타임스탬프를 적절하게 조정합니다. 시간대가 데이터에 미치는 영향에 대한 자세한 내용은 [!DNL Mixpanel] 다음에 대한 안내서: [프로젝트의 시간대 관리](https://help.mixpanel.com/hc/en-us/articles/115004547203-Manage-Timezones-for-Projects-in-Mixpanel).

잠시 후 올바른 인터페이스가 미리보기 패널로 업데이트되어 데이터 흐름을 생성하기 전에 스키마를 검사할 수 있습니다. 완료되면 다음을 선택합니다. **[!UICONTROL 다음]**.

![구성](../../../../images/tutorials/create/mixpanel-export-events/authentication-configuration.png)

## 다음 단계

이 자습서를 따라 [!DNL Mixpanel] 계정입니다. 이제 다음 튜토리얼을 계속 진행하여 [analytics 데이터를 Platform으로 가져오도록 데이터 흐름 구성](../../dataflow/analytics.md).

## 추가 리소스 {#additional-resources}

아래 섹션에서는 사용 시 참조할 수 있는 추가 리소스를 제공합니다. [!DNL Mixpanel] 소스.

### 유효성 검사 {#validation}

다음은 을(를) 성공적으로 연결했는지 확인하기 위해 수행할 수 있는 단계입니다. [!DNL Mixpanel] 소스 및 해당 [!DNL Mixpanel] 이벤트가 Platform에 수집되고 있습니다.

Platform UI에서 를 선택합니다. **[!UICONTROL 데이터 세트]** 왼쪽 탐색 모음에서 다음 위치에 액세스: [!UICONTROL 데이터 세트] 작업 영역. 다음 [!UICONTROL 데이터 세트 활동] 화면에 실행 세부 정보가 표시됩니다.

![dataset-activity](../../../../images/tutorials/create/mixpanel-export-events/dataset-activity.png)

그런 다음 보려는 데이터 흐름의 데이터 흐름 실행 ID를 선택하여 해당 데이터 흐름 실행에 대한 특정 세부 정보를 확인합니다.

![데이터 흐름 모니터링](../../../../images/tutorials/create/mixpanel-export-events/dataflow-monitoring.png)

마지막으로 다음을 선택합니다. **[!UICONTROL 데이터 세트 미리 보기]** 수집된 데이터를 표시합니다.

![preview-dataset](../../../../images/tutorials/create/mixpanel-export-events/preview-dataset.png)

의 데이터에 대해 이 데이터를 확인할 수 있습니다. [!DNL Mixpanel] > [!DNL Events] 페이지를 가리키도록 업데이트하는 중입니다. 다음을 참조하십시오. [[!DNL Mixpanel] 이벤트에 대한 문서](https://help.mixpanel.com/hc/en-us/articles/4402837164948-Events-formerly-Live-View-) 추가 정보.

![mixpanel-events](../../../../images/tutorials/create/mixpanel-export-events/mixpanel-events.png)

### Mixpanel 스키마

아래 표에는 설정해야 하는 지원되는 매핑이 나와 있습니다. [!DNL Mixpanel].

>[!TIP]
>
>다음을 참조하십시오 [Event Export API > 다운로드](https://developer.mixpanel.com/reference/raw-event-export) 를 참조하십시오.


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

* 에 표시된 대로 시간당 최대 100개의 동시 쿼리와 60개의 쿼리가 있습니다. [API 속도 제한 내보내기](https://help.mixpanel.com/hc/en-us/articles/115004602563-Rate-Limits-for-API-Endpoints).
