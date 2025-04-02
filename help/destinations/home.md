---
title: 대상 개요
description: 대상은 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과 미리 빌드된 통합입니다. Adobe Experience Platform의 대상 을 사용하여 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 다양한 사용 사례에 대해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.
exl-id: afd07ddc-652e-4e22-b298-feba27332462
source-git-commit: 8d57694ffe0ac962b988ebcf9f35fbb7bf816c04
workflow-type: tm+mt
source-wordcount: '1359'
ht-degree: 3%

---

# [!DNL Destinations] 개요 {#overview}

![대상 개요 배너.](./assets/overview/destinations-overview-banner.png)

**[!DNL Destinations]**&#x200B;는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있는 대상 플랫폼과 사전 설치된 통합입니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타기팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

<div id="recs-overview-body-1"></div>
<div id="recs-overview-body-2"></div>
<div id="recs-overview-body-3"></div>
<div id="recs-overview-body-4"></div>
<div id="recs-overview-body-5"></div>
<div id="recs-overview-body-6"></div>

## 대상 및 소스 {#destinations-and-sources}

Platform의 핵심 기능 중 하나는 자사 데이터를 수집하고 비즈니스 요구 사항에 맞게 활성화하는 것입니다. [소스](../sources/home.md)를 사용하여 데이터를 플랫폼으로 수집하고 플랫폼에서 데이터를 내보내는 대상으로 지정합니다.

## 대상 단계 {#steps}

* 플랫폼에서 사용할 수 있는 모든 대상의 [셀프 서비스 카탈로그](./catalog/overview.md)에서 선택하십시오.
* 대상을 사용하여 대상자 또는 데이터 세트를 마케팅 자동화 플랫폼, 디지털 광고 플랫폼 등으로 보냅니다.
* 정기적으로 원하는 대상으로 데이터 내보내기를 예약합니다.

## 컨트롤 {#controls}

[대상 작업 영역](./ui/destinations-workspace.md)의 컨트롤을 사용하면 다음 작업을 수행할 수 있습니다.

* 데이터를 활성화할 수 있는 대상 플랫폼의 카탈로그를 검색하십시오.
* 카탈로그의 대상에 대한 데이터 흐름을 만들고, 편집하고, 활성화하고, 비활성화합니다.
* 저장소 위치에 계정을 만들거나 대상 플랫폼의 계정에 플랫폼을 연결합니다.
* 대상에 활성화할 대상 또는 데이터 세트를 선택합니다.
* 전자 메일 마케팅 대상, CRM 플랫폼, 클라우드 저장소 위치 등과 같은 특정 대상으로 대상을 활성화할 때 내보낼 [XDM(경험 데이터 모델) 필드](../xdm/home.md)를 선택하십시오.
* 사람, 계정 및 잠재 고객 등 대상에 대해 다양한 유형의 프로필 및 대상자를 활성화합니다.

## 대상 유형 및 범주 {#types-and-categories}

Experience Platform을 사용하면 다양한 유형의 대상에 데이터를 활성화하여 활성화 사용 사례를 충족할 수 있습니다. 대상은 API 기반 통합에서 파일 수신 시스템과의 통합, 프로필 조회 대상 등에 이르기까지 다양합니다. 사용 가능한 모든 대상에 대한 자세한 내용은 [대상 유형 및 범주 개요](./destination-types.md)를 참조하십시오.

## Adobe이 빌드한 대상 및 파트너가 빌드한 대상 {#adobe-and-partner-built-destinations}

Experience Platform 대상 카탈로그의 일부 커넥터는 Adobe에서 빌드하고 유지 관리하는 반면, 다른 커넥터는 [Destination SDK](/help/destinations/destination-sdk/overview.md)을(를) 사용하여 파트너 회사에서 빌드하고 유지 관리합니다. 파트너가 대상을 만들고 유지 관리하는 경우 각 파트너가 빌드한 커넥터에 대한 설명서 페이지 맨 위의 참고 사항이 호출됩니다. 예를 들어 [Amazon S3 커넥터](/help/destinations/catalog/cloud-storage/amazon-s3.md)는 Adobe에서 만들고 [TikTok 커넥터](/help/destinations/catalog/social/tiktok.md)는 TikTok 팀에서 만들고 유지 관리합니다.

파트너가 작성 및 유지 관리하는 커넥터의 경우 파트너 팀이 커넥터 문제를 해결해야 할 수 있습니다(설명서 페이지의 메모에 제공된 연락 방법). Adobe 작성 및 유지 관리 커넥터와 관련된 문제는 Adobe 담당자 또는 고객 지원 센터에 문의하십시오.

## 대상 및 액세스 제어 {#access-controls}

Platform의 대상 기능은 Adobe Experience Platform 액세스 제어 권한과 함께 작동합니다. 사용자의 권한 수준에 따라 대상을 보고, 관리하고, 활성화할 수 있습니다. 개별 권한에 대한 자세한 내용을 보려면 Adobe Experience Platform의 [액세스 컨트롤](../access-control/home.md)(으)로 이동하여 페이지 하단의 테이블로 스크롤하십시오.

다음 표에서는 대상에 대해 특정 작업을 수행하는 데 필요한 권한 및 권한 조합을 간략하게 설명합니다.

| 권한 수준 | 설명 |
| ---- | ---- |
| **[!UICONTROL 대상 보기]** | Experience Platform UI의 대상 탭에 액세스하려면 **[!UICONTROL 대상 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. |
| **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 관리]** | 대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. |
| **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** | 대상에 대상을 활성화하고 워크플로우의 [매핑 단계](ui/activate-batch-profile-destinations.md#mapping)을(를) 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. |
| **[!UICONTROL 대상 보기]**, **[!UICONTROL 매핑하지 않고 세그먼트 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** | 워크플로우의 [매핑 단계](ui/activate-batch-profile-destinations.md#mapping)에 액세스하지 않고 기존 데이터 흐름에서 대상을 추가하거나 제거하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 매핑하지 않고 세그먼트 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. |
| **[!UICONTROL 대상 보기]**, **[!UICONTROL 데이터 집합 대상 관리 및 활성화]** | 대상으로 데이터 세트를 내보내려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 데이터 세트 대상 관리 및 활성화]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. |
| **[!UICONTROL ID 그래프 보기]** | 대상으로 *ID*&#x200B;를 내보내려면 **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"} |

{style="table-layout:auto"}

아래 다이어그램은 대상에 대해 수행하려는 작업에 따라 필요한 권한을 시각적으로 표시합니다.

![대상에 대해 특정 작업을 수행하는 데 필요한 권한을 보여 주는 다이어그램입니다.](/help/destinations/assets/overview/permissions-diagram.png)

액세스 제어에 대한 자세한 내용은 [액세스 제어 사용 안내서](../access-control/ui/overview.md)를 참조하세요.

### 대상에 대한 속성 기반 액세스 제어 {#attribute-based-access}

Adobe Experience Platform의 속성 기반 액세스 제어를 통해 관리자는 속성에 따라 특정 개체 및/또는 기능에 대한 액세스를 제어할 수 있습니다.

속성 기반 액세스 제어를 사용하면 권한이 있는 필드에 매핑 구성을 적용할 수 있습니다. 또한 데이터 세트의 모든 필드에 대한 액세스 권한이 없는 경우 데이터를 대상으로 내보낼 수 없습니다.

대상이 특성 기반 액세스 컨트롤로 작동하는 방법에 대한 자세한 내용은 [특성 기반 액세스 컨트롤 개요](../access-control/abac/overview.md#destinations)를 참조하십시오.

## 대상에서 프로필 제거 {#profile-removal}

대상에 대해 활성화된 대상자에서 프로필이 제거되면 해당 프로필도 대상 플랫폼의 해당 대상자에서 제거됩니다. 예를 들어 이전에 LinkedIn으로 활성화된 대상에서 프로필이 제거되면 연결된 [!UICONTROL LinkedIn과 일치하는 대상]에서 해당 프로필이 제거됩니다.

대상에서 프로필 제거(세그먼테이션 해제라고도 함)는 세그먼테이션과 동일한 케이던스에서 발생합니다. Experience Platform의 대상에서 프로필이 제거되자마자 대상에 대해 다음으로 예약된 데이터 흐름은 해당 변경 사항을 반영하고 대상 대상에서 프로필을 제거합니다.

대상 플랫폼에서 프로필 제거가 적용되는 실제 속도는 대상의 수집 및 처리 행동에 따라 달라질 수 있습니다.

## 대상 모니터링 {#destinations-monitoring}

대상에 대한 연결을 설정하고 활성화 워크플로를 완료한 후 수신 시스템으로 데이터 내보내기를 모니터링할 수 있습니다. 자세한 내용은 UI의 대상에 대한 데이터 흐름 모니터링에 대한 [안내서](/help/dataflows/ui/monitor-destinations.md)를 참조하십시오.

![대상 모니터링 페이지 예입니다.](./assets/overview/monitoring-page-example.png)

데이터가 대상으로 성공적으로 전달되고 있는지 확인할 수도 있습니다. 카탈로그의 대부분의 대상 설명서 페이지에는 Experience Platform에서 데이터를 성공적으로 가져왔음을 대상 플랫폼에서 확인하는 방법을 나타내는 *데이터 내보내기 유효성 검사*&#x200B;이(가) 있습니다. [Amazon 광고 대상](/help/destinations/catalog/advertising/amazon-ads.md#exported-data)에 대한 이 섹션의 예를 봅니다.

## 대상으로 데이터 활성화에 대한 데이터 거버넌스 제한 사항 {#data-governance}

다음을 통해 플랫폼 대상에 데이터 거버넌스가 적용됩니다.

* 대상 만들기 워크플로우에서 선택할 수 있는 *마케팅 작업*;
* 특정 사용 레이블이 포함된 데이터를 특정 마케팅 작업이 있는 대상으로 활성화하지 못하도록 제한하는 *데이터 사용 정책*.

[마케팅 작업](../data-governance/policies/overview.md) 및 [데이터 정책 위반 해결](../data-governance/enforcement/auto-enforcement.md)에 대한 자세한 내용은 플랫폼의 데이터 거버넌스 설명서를 참조하십시오.

대상 만들기 워크플로에서 마케팅 작업을 선택하는 방법에 대한 자세한 내용은 플랫폼의 다양한 대상 유형에 대한 다음 페이지를 참조하십시오.

* [Advertising 대상 - Google Ad Manager](./catalog/advertising/google-ad-manager.md)
* [Advertising 대상 - Google 광고](./catalog/advertising/google-ads-destination.md)
* [Advertising 대상 - Google 디스플레이 및 비디오 360](./catalog/advertising/google-dv360.md)
* [클라우드 스토리지 대상](./catalog/cloud-storage/overview.md)
* [이메일 마케팅 대상](./catalog/email-marketing/overview.md)
* [소셜 대상](./catalog/social/overview.md)

대상자 활성화 워크플로의 데이터 정책 위반에 대한 자세한 내용은 다음 안내서에서 **[!UICONTROL 검토]** 단계를 참조하십시오.

* [대상 데이터를 스트리밍 대상 내보내기 대상으로 활성화](./ui/activate-segment-streaming-destinations.md#review)
* [대상자 데이터를 스트리밍 프로필 내보내기 대상으로 활성화](./ui/activate-streaming-profile-destinations.md#review)
* [대상자 데이터를 활성화하여 프로필 내보내기 대상 일괄 처리](./ui/activate-batch-profile-destinations.md#review)

## 사용 약관 {#terms-and-conditions}

Beta(&quot;Beta&quot;)로 레이블이 지정된 대상을 사용함으로써, 귀하는 이로써 Beta이 어떠한 종류의 보증도 없이 ***&quot;있는 그대로&quot; 제공된다는 것을 인정합니다***.

Adobe은 Beta을 유지, 수정, 업데이트, 변경, 수정 또는 지원할 의무가 없습니다. 이러한 Beta 및/또는 동봉된 자료의 올바른 기능이나 성능에 어떤 식으로든 의존하지 말고 정보 자료를 사용하는 것이 좋습니다. Beta은 Adobe의 기밀 정보로 간주됩니다.

귀하가 Adobe에 제공한 &quot;피드백&quot;(Beta 사용 중 발생하는 문제 또는 결함, 제안, 개선 사항 및 권장 사항을 포함하되 이에 제한되지 않는 Beta 관련 정보)은 해당 피드백에 대한 모든 권한, 제목 및 관심을 포함하여 Adobe에 할당됩니다.

진행 중 피드백을 제출하거나 지원 티켓을 만들어 제안을 공유하거나 버그를 보고하면 기능 개선 사항을 확인할 수 있습니다.