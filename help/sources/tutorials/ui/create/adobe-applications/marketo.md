---
keywords: Experience Platform;홈;인기 항목;Marketo 소스 커넥터;Marketo 커넥터;Marketo 소스;Marketo
solution: Experience Platform
title: UI에서 Marketo Engage 소스 커넥터 만들기
topic-legacy: overview
type: Tutorial
description: 이 자습서에서는 B2B 데이터를 Adobe Experience Platform으로 가져오기 위해 UI에서 Marketo Engage 소스 커넥터를 만드는 단계를 제공합니다.
exl-id: a6aa596b-9cfa-491e-86cb-bd948fb561a8
translation-type: tm+mt
source-git-commit: 5322adb4b3a244de92300e7ce9d942ad4b968454
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 0%

---

# (베타) UI에서 [!DNL Marketo Engage] 소스 커넥터를 만듭니다.

>[!IMPORTANT]
>
>[!DNL Marketo Engage] 소스는 현재 베타 상태입니다. 기능 및 설명서는 변경될 수 있습니다. 또한 베타 프로그램 중에 커넥터를 사용할 때는 비프로덕션 샌드박스를 사용해야 합니다. 샌드박스에 대한 자세한 내용은 [샌드박스 설명서](https://experienceleague.adobe.com/docs/experience-platform/sandbox/home.html?lang=en#understanding-sandboxes)를 참조하십시오.

이 자습서에서는 소비자 데이터를 Adobe Experience Platform으로 가져오기 위해 UI에서 [!DNL Marketo Engage](이하 &quot;[!DNL Marketo]&quot;) 소스 커넥터를 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

* [소스](../../../../home.md):Experience Platform을 사용하면 Platform 서비스를 사용하여 수신 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [경험 데이터 모델(XDM)](../../../../../xdm/home.md):Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [UI에서 스키마 만들기 및 편집](../../../../../xdm/ui/resources/schemas.md):UI에서 스키마를 만들고 편집하는 방법을 알아봅니다.
* [ID 네임스페이스](../../../../../identity-service/namespaces.md):ID 네임스페이스는 ID와 관련된 컨텍스트 [!DNL Identity Service] 의 지표로 사용되는 구성 요소입니다. 정규화된 ID에는 ID 값과 네임스페이스가 포함됩니다.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
* [샌드박스](../../../../../sandboxes/home.md):Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

### 필요한 자격 증명 수집

플랫폼에서 [!DNL Marketo] 계정에 액세스하려면 다음 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `munchkinId` | Munchkin ID는 특정 [!DNL Marketo] 인스턴스의 고유 식별자입니다. |
| `clientId` | [!DNL Marketo] 인스턴스의 고유 클라이언트 ID. |
| `clientSecret` | [!DNL Marketo] 인스턴스의 고유한 클라이언트 암호입니다. |

이러한 값을 가져오는 방법에 대한 자세한 내용은 [[!DNL Marketo] 인증 안내서](../../../../connectors/adobe-applications/marketo/marketo-auth.md)를 참조하십시오.

필요한 자격 증명을 수집했으면 다음 섹션의 단계를 따를 수 있습니다.

## [!DNL Marketo] 계정 연결

플랫폼 UI의 왼쪽 탐색 막대에서 **[!UICONTROL Sources]**&#x200B;을 선택하여 [!UICONTROL Sources] 작업 영역에 액세스합니다. [!UICONTROL Catalog] 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면의 왼쪽에 있는 카탈로그에서 적절한 범주를 선택할 수 있습니다. 또는 검색 막대를 사용하여 작업할 특정 소스를 찾을 수 있습니다.

[!UICONTROL Adobe applications] 범주에서 **[!UICONTROL Marketo Engage]**&#x200B;을 선택합니다. 그런 다음 **[!UICONTROL Add data]**&#x200B;을 선택하여 새 [!DNL Marketo] 데이터 흐름을 만듭니다.

![카탈로그](../../../../images/tutorials/create/marketo/catalog.png)

**[!UICONTROL Connect to Marketo Engage]** 페이지가 나타납니다. 이 페이지에서 새 계정을 사용하거나 기존 계정에 액세스할 수 있습니다.

### 새 계정

새 계정을 만드는 경우 **[!UICONTROL New account]**&#x200B;을 선택합니다. 표시되는 입력 양식에서 계정 이름, 선택적 설명 및 [!DNL Marketo] 인증 자격 증명을 입력합니다. 완료되면 **[!UICONTROL Connect to source]**&#x200B;을 선택한 다음 새 연결이 설정될 때까지 잠시 기다려 주십시오.

![신규 계정](../../../../images/tutorials/create/marketo/new.png)

### 기존 계정

기존 계정으로 데이터 흐름을 만들려면 **[!UICONTROL Existing account]**&#x200B;을 선택한 다음 사용할 [!DNL Marketo] 계정을 선택합니다. 계속하려면 **[!UICONTROL Next]**&#x200B;을 선택합니다.

![기존](../../../../images/tutorials/create/marketo/existing.png)

## 데이터 세트 선택

[!DNL Marketo] 계정을 만든 후 다음 단계에서는 [!DNL Marketo] 데이터 세트를 탐색할 수 있는 인터페이스를 제공합니다.

인터페이스의 왼쪽 절반은 디렉토리 브라우저로, 10개의 [!DNL Marketo] 데이터 세트를 표시합니다. 완벽하게 작동하는 [!DNL Marketo] 소스 연결을 사용하려면 9개의 다른 데이터 세트를 수집해야 합니다. [!DNL Marketo] 계정 기반 마케팅(ABM) 기능도 사용하는 경우 10번째 데이터 흐름을 만들어 [!UICONTROL Named Accounts] 데이터 세트를 인제스트해야 합니다.

>[!NOTE]
>
>간결성을 위해 다음 자습서에서는 [!UICONTROL Named Accounts]을 예로 사용하지만 아래 설명된 단계는 10개의 [!DNL Marketo] 데이터 세트에 적용됩니다.

먼저 인제스트할 데이터 세트를 선택한 다음 **[!UICONTROL Next]**&#x200B;을 선택합니다.

![select-data](../../../../images/tutorials/create/marketo/select-data.png)

## [!DNL Marketo] 스키마를 플랫폼에 매핑

[!UICONTROL Mapping] 단계가 나타나 [!DNL Marketo] 스키마를 플랫폼에 매핑하는 인터페이스를 제공합니다.

수집할 인바운드 데이터의 데이터 세트를 선택합니다. 기존 데이터 집합을 사용하거나 새 데이터 집합을 만들 수 있습니다.

### 기존 데이터 세트 사용

데이터를 기존 데이터 세트에 인제스트하려면 **[!UICONTROL Existing dataset]**&#x200B;을 선택한 다음 데이터 세트 아이콘을 선택합니다.

![기존 데이터 세트](../../../../images/tutorials/create/marketo/existing-dataset.png)

**[!UICONTROL Select dataset]** 대화 상자가 나타납니다. 사용할 적절한 스키마가 있는 데이터 세트를 찾아 선택한 다음 **[!UICONTROL Confirm]**&#x200B;을 선택합니다.

![select-existing-dataset](../../../../images/tutorials/create/marketo/select-dataset.png)

### 새 데이터 세트 사용

데이터를 새 데이터 세트에 인제스트하려면 **[!UICONTROL New dataset]**&#x200B;을 선택하고 제공된 필드에 데이터 세트에 대한 이름과 설명을 입력합니다.

**[!UICONTROL Select schema]** 검색 표시줄에 스키마 이름을 입력하여 스키마를 검색할 수 있습니다. 드롭다운 아이콘을 선택하여 기존 스키마 목록을 볼 수도 있습니다. 또는 **[!UICONTROL Advanced search]**&#x200B;을 선택하여 해당 세부 정보를 포함한 기존 스키마의 페이지에 액세스할 수 있습니다.

**[!UICONTROL Profile dataset]** 버튼을 토글하여 [!DNL Profile]에 대한 대상 데이터 세트를 활성화하면 엔티티의 속성 및 행동을 전체적으로 볼 수 있습니다. 모든 [!DNL Profile] 사용 가능한 데이터 집합의 데이터는 [!DNL Profile]에 포함되며 데이터 흐름을 저장할 때 변경 내용이 적용됩니다.

![새로운 데이터 세트 만들기](../../../../images/tutorials/create/marketo/new-dataset-schema.png)

스키마를 선택하고 아래로 스크롤하여 [!DNL Marketo] 데이터 집합 필드를 적절한 대상 XDM 필드에 매핑하기 시작합니다.

### 데이터 세트 소스 필드를 대상 XDM 필드에 매핑[!DNL Marketo]

각 [!DNL Marketo] 데이터 집합에는 따라야 할 고유한 매핑 규칙이 있습니다. [!DNL Marketo] 데이터 집합을 XDM에 매핑하는 방법에 대한 자세한 내용은 다음을 참조하십시오.

* [활동](../../../../connectors/adobe-applications/mapping/marketo.md#activities)
* [프로그램](../../../../connectors/adobe-applications/mapping/marketo.md#programs)
* [프로그램 멤버십](../../../../connectors/adobe-applications/mapping/marketo.md#program-memberships)
* [회사](../../../../connectors/adobe-applications/mapping/marketo.md#companies)
* [정적 목록](../../../../connectors/adobe-applications/mapping/marketo.md#static-lists)
* [정적 목록 구성원 자격](../../../../connectors/adobe-applications/mapping/marketo.md#static-list-memberships)
* [지정된 계정](../../../../connectors/adobe-applications/mapping/marketo.md#named-accounts)
* [기회](../../../../connectors/adobe-applications/mapping/marketo.md#opportunities)
* [기회 연락처 역할](../../../../connectors/adobe-applications/mapping/marketo.md#opportunity-contact-roles)
* [인물](../../../../connectors/adobe-applications/mapping/marketo.md#persons)

선택한 데이터 세트에 따라 매핑 결과를 보려면 **[!UICONTROL Preview data]**&#x200B;을 선택합니다.

![매핑](../../../../images/tutorials/create/marketo/mapping.png)

[!UICONTROL Preview] 팝업에서는 선택한 데이터 세트에서 최대 100개의 샘플 데이터 행 매핑 결과를 확인할 수 있는 인터페이스를 제공합니다.

![미리 보기](../../../../images/tutorials/create/marketo/mapping-preview.png)

소스 필드가 적절한 대상 필드에 매핑되면 **[!UICONTROL Close]**&#x200B;을 선택합니다.

## 데이터 흐름 세부 정보 제공

[!UICONTROL Dataflow detail] 단계가 나타나므로 새 데이터 플로우에 대한 이름 및 간단한 설명을 제공할 수 있습니다.

![데이터 흐름 세부 정보](../../../../images/tutorials/create/marketo/dataflow-detail.png)

API를 사용하여 다운로드할 수 있는 새로 인제스트된 배치에 대한 자세한 오류 메시지 생성을 허용하려면 **[!UICONTROL Error diagnostics]** 전환을 활성화합니다. 자세한 내용은 [데이터 통합 오류 진단](../../../../../ingestion/quality/error-diagnostics.md)에 대한 자습서를 참조하십시오.

![오류](../../../../images/tutorials/create/marketo/errors.png)

[!DNL Marketo] 커넥터는 일괄 처리를 사용하여 모든 기록 레코드를 수집하며 실시간 업데이트를 위해 스트리밍 통합 기능을 사용합니다. 이렇게 하면 잘못된 레코드를 인제스트하는 동안 커넥터에서 스트리밍을 계속할 수 있습니다. 데이터 흐름 실패를 방지하기 위해 **[!UICONTROL Partial ingestion]** 전환을 활성화한 다음 [!UICONTROL Error threshold %]을 최대로 설정합니다.

**[!UICONTROL Partial ingestion]** 특정 임계값까지 오류가 포함된 데이터를 인제스트할 수 있습니다. 자세한 내용은 [부분 일괄 처리 통합 개요](../../../../../ingestion/batch-ingestion/partial.md)를 참조하십시오.

데이터 흐름 세부 정보를 제공하고 오류 임계값을 최대값으로 설정한 후에는 **[!UICONTROL Next]**&#x200B;을 선택합니다.

![부분 섭취](../../../../images/tutorials/create/marketo/partial-ingestion.png)

## 데이터 흐름 검토

**[!UICONTROL Review]** 단계가 나타나 새 데이터 흐름을 만들기 전에 검토할 수 있습니다. 세부 사항은 다음 카테고리 내에서 그룹화됩니다.

* **[!UICONTROL Connection]**:소스 유형, 선택한 소스 엔티티의 관련 경로 및 해당 소스 엔티티 내의 열 양을 표시합니다.
* **[!UICONTROL Assign dataset & map fields]**:데이터 세트가 준수하는 스키마를 포함하여 원본 데이터를 수집할 데이터 집합을 표시합니다.

데이터 흐름을 검토했으면 **[!UICONTROL Finish]**&#x200B;을 선택하고 데이터 흐름을 만드는 데 약간의 시간이 소요됩니다.

![검토](../../../../images/tutorials/create/marketo/review.png)

## 데이터 흐름 모니터링

데이터 흐름 기능이 만들어지면 데이터 수집이 처리되는 데이터를 모니터링하여 데이터 수집률, 성공 및 오류에 대한 정보를 확인할 수 있습니다. 데이터 흐름을 모니터링하는 방법에 대한 자세한 내용은 UI](../../../../../dataflows/ui/monitor-sources.md)에서 [데이터 흐름 모니터링의 자습서를 참조하십시오.

## 특성 삭제

데이터 집합의 사용자 지정 속성은 소급하여 숨기거나 제거할 수 없습니다. 기존 데이터 세트에서 사용자 지정 특성을 숨기거나 제거하려면 이 사용자 지정 특성, 새 XDM 스키마 없이 새 데이터 세트를 만들고 새로 만드는 데이터 세트에 대해 새 데이터 흐름을 구성해야 합니다. 또한 숨기거나 제거할 사용자 지정 특성이 있는 데이터 세트로 구성된 원본 데이터 흐름을 비활성화하거나 삭제해야 합니다.

## 데이터 흐름 삭제

[!UICONTROL Dataflows] 작업 영역에서 사용할 수 있는 **[!UICONTROL Delete]** 함수를 사용하여 더 이상 필요하지 않거나 잘못 만들어진 데이터 흐름을 삭제할 수 있습니다. 데이터 흐름 삭제 방법에 대한 자세한 내용은 UI](../../delete.md)에서 데이터 흐름 삭제의 자습서를 참조하십시오.[

## 다음 단계

이 자습서를 따라 데이터 흐름을 만들어 [!DNL Marketo] 데이터를 가져왔습니다. 이제 수신 데이터를 [!DNL Real-time Customer Profile] 및 [!DNL Data Science Workspace] 등의 다운스트림 플랫폼 서비스에서 사용할 수 있습니다. 자세한 내용은 다음 문서를 참조하십시오.

* [[!DNL Real-time Customer Profile] 개요](../../../../profile/home.md)
* [[!DNL Data Science Workspace] 개요](../../../../data-science-workspace/home.md)
