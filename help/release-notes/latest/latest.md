---
title: Adobe Experience Platform 릴리스 정보 2025년 7월
description: Adobe Experience Platform의 2025년 7월 릴리스 정보입니다.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: b0c2d5535bb4cdf7d00eaca43d65f744276494f3
workflow-type: tm+mt
source-wordcount: '1574'
ht-degree: 89%

---

# Adobe Experience Platform 릴리스 정보

>[!TIP]
>
>다른 Adobe Experience Platform 애플리케이션의 릴리스 정보는 다음 문서를 참조하십시오.
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/ko/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/releases/pre-release-notes)
>- [페더레이션된 대상자 컴포지션](https://experienceleague.adobe.com/ko/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/ko/docs/real-time-cdp-collaboration/using/latest)

**릴리스 일자: 2025년 7월 29일**

Adobe Experience Platform의 새로운 기능 및 기존 기능 업데이트:

- [용량](#capacity)
- [대상](#destinations)
- [데이터 수집](#data-ingestion)
- [Real-Time CDP B2B Edition](#b2b)
- [샌드박스](#sandboxes)
- [Segmentation Service](#segmentation-service)
- [소스](#sources)


## 용량 {#capacity}

>[!AVAILABILITY]
>
>이 기능은 지역에 따라 사용할 수 있습니다. 아메리카 지역 사용자의 경우 8월 11일부터 제공될 예정입니다. 유럽 사용자의 경우 8월 25일부터 제공될 예정입니다. 아시아 사용자의 경우 9월 8일부터 제공될 예정입니다.

용량은 조직의 [가드레일](../../rtcdp/guardrails/overview.md)에 대한 포괄적인 보기를 제공하며 샌드박스 수준에서 용량을 할당하여 잠재적인 용량 위반을 해결하는 방법에 대한 권장 사항을 제공합니다. 이 릴리스에서는 스트리밍 수집 및 스트리밍 세분화에 대한 용량을 모두 볼 수 있습니다.

자세한 내용은 [용량 개요](../../landing/license-usage-and-guardrails/capacity.md)를 참조하십시오.

## 대상 {#destinations}

[!DNL Destinations]는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있는 대상 플랫폼과 사전 설치된 통합입니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타기팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**업데이트된 대상**

| 대상 | 설명 |
| --- | --- |
| [Google 고객 일치 타기팅 + 디스플레이 및 비디오 360](/help/destinations/catalog/advertising/google-customer-match-dv360.md) 연결 제한적 제공 | Adobe는 6월에 모든 고객에게 잠시 제공되었던 이 통합 기능을 다시 제한적으로 제공합니다. 현재 이 대상에 대한 액세스는 이미 활성화된 고객으로 제한되어 있으며, Adobe와 Google는 구현 문제를 해결하기 위해 노력하고 있습니다. 더 광범위한 출시가 재개된 후 이 통합을 사용하고 싶다면 Adobe 담당자에게 연락하여 의사를 전달해 주시기 바랍니다. |
| [[!DNL The Trade Desk]](../../destinations/catalog/advertising/tradedesk.md) 내부 업그레이드 | 2025년 7월 31일 금요일부터 대상 카탈로그에 두 개의 [!DNL The Trade Desk] 카드가 나란히 표시됩니다. 이는 대상 서비스의 내부 업그레이드로 인한 변경 사항입니다. <br><br>기존 [!DNL The Trade Desk] 대상 커넥터의 이름이 **[!UICONTROL (더 이상 사용되지 않음)로 변경되었으며, 이름이]** The Trade Desk **[!UICONTROL 인 새 카드를 사용할 수 있습니다.]** 새 활성화 데이터 흐름을 보려면 카탈로그에서 새 **[!UICONTROL Trade Desk]** 연결을 사용하십시오. <br><br>**[!UICONTROL (사용되지 않음) Trade Desk]** 대상에 대한 활성 데이터 흐름이 있는 경우 자동으로 업데이트되므로 사용자의 작업이 필요하지 않습니다. <br><br>흐름 서비스 API[를 통해 데이터 흐름을 만드는 경우 ](https://developer.adobe.com/experience-platform-apis/references/destinations/) 및 [!DNL flow spec ID]을(를) 다음 값으로 업데이트해야 합니다.[!DNL connection spec ID]<ul><li>흐름 사양 ID: `86134ea1-b014-49e8-8bd3-689f4ce70578`</li><li>연결 사양 ID: `1029798b-a97f-4c21-81b2-e0301471166e`</li></ul> |

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 대상 연결에 대한 계정 이름 및 설명 | 이제 대상에 연결할 때 [계정 이름과 설명](/help/destinations/ui/connect-destination.md)을 추가할 수 있으므로 여러 계정이 있는 대상을 더 효과적으로 관리할 수 있습니다. |
| 에지 대상에 대한 향상된 데이터스트림 정보 | [Adobe Target](/help/destinations/catalog/personalization/adobe-target-v2.md) 및 [사용자 정의 개인화](/help/destinations/catalog/personalization/custom-personalization.md) 대상에 대한 오른쪽 레일 정보가 데이터스트림 이름을 표시하도록 개선되어 관련 데이터스트림 구성을 더 명확하게 파악하고 기존 데이터 흐름을 검토할 때 혼동을 줄일 수 있습니다. 대상 구성 화면의 **[!UICONTROL 데이터스트림 ID]** 선택기가 사용자 인터페이스의 명확성 향상을 위해 **[!UICONTROL 데이터스트림]**&#x200B;으로 업데이트되었습니다. |
| 대상 선택 시 마케팅 액션 가시성 | 이제 마케팅 활동이 대상 작업 공간의 **[[!UICONTROL 찾아보기]](/help/destinations/ui/destinations-workspace.md#browse)** 탭 오른쪽 레일과 **[[!UICONTROL 데이터 흐름 실행]](/help/dataflows/ui/monitor-destinations.md)** 페이지에 표시되어 보기 페이지로 이동할 필요 없이 마케팅 액션 변경 사항을 즉시 확인할 수 있습니다. 이 개선 사항은 대상 설정 중에 마케팅 액션 구성을 더 쉽게 확인할 수 있도록 하여 사용자 경험을 향상시킵니다. |
| [!BADGE 제한적 Beta]{type=Informative} 대상에 대한 마케팅 액션 편집 | 이제 기존 대상에 대해 [마케팅 작업을 편집](/help/destinations/ui/edit-activation.md#edit-marketing-actions)할 수 있습니다. 이 기능은 현재 제한적 Beta 버전으로 제공됩니다. 액세스 권한을 요청하려면 Adobe 담당자에게 문의하십시오. |
| [!BADGE 제한적 Beta]{type=Informative} 대상 편집 | 이제 대상 구성을 만든 후 [편집](/help/destinations/ui/edit-destination.md)할 수 있습니다. 이 기능은 현재 제한적 Beta 버전으로 제공됩니다. 액세스 권한을 요청하려면 Adobe 담당자에게 문의하십시오. |

**수정 사항**

| 문제 | 설명 |
| --- | --- |
| 카테고리 스크롤 기능 | 대상 및 소스 카탈로그의 카테고리 사이드 메뉴가 마우스오버 시 제대로 스크롤되지 않던 문제가 해결되어 대상 카테고리를 탐색하는 사용자의 탐색 편의성이 향상되었습니다. |

자세한 내용은 [대상 개요](../../destinations/home.md)를 참조하십시오.

## 데이터 수집 {#ingestion}

Experience Platform은 다양한 소스에서 배치 및 스트리밍 데이터 수집을 모두 지원하는 포괄적인 데이터 수집 프레임워크를 제공합니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 스트리밍 프로필 수집 모니터링 지원 | 이제 처리량, 지연 시간 및 데이터 품질 지표에 대한 투명성을 제공하는 스트리밍 프로필 수집에 대한 실시간 모니터링을 사용할 수 있습니다. 이를 통해 데이터 엔지니어는 용량 위반 및 수집 문제를 식별하는 데 도움이 되는 사전 예방적 경고 및 실행 가능한 인사이트를 얻을 수 있습니다. 자세한 내용은 [스트리밍 프로필 수집 모니터링](../../dataflows/ui/monitor-streaming-profile.md)에 대한 안내서를 참조하십시오. |

자세한 내용은 [데이터 수집 개요](../../ingestion/home.md)를 참조하십시오.

## Real-Time CDP B2B Edition {#b2b}

Real-Time CDP B2B Edition은 포괄적인 B2B 고객 데이터 관리 기능을 제공하여 조직이 통합된 고객 프로필을 빌드하고, 정교한 B2B 대상자를 생성하며, 다양한 마케팅 채널에서 데이터를 활성화할 수 있도록 합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| B2B 아키텍처 업그레이드 | Experience Platform이 B2B 속성을 가진 다중 엔티티 대상자에 대한 중요한 개선 사항을 도입하는 새로운 B2B 아키텍처로 업그레이드되고 있습니다. 이 업그레이드는 병합 정책 지원을 통합하고, 대상자 수의 정확도를 높이며, 엔티티 해결 기능을 향상시킵니다. 변경 사항에 대한 포괄적인 세부 내용을 보려면 [Real-Time CDP B2B Edition 아키텍처 업그레이드 개요](../../rtcdp/b2b-architecture-upgrade.md)를 읽어 보십시오. |
| 다중 엔티티 대상자에 대한 병합 정책 통합 | B2B 속성이 있는 다중 엔티티 대상자는 더 이상 여러 병합 정책을 지원하지 않고 단일 병합 정책(기본 병합 정책)만 지원합니다. 이 변경 사항은 일관된 대상자 구성을 보장하고 병합 논리 관리를 간소화합니다. 자세한 내용은 [병합 정책 개요](../../profile/merge-policies/overview.md)를 참조하십시오. |
| B2B 엔티티에 대한 향상된 대상자 수 | 계정 및 기회와 같은 B2B 엔티티가 있는 대상자의 규모 추정치가 이제 실시간 세분화 결과를 기반으로 정확해졌습니다. 이 개선 사항은 복잡한 B2B 관계와 관련된 대상자에 대해 더 정확하고 신뢰할 수 있는 추정치를 제공합니다. |
| 대상자 멤버십에 대한 계정 스냅샷 | 이제 스냅샷 내보내기 시 계정 엔티티에 대한 대상자 멤버십 세부 정보가 포함되어 계정 수준 대상자 상태, 타임스탬프 및 멤버십 지표에 액세스할 수 있습니다. 이를 통해 프로필(개인) 및 계정 세분화 모델 간에 기능 동등성이 제공됩니다. |
| 다중 엔티티 대상자에 대한 샌드박스 도구 변경 사항 | 마이그레이션 전에 내보낸 B2B 엔티티 및 경험 이벤트가 포함된 다중 엔티티 대상자를 가져오는 기능은 더 이상 지원되지 않습니다. 이들 대상자는 가져오기 유효성 검사에 실패하며 새 아키텍처로 자동 변환될 수 없습니다. 마이그레이션 후 대상 샌드박스로 가져오기 전에 대상자를 다시 내보내야 합니다. 자세한 내용은 [샌드박스 도구에 대해 지원되는 오브젝트에 대한 안내서](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling)를 참조하십시오. |
| B2B 엔티티 API 지원 중단 | B2B 엔티티(계정-개인 관계, 기회-개인 관계, 캠페인, 캠페인 멤버, 마케팅 목록 및 마케팅 목록 멤버)에 대한 [!DNL Profile Access] API 조회 작업이 더 이상 지원되지 않습니다. 또한 B2B 엔티티(계정, 계정-개인 관계, 기회, 기회-개인 관계, 캠페인, 캠페인 멤버, 마케팅 목록 및 마케팅 목록 멤버)에 대한 [!DNL Profile Access] API 삭제 작업도 더 이상 지원되지 않습니다. 자세한 내용은 [엔티티 엔드포인트 API 안내서](../../profile/api/entities.md)를 참조하십시오. |
| 엔티티 해결을 위한 ID 네임스페이스 업데이트 | 이제 계정 및 기회 엔티티는 특정 ID 네임스페이스(계정의 경우 `b2b_account`, 기회의 경우 `b2b_opportunity`)를 사용하여 시간 우선순위 기반 병합을 사용합니다. 다른 모든 엔티티는 시간 우선순위 기반 병합을 사용하여 병합된 기본 ID 중복 항목으로 통합됩니다. 엔티티 해결에 대한 자세한 내용은 [엔티티 엔드포인트 API 안내서](../../profile/api/entities.md)를 참조하십시오. |

자세한 내용은 [Real-Time CDP B2B Edition 개요](../../rtcdp/b2b-overview.md)를 참조하십시오.

## 샌드박스 {#sandboxes}

Experience Platform은 전 세계적으로 디지털 체험 애플리케이션을 풍부하게 제공하기 위해 빌드되었습니다. 기업은 여러 디지털 경험 애플리케이션을 동시에 실행하는 경우가 많으며, 운영 규정 준수를 보장하면서 이러한 애플리케이션의 개발, 테스트 및 배포를 처리해야 합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 다중 엔티티 대상자 가져오기 변경 사항 | 샌드박스 도구가 새로운 B2B 아키텍처 업그레이드를 지원하도록 업데이트되었습니다. B2B 엔티티 및 경험 이벤트를 포함하는 다중 엔티티 대상자는 샌드박스 도구를 통해 대상 샌드박스로 가져오기 전에 아키텍처 업그레이드 후 다시 내보내야 합니다. 업그레이드 이전 버전을 가져오면 유효성 검사에 실패합니다. 자세한 내용은 [샌드박스 도구에 대해 지원되는 오브젝트에 대한 안내서](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling)를 참조하십시오. |

샌드박스에 대한 자세한 내용은 [샌드박스 개요](../../sandboxes/home.md)를 참조하십시오.

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service]는 고객 기반 내에서 마케팅 가능한 사용자 그룹을 구분하는 기준을 설명하여 프로필의 특정 하위 집합을 정의합니다. 대상자는 기록 데이터(예: 인구 통계 정보) 또는 고객과 브랜드의 상호 작용을 나타내는 시계열 이벤트를 기반으로 할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 외부 대상자 API | 외부 대상자 API를 사용하여 외부에서 생성된 대상자를 Adobe Experience Platform으로 프로그래밍 방식으로 가져올 수 있습니다. 자세한 내용은 [ 외부 대상자 엔드포인트 안내서](../../segmentation/api/external-audiences.md)를 참조하십시오. |

세분화에 대한 자세한 내용은 [세분화 서비스 개요](../../segmentation/home.md)를 참조하십시오.

## 소스 {#sources}

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새로운 소스**

| 소스 | 설명 |
| --- | --- |
| [!BADGE 에 대한 &#x200B;]{type=Informative}Beta[!DNL Didomi] 지원(스트리밍 SDK) | [!DNL Didomi] 소스를 사용하여 [!DNL Didomi]에서 동의 및 기본 설정 관리 데이터를 수집하여 개인 정보 보호 규정 및 동의 기반 마케팅 전략을 준수할 수 있습니다. 설정하는 방법에 대한 자세한 내용은 [[!DNL Didomi] 소스 개요](../../sources/connectors/consent-and-preferences/didomi.md)를 참조하십시오. 소스 연결을 생성하는 단계는 [[!DNL Didomi] 소스 연결 안내서](../../sources/tutorials/ui/create/consent-and-preferences/didomi.md)를 참조하십시오. |

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [!DNL Flow Service] API를 사용하는 일부 소스에서 변경 데이터 캡처 지원 | 이제 소스 커넥터를 사용하여 증분 수집을 위한 변경 데이터 캡처를 활성화하는 데이터 흐름을 생성할 수 있습니다. 이 기능을 통해 고객은 증분 수집을 위해 변경 데이터 유형을 가져와 데이터 신선도를 높이고 처리 오버헤드를 줄일 수 있습니다. 자세한 내용은 [소스에 대한 변경 데이터 캡처 사용](../../sources/tutorials/api/change-data-capture.md)에 관한 설명서를 참조하십시오. |
| [!DNL Salesforce]에서 레코드의 소프트 삭제 지원 | 이제 [!DNL Salesforce] 원본은 선택적 `includeDeletedObjects` 매개 변수를 통해 일시 삭제된 레코드를 포함할 수 있습니다. true로 설정하면 고객은 일시 삭제된 레코드를 [!DNL Salesforce] 쿼리에 포함하고 이러한 레코드를 Experience Platform으로 가져올 수 있습니다. 자세한 내용은 [[!DNL Salesforce] 소스 설명서](../../sources/connectors/crm/salesforce.md)를 참조하십시오. |

자세한 내용은 [소스 개요](../../sources/home.md)를 참조하십시오.
