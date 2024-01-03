---
title: ID 서비스에서 삭제
description: 이 문서에서는 Experience Platform에서 ID 데이터를 삭제하는 데 사용할 수 있는 다양한 메커니즘에 대한 개요를 제공하고 ID 그래프가 영향을 받는 방법에 대한 명확한 설명을 제공합니다.
exl-id: 0619d845-71c1-4699-82aa-c6436815d5b3
source-git-commit: 44e4e83d80302f64854f6c8f9531da913a2f0942
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 1%

---

# ID 서비스에서 삭제

Adobe Experience Platform Identity Service는 개별 사용자에 대해 장치 및 시스템 간에 ID를 결정적으로 연결하여 ID 그래프를 생성합니다. ID 그래프 연결은 표시된 두 개 이상의 ID가 동일한 데이터 행 내에서 수신될 때 설정됩니다.

ID 그래프는 실시간 고객 프로필에서 고객 속성 및 행동에 대한 포괄적이고 단일 보기를 만드는 데 활용되므로 디바이스가 아닌 사람에게 효과적인 개인 디지털 경험을 실시간으로 제공할 수 있습니다.

이 문서에서는 Experience Platform에서 ID 데이터를 삭제하는 데 사용할 수 있는 다양한 메커니즘에 대한 개요를 제공하고 ID 그래프가 영향을 받는 방법에 대한 명확한 설명을 제공합니다.

## 시작하기

아래 문서에서는 Experience Platform의 다음 기능을 참조합니다.

* [ID 서비스](home.md): 디바이스와 시스템 간에 ID를 연결하여 개별 고객과 고객의 행동을 더 잘 파악할 수 있습니다.
   * [ID 그래프](./ui/identity-graph-viewer.md): ID 그래프는 특정 고객에 대한 서로 다른 ID 간의 관계 맵으로, 고객이 다양한 채널에서 브랜드와 상호 작용하는 방식을 시각적으로 보여 줍니다.
   * [ID 네임스페이스](namespaces.md): ID 네임스페이스는 ID가 연관되는 컨텍스트의 지표 역할을 하는 ID 서비스의 구성 요소입니다. 예를 들어, &quot;name&quot;의 값을 구별합니다<span>@email.com&quot; 을 이메일 주소로 사용하거나 &quot;443522&quot;를 숫자 CRM ID로 사용합니다.
* [카탈로그 서비스](../catalog/home.md): 데이터 레이크 내에서 데이터 계보, 메타데이터, 파일 설명, 디렉터리 및 데이터 세트를 탐색합니다.
* [데이터 위생](../hygiene/home.md): 자동화된 데이터 세트 만료를 예약하거나 하나의 데이터 세트 또는 모든 데이터 세트에서 개별 레코드를 삭제하여 저장된 소비자 데이터를 관리합니다.
* [Adobe Experience Platform Privacy Service](../privacy-service/home.md): Adobe Experience Cloud 애플리케이션 전반에서 개인 데이터에 액세스하거나, 판매를 거부하거나, 삭제하기 위한 고객 요청을 관리합니다.
* [실시간 고객 프로필](../profile/home.md): 여러 소스에서 집계한 데이터를 기반으로 통합 고객 프로필을 실시간으로 제공합니다.

## 단일 ID 삭제

단일 ID 삭제 요청을 사용하면 그래프 내의 ID를 삭제할 수 있으므로 ID 네임스페이스와 연결된 단일 사용자 ID에 연결된 링크가 제거됩니다. 다음에서 제공하는 메커니즘을 사용할 수 있습니다. [Privacy Service](../privacy-service/home.md) 데이터 삭제 요청 및 GDPR(일반 데이터 보호 규정)과 같은 개인 정보 보호 규정 준수와 같은 사용 사례입니다.

아래 섹션에서는 Experience Platform에서 단일 ID 삭제 요청에 사용할 수 있는 메커니즘에 대해 간략히 설명합니다.

### Privacy Service에서 단일 ID 삭제

Privacy Service은 일반 데이터 보호 규정(GDPR) 및 캘리포니아 소비자 개인정보 보호법(CCPA)과 같은 개인정보 보호 규정에 따라 설명된 대로 개인 데이터에 액세스하거나, 판매를 거부하거나, 삭제하도록 고객 요청을 처리합니다. Privacy Service을 사용하면 API 또는 UI를 사용하여 작업 요청을 제출할 수 있습니다. Experience Platform이 Privacy Service에서 삭제 요청을 수신하면 플랫폼은 요청이 수신되었고 영향을 받는 데이터가 삭제 표시되었음을 Privacy Service에게 확인합니다. 개별 ID의 삭제는 제공된 네임스페이스 및/또는 ID 값을 기반으로 합니다. 또한 해당 조직과 연관된 모든 샌드박스에 대해 삭제가 수행됩니다. 자세한 내용은 의 안내서를 참조하십시오. [identity 서비스에서 개인 정보 보호 요청 처리](privacy.md).

아래 표는 Privacy Service 의 단일 ID 삭제 분류를 제공합니다.

| 단일 ID 삭제 | Privacy Service |
| --- | --- |
| 수락된 사용 사례 | 데이터 개인 정보 보호 요청(GDPR, CCPA)만 해당. |
| 예상 대기 시간 | 일 ~ 주 |
| 영향을 받는 서비스 | Privacy Service에서 단일 ID 삭제를 사용하면 ID 서비스에서 데이터를 삭제할지, 실시간 고객 프로필에서 삭제할지 또는 데이터 레이크에서 삭제할지 선택할 수 있습니다. |
| 삭제 패턴 | ID 서비스에서 ID를 삭제합니다. |

{style="table-layout:auto"}

## 데이터 세트 삭제

다음 섹션에서는 Experience Platform에서 데이터 세트 및 관련 ID 링크를 삭제하는 데 사용할 수 있는 메커니즘에 대해 설명합니다.

### 카탈로그 서비스의 데이터 세트 삭제

카탈로그 서비스를 사용하여 데이터 세트 삭제 요청을 제출할 수 있습니다. 카탈로그 서비스를 사용하여 데이터 세트를 삭제하는 방법에 대한 자세한 내용은 [카탈로그 서비스 API를 사용하여 오브젝트 삭제](../catalog/api/delete-object.md). 또는 Platform UI를 사용하여 데이터 세트 삭제에 대한 요청을 제출할 수 있습니다. 자세한 내용은 [데이터 세트 사용 안내서](../catalog/datasets/user-guide.md#delete-a-dataset).

### 데이터 위생 상태의 데이터 세트 만료

다음 [[!UICONTROL 데이터 위생] 작업 영역](../hygiene/ui/overview.md) Adobe Experience Platform UI에서 데이터 세트에 대한 만료를 예약할 수 있습니다. 데이터 세트가 만료 날짜에 도달하면 데이터 레이크, ID 서비스 및 실시간 고객 프로필은 각 서비스에서 데이터 세트의 콘텐츠를 제거하는 별도의 프로세스를 시작합니다. 자세한 내용은 의 안내서를 참조하십시오. [를 사용하여 데이터 세트 만료 관리 [!UICONTROL 데이터 위생] 작업 영역](../hygiene/ui/dataset-expiration.md).

아래 표는 카탈로그 서비스의 데이터 세트 삭제와 데이터 위생 사이의 차이점에 대한 분석을 제공합니다.

| 데이터 세트 삭제 | 카탈로그 서비스 | 데이터 위생 |
| --- | --- | --- |
| 수락된 사용 사례 | Platform에서 전체 데이터 세트 및 관련 ID 정보를 삭제합니다. | Experience Platform에 저장된 데이터의 관리. |
| 예상 대기 시간 | 일 | 일 |
| 영향을 받는 서비스 | 카탈로그 서비스를 통해 데이터 세트를 삭제하면 ID 서비스, 실시간 고객 프로필 및 데이터 레이크에서 데이터가 삭제됩니다. | 데이터 위생 관리를 통해 데이터 세트를 삭제하면 ID 서비스, 실시간 고객 프로필 및 데이터 레이크에서 데이터가 삭제됩니다. |
| 삭제 패턴 | 특정 데이터 세트에 의해 설정된 ID 서비스에서 연결된 ID를 삭제합니다. | 만료 일정에 따라 특정 데이터 세트에 의해 설정된 ID 서비스에서 연결된 ID를 삭제합니다. |

{style="table-layout:auto"}

## 삭제 후 ID 그래프의 다른 상태

모든 ID 그래프 삭제는 삭제 요청에서 지정한 대로 둘 이상의 ID 간 연결을 제거합니다. 데이터 세트 삭제 요청의 경우 지정된 데이터 세트에 의해 설정된 모든 ID 링크가 제거되며 그래프에서 ID가 제거되거나 제거되지 않을 수 있습니다. 단일 ID 삭제 요청의 경우 지정된 ID에 대한 ID 링크가 제거되므로 ID 값 자체가 모든 ID 그래프에서 제거됩니다. 다른 ID에 대한 단일 연결이 없는 ID는 ID 서비스에 저장되지 않습니다.

다음은 삭제 작업이 ID 그래프의 상태에 미칠 수 있는 잠재적 영향에 대한 개요입니다.

| ID 그래프 상태 | 설명 |
| --- | --- |
| 부분 업데이트 | 삭제 요청이 성공적으로 처리된 후 그래프 내에 두 개 이상의 ID가 연결된 상태로 유지되면 그래프의 부분 업데이트가 발생합니다. 삭제 후에도 나머지 ID 링크는 서로 연결된 상태로 유지되거나, 삭제된 ID에 따라 두 개 이상의 그래프로 분리될 수 있습니다. |
| 전체 제거 | 그래프가 존재하려면 적어도 두 개의 연결된 ID가 있어야 합니다. 따라서 삭제 요청으로 인해 그래프 내의 모든 기존 링크가 제거되면 그래프가 완전히 제거됩니다. |
| 변경 내용 없음 | 특정 삭제 요청에 그래프의 어떤 멤버와도 연결되어 있지 않은 ID 또는 데이터 세트가 포함된 경우 그래프는 영향을 받지 않습니다. 또한 링크가 삭제되지 않은 다른 링크에 의해 설정된 경우 삭제 요청으로 데이터 세트 또는 ID-데이터 세트 조합 간의 링크가 제거되더라도 그래프가 업데이트되지 않습니다. 즉, 링크가 두 개의 다른 데이터 세트에 있는 경우 데이터 세트 중 하나만 제거되므로 그래프가 업데이트되지 않습니다. |

{style="table-layout:auto"}

## 다음 단계

이 문서에서는 Experience Platform에서 ID 및 데이터 세트를 삭제하는 데 사용할 수 있는 다양한 메커니즘에 대해 설명합니다. 이 문서에서는 ID 및 데이터 세트 삭제가 ID 그래프에 미치는 영향에 대해서도 간략히 설명했습니다. ID 서비스에 대한 자세한 내용은 [ID 서비스 개요](home.md).

<!--

You can use [Data hygiene](../hygiene/home.md) for data cleansing, removing anonymous data, or data minimization for the data that you have collected.

### Single identity deletion in the [!UICONTROL Data Hygiene] workspace

The [[!UICONTROL Data Hygiene] workspace](../hygiene/ui/overview.md) in the Platform UI allows you to delete consumer records that are participating in Identity Service and Real-Time Customer Profile. For a comprehensive guide on using the [!UICONTROL Data Hygiene] workspace, see the tutorial on [deleting consumer records](../hygiene/ui/record-delete.md).

The table below provides a breakdown of differences between single identity deletion in Privacy Service and Data hygiene:

| Single identity deletion | Privacy Service | Data hygiene |
| --- | --- | --- |
| Accepted use cases | Data privacy requests (GDPR, CCPA) only. | Management of data stored in Experience Platform. |
| Estimated latency | Days to weeks | Days |
| Services impacted | Single identity deletion in Privacy Service allows you to select whether data will be deleted from Identity Service, Real-Time Customer Profile, or data lake. | Single identity deletion in Data hygiene deletes the selected data across Identity Service, Real-Time Customer Profile, and data lake. |
| Deletion patterns | Delete an identity from Identity Service. | Delete an identity from Identity Service. |

-->
