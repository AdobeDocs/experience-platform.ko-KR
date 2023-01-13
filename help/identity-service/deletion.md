---
title: Identity 서비스에서 삭제
description: 이 문서에서는 Experience Platform에서 ID 데이터를 삭제하고 ID 그래프가 어떤 영향을 받을 수 있는지에 대한 명확한 설명을 제공하는 데 사용할 수 있는 다양한 메커니즘에 대한 개요를 제공합니다.
source-git-commit: da1ce4560d28d43db47318883f9656cebb2eb487
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 1%

---

# Identity 서비스에서 삭제

Adobe Experience Platform Identity 서비스는 개별 사용자에 대해 장치 및 시스템 간에 ID를 결정적으로 연결하여 ID 그래프를 생성합니다. ID 그래프 링크는 동일한 데이터 행 내에서 두 개 이상의 표시된 ID를 받으면 설정됩니다.

실시간 고객 프로필에서 ID 그래프를 활용하여 고객 속성 및 행동에 대한 포괄적이고 단일 보기를 만들어 장치가 아닌 사람, 사람 등에게 효과적이고 개인화된 디지털 경험을 실시간 제공할 수 있습니다.

이 문서에서는 Experience Platform에서 ID 데이터를 삭제하고 ID 그래프가 어떤 영향을 받을 수 있는지에 대한 명확한 설명을 제공하는 데 사용할 수 있는 다양한 메커니즘에 대한 개요를 제공합니다.

## 시작하기

아래 문서는 Experience Platform의 다음 기능을 참조합니다.

* [ID 서비스](home.md): 여러 장치와 시스템에서 ID를 브리징하여 개별 고객과 고객의 행동을 더 잘 파악할 수 있습니다.
   * [ID 그래프](./ui/identity-graph-viewer.md): ID 그래프는 특정 고객에 대해 서로 다른 ID 간의 관계 맵으로서, 고객이 다른 채널에서 브랜드와 상호 작용하는 방법을 시각적으로 보여줍니다.
   * [ID 네임스페이스](namespaces.md): ID 네임스페이스는 ID 서비스의 구성 요소이며 ID가 연관되는 컨텍스트의 지표 역할을 합니다. 예를 들어 &quot;name&quot;이라는 값을 구분합니다<span>@email.com&quot; 을 이메일 주소로 보내거나 &quot;443522&quot;을 숫자 CRM ID로 사용합니다.
* [카탈로그 서비스](../catalog/home.md): 데이터 레이크 내에서 데이터 계보, 메타데이터, 파일 설명, 디렉토리 및 데이터 세트를 탐색합니다.
* [데이터 위생](../hygiene/home.md): 자동화된 데이터 세트 만료를 예약하거나 하나의 데이터 세트 또는 모든 데이터 세트에서 개별 레코드를 삭제하여 저장된 소비자 데이터를 관리합니다.
* [Adobe Experience Platform Privacy Service](../privacy-service/home.md): Adobe Experience Cloud 애플리케이션에서 개인 데이터를 액세스, 판매 거부 또는 삭제하기 위한 고객 요청을 관리합니다.
* [실시간 고객 프로필](../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 실시간으로 통합 고객 프로필을 제공합니다.

## 단일 ID 삭제

단일 ID 삭제 요청을 사용하여 그래프 내에서 ID를 삭제할 수 있으므로 ID 네임스페이스와 연결된 단일 사용자 ID에 연결된 링크가 제거됩니다. 에서 제공하는 메커니즘을 사용할 수 있습니다. [Privacy Service](../privacy-service/home.md) 고객이 데이터 삭제를 요청하고 GDPR(일반 데이터 보호 규정)과 같은 개인 정보 보호 규정을 준수하는 것과 같은 사용 사례입니다.

아래 섹션에서는 Experience Platform에서 단일 ID 삭제 요청에 사용할 수 있는 메커니즘에 대해 간략하게 설명합니다.

### Privacy Service에서 단일 ID 삭제

Privacy Service은 GDPR(General Data Protection Regulation) 및 CCPA(California Consumer Privacy Act)와 같은 개인 정보 보호 규정에 따라 지정된 대로 고객 개인 데이터에 대한 액세스, 판매 거부 또는 삭제 요청을 처리합니다. Privacy Service을 사용하여 API 또는 UI를 사용하여 작업 요청을 제출할 수 있습니다. Experience Platform이 Privacy Service에서 삭제 요청을 받으면가 요청을 수신하고 영향을 받는 데이터가 삭제로 표시되었다는 확인을 Privacy Service에게 보냅니다. 개별 ID의 삭제는 제공된 네임스페이스 및/또는 ID 값을 기반으로 합니다. 또한 해당 조직과 연관된 모든 샌드박스에 대해서도 삭제를 수행합니다. 자세한 내용은 다음 안내서를 참조하십시오. [ID 서비스의 개인 정보 보호 요청 처리](privacy.md).

아래 표는 Privacy Service에서 단일 ID 삭제에 대한 분류를 제공합니다.

| 단일 ID 삭제 | Privacy Service |
| --- | --- |
| 수락된 사용 사례 | 데이터 개인 정보 보호 요청(GDPR, CCPA)만 지원합니다. |
| 예상 지연 | 일 - 주 |
| 영향을 받는 서비스 | Privacy Service에서 단일 ID 삭제를 사용하여 데이터를 ID 서비스, 실시간 고객 프로필 또는 데이터 레이크에서 삭제할지 여부를 선택할 수 있습니다. |
| 삭제 패턴 | ID 서비스에서 ID를 삭제합니다. |

{style=&quot;table-layout:auto&quot;}

## 데이터 집합 삭제

다음 섹션에서는 Experience Platform에서 데이터 세트 및 관련 ID 링크를 삭제하는 데 사용할 수 있는 메커니즘에 대해 설명합니다.

### 카탈로그 서비스의 데이터 집합 삭제

카탈로그 서비스를 사용하여 데이터 집합 삭제 요청을 제출할 수 있습니다. 카탈로그 서비스를 사용하여 데이터 세트를 삭제하는 방법에 대한 자세한 내용은 다음 안내서를 참조하십시오 [카탈로그 서비스 API를 사용하여 개체 삭제](../catalog/api/delete-object.md). 또는 Platform UI를 사용하여 데이터 집합 삭제 요청을 제출할 수 있습니다. 자세한 내용은 [데이터 세트 사용 안내서](../catalog/datasets/user-guide.md#delete-a-dataset).

### 데이터 위생의 데이터 집합 만료

다음 [[!UICONTROL 데이터 위생] 작업 영역](../hygiene/ui/overview.md) Adobe Experience Platform UI에서 데이터 세트에 대한 만료를 예약할 수 있습니다. 데이터 세트가 만료 날짜에 도달하면 데이터 레이크, Identity 서비스 및 실시간 고객 프로필에서 별도의 프로세스를 시작하여 해당 서비스에서 데이터 세트의 컨텐츠를 제거합니다. 자세한 내용은 다음 안내서를 참조하십시오. [다음을 사용하여 데이터 세트 만료 관리 [!UICONTROL 데이터 위생] 작업 영역](../hygiene/ui/dataset-expiration.md).

아래 표는 카탈로그 서비스의 데이터 집합 삭제와 데이터 위생의 차이점을 분류합니다.

| 데이터 집합 삭제 | 카탈로그 서비스 | 데이터 위생 |
| --- | --- | --- |
| 수락된 사용 사례 | Platform에서 전체 데이터 세트 및 관련 ID 정보를 삭제합니다. | Experience Platform에 저장된 데이터 관리. |
| 예상 지연 | 일 | 일 |
| 영향을 받는 서비스 | 카탈로그 서비스를 통해 데이터 세트를 삭제하면 ID 서비스, 실시간 고객 프로필 및 데이터 레이크에서 데이터가 삭제됩니다. | 데이터 위생을 통해 데이터 세트를 삭제하면 Identity Service, Real-Time Customer Profile 및 Data Lake에서 데이터가 삭제됩니다. |
| 삭제 패턴 | 특정 데이터 세트에 의해 설정된 ID 서비스에서 연결된 ID를 삭제합니다. | 만료 일정을 기반으로 특정 데이터 세트에 의해 설정된 ID 서비스에서 연결된 ID를 삭제합니다. |

{style=&quot;table-layout:auto&quot;}

## 삭제 후 ID 그래프의 여러 상태

모든 ID 그래프 삭제를 수행하면 삭제 요청에 지정된 대로 두 개 이상의 ID 간에 링크가 제거됩니다. 데이터 집합 삭제 요청의 경우 지정된 데이터 집합에 의해 설정된 모든 ID 링크가 제거되며 그래프에서 ID를 제거할 수 있거나 제거할 수 없습니다. 단일 ID 삭제 요청의 경우 지정된 ID에 대해 ID 링크가 제거되어 모든 ID 그래프에서 ID 값 자체가 제거됩니다. 다른 ID에 대한 단일 링크가 없는 ID는 Identity 서비스에 저장되지 않습니다.

아래는 삭제를 통해 ID 그래프의 상태에 영향을 줄 수 있는 잠재적 영향에 대한 개요입니다.

| ID 그래프 상태 | 설명 |
| --- | --- |
| 부분 업데이트 | 삭제 요청이 성공적으로 처리된 후 그래프 내에 두 개 이상의 ID가 연결되어 있을 때 그래프의 부분 업데이트가 발생합니다. 삭제 후에 나머지 ID 링크는 서로 연결되어 있거나, 삭제된 ID에 따라 두 개 이상의 개별 그래프로 분할될 수 있습니다. |
| 전체 제거 | 그래프에 존재하려면 두 개 이상의 연결된 ID가 있어야 합니다. 따라서 삭제 요청으로 인해 그래프 내에 기존의 모든 링크가 제거되면 그래프가 완전히 제거됩니다. |
| 변경 내용 없음 | 특정 삭제 요청에 그래프의 구성원과 연관되지 않은 ID 또는 데이터 세트가 포함된 경우 그래프에는 영향을 주지 않습니다. 또한, 링크가 삭제되지 않은 다른 링크에 의해 설정되었다면 삭제 요청이 데이터 세트 또는 ID 데이터 세트 조합 간의 링크를 제거하더라도 그래프가 업데이트되지 않습니다. 즉, 링크가 두 개의 다른 데이터 세트에 있는 경우 데이터 세트 중 하나만 제거되므로 그래프가 업데이트되지 않습니다. |

{style=&quot;table-layout:auto&quot;}

## 다음 단계

이 문서는 Experience Platform에서 ID 및 데이터 세트를 삭제하는 데 사용할 수 있는 다양한 메커니즘에 대해 다룹니다. 이 문서에서는 ID 및 데이터 집합 삭제가 ID 그래프에 미치는 영향을 간략하게 설명합니다. ID 서비스에 대한 자세한 내용은 [ID 서비스 개요](home.md).

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