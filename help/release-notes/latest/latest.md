---
title: Adobe Experience Platform 릴리스 노트 2025년 7월
description: Adobe Experience Platform의 2025년 7월 릴리스 정보.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: b0c2d5535bb4cdf7d00eaca43d65f744276494f3
workflow-type: tm+mt
source-wordcount: '1574'
ht-degree: 22%

---

# Adobe Experience Platform 릴리스 정보

>[!TIP]
>
>다른 Adobe Experience Platform 애플리케이션의 릴리스 정보는 다음 문서를 참조하십시오.
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/ko/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/releases/pre-release-notes)
>- [페더레이션된 대상자 구성](https://experienceleague.adobe.com/ko/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/ko/docs/real-time-cdp-collaboration/using/latest)

**릴리스 일자: 2025년 7월 29일 수요일**

Adobe Experience Platform의 새로운 기능 및 기존 기능 업데이트:

- [용량](#capacity)
- [대상](#destinations)
- [데이터 수집](#data-ingestion)
- [Real-Time CDP B2B 에디션](#b2b)
- [샌드박스](#sandboxes)
- [Segmentation Service](#segmentation-service)
- [소스](#sources)


## 용량 {#capacity}

>[!AVAILABILITY]
>
>이 기능은 지역에 따라 사용할 수 있습니다. 미주 지역의 사용자는 8월 11일부터 이 기능을 사용할 수 있습니다. 유럽의 사용자들은 8월 25일부터 이 기능을 사용할 수 있습니다. 아시아 지역의 사용자는 9월 8일부터 이 기능을 사용할 수 있습니다.

용량은 조직의 [보호 기능](../../rtcdp/guardrails/overview.md)을 종합적으로 볼 수 있으며, 샌드박스 수준에서 용량을 할당하여 잠재적인 용량 위반을 해결하는 방법에 대한 권장 사항을 제공합니다. 이 릴리스에서는 스트리밍 수집 및 스트리밍 세분화에 대한 용량을 확인할 수 있습니다.

자세한 내용은 [용량 개요](../../landing/license-usage-and-guardrails/capacity.md)를 참조하십시오.

## 대상 {#destinations}

[!DNL Destinations]는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있는 대상 플랫폼과 사전 설치된 통합입니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타기팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**업데이트된 대상**

| 대상 | 설명 |
| --- | --- |
| [Google Customer Match + Display &amp; Video 360](/help/destinations/catalog/advertising/google-customer-match-dv360.md) 연결의 제한된 가용성 | 6월에 모든 고객이 잠시 이용할 수 있게 된 후 Adobe은 이 통합을 제한된 가용성으로 반환했습니다. 현재 이 대상에 대한 액세스는 이미 활성화된 고객으로 제한되며, Adobe 및 Google은 구현 문제를 해결하기 위해 노력하고 있습니다. 광범위한 롤아웃이 재개된 후 이 통합을 사용하려면 Adobe 담당자에게 문의하여 의도를 나타내십시오. |
| [[!DNL The Trade Desk]](../../destinations/catalog/advertising/tradedesk.md) 내부 업그레이드 | 2025년 7월 31일 금요일부터 대상 카탈로그에 두 개의 [!DNL The Trade Desk] 카드가 나란히 표시됩니다. 이는 대상 서비스의 내부 업그레이드로 인한 변경 사항입니다. <br><br>기존 [!DNL The Trade Desk] 대상 커넥터의 이름이 **[!UICONTROL (더 이상 사용되지 않음)로 변경되었으며, 이름이]** The Trade Desk **[!UICONTROL 인 새 카드를 사용할 수 있습니다.]** 새 활성화 데이터 흐름을 보려면 카탈로그에서 새 **[!UICONTROL Trade Desk]** 연결을 사용하십시오. <br><br>**[!UICONTROL (사용되지 않음) Trade Desk]** 대상에 대한 활성 데이터 흐름이 있는 경우 자동으로 업데이트되므로 사용자의 작업이 필요하지 않습니다. <br><br>흐름 서비스 API[를 통해 데이터 흐름을 만드는 경우 ](https://developer.adobe.com/experience-platform-apis/references/destinations/) 및 [!DNL flow spec ID]을(를) 다음 값으로 업데이트해야 합니다.[!DNL connection spec ID]<ul><li>흐름 사양 ID: `86134ea1-b014-49e8-8bd3-689f4ce70578`</li><li>연결 사양 ID: `1029798b-a97f-4c21-81b2-e0301471166e`</li></ul> |

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 대상 연결에 대한 계정 이름 및 설명 | 이제 대상에 연결할 때 [계정 이름 및 설명을 추가](/help/destinations/ui/connect-destination.md)할 수 있으므로 여러 계정이 있는 대상을 보다 효율적으로 관리할 수 있습니다. |
| 에지 대상에 대한 데이터 스트림 정보 개선 | [Adobe Target](/help/destinations/catalog/personalization/adobe-target-v2.md) 및 [사용자 지정 Personalization](/help/destinations/catalog/personalization/custom-personalization.md) 대상에 대한 오른쪽 레일 정보가 데이터 스트림 이름을 표시하도록 개선되어 연결된 데이터 스트림 구성에 대한 더 명확한 가시성을 제공하고 기존 데이터 흐름을 검토할 때 혼동을 줄이는 데 도움이 됩니다. 사용자 인터페이스의 명확성을 개선하기 위해 대상 구성 화면의 **[!UICONTROL 데이터 스트림 ID]** 선택기가 **[!UICONTROL 데이터 스트림]**(으)로 업데이트되었습니다. |
| 대상 선택에서의 마케팅 작업 가시성 | 이제 마케팅 작업이 대상 작업 영역의 **[[!UICONTROL 찾아보기]](/help/destinations/ui/destinations-workspace.md#browse)** 탭의 오른쪽 레일과 **[[!UICONTROL 데이터 흐름 실행]](/help/dataflows/ui/monitor-destinations.md)** 페이지에 표시되므로 보기 페이지로 이동할 필요 없이 마케팅 작업 변경 사항을 즉시 볼 수 있습니다. 이 개선 사항을 통해 대상 설정 중에 마케팅 작업 구성을 보다 쉽게 확인할 수 있으므로 사용자 경험이 개선됩니다. |
| 대상에 대한 [!BADGE 제한된 베타]{type=Informative} 마케팅 작업 편집 | 이제 기존 대상에 대해 [마케팅 작업을 편집](/help/destinations/ui/edit-activation.md#edit-marketing-actions)할 수 있습니다. 이 기능은 현재 제한된 베타에 있습니다. 액세스 권한을 요청하려면 Adobe 담당자에게 문의하십시오. |
| [!BADGE 제한된 베타]{type=Informative} 대상 편집 | 이제 대상 구성을 만든 후 [편집](/help/destinations/ui/edit-destination.md)할 수 있습니다. 이 기능은 현재 제한된 베타에 있습니다. 액세스 권한을 요청하려면 Adobe 담당자에게 문의하십시오. |

**수정 사항**

| 문제 | 설명 |
| --- | --- |
| 범주 스크롤 기능 | 대상 및 소스 카탈로그의 카테고리 사이드 메뉴가 마우스오버에서 제대로 스크롤되지 않던 문제를 수정하여 대상 카테고리를 탐색하는 사용자의 탐색 유용성을 개선했습니다. |

자세한 내용은 [대상 개요](../../destinations/home.md)를 참조하십시오.

## 데이터 수집 {#ingestion}

Experience Platform은 다양한 소스에서 일괄 데이터 수집과 스트리밍 데이터 수집을 모두 지원하는 포괄적인 데이터 수집 프레임워크를 제공합니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 스트리밍 프로필 수집 모니터링 지원 | 이제 스트리밍 프로필 수집에 대한 실시간 모니터링을 사용할 수 있으므로 처리량, 지연 시간 및 데이터 품질 지표에 대한 투명성을 제공합니다. 사전 예방적 경고 및 조치 가능한 통찰력을 지원하여 데이터 엔지니어가 용량 위반 및 수집 문제를 식별하는 데 도움이 됩니다. 자세한 내용은 [스트리밍 프로필 수집 모니터링](../../dataflows/ui/monitor-streaming-profile.md)에 대한 안내서를 참조하십시오. |

자세한 내용은 [데이터 수집 개요](../../ingestion/home.md)를 참조하십시오.

## Real-Time CDP B2B 에디션 {#b2b}

Real-Time CDP B2B edition은 포괄적인 B2B 고객 데이터 관리 기능을 제공하므로, 조직은 통합된 고객 프로필을 구축하고, 정교한 B2B 대상을 만들고, 다양한 마케팅 채널에서 데이터를 활성화할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| B2B 아키텍처 업그레이드 | Experience Platform은 B2B 속성을 사용하는 다중 엔티티 대상을 크게 개선하는 새 B2B 아키텍처로 업그레이드하고 있습니다. 이 업그레이드는 병합 정책 지원을 통합하고, 대상자 수의 정확성을 개선하고, 엔티티 해결 기능을 향상시킵니다. 변경 내용에 대한 포괄적인 상세 정보는 [Real-Time CDP B2B edition 아키텍처 업그레이드 개요](../../rtcdp/b2b-architecture-upgrade.md)를 참조하십시오. |
| 다중 엔티티 대상을 위한 병합 정책 통합 | B2B 속성을 사용하는 다중 엔티티 대상은 이제 여러 병합 정책을 지원하는 대신 단일 병합 정책(기본 병합 정책)만 지원합니다. 이 변경 사항은 일관된 대상 구성을 보장하고 병합 논리 관리를 단순화합니다. 자세한 내용은 [병합 정책 개요](../../profile/merge-policies/overview.md)를 참조하십시오. |
| B2B 엔티티에 대한 향상된 대상 수 | 계정 및 기회와 같은 B2B 엔티티가 있는 대상에 대한 대상 크기 예상치는 이제 실시간 세분화 결과를 기반으로 정확하게 계산됩니다. 이러한 개선은 복잡한 B2B 관계를 포함하는 대상자에 대해 보다 정확하고 신뢰할 수 있는 추정치를 제공한다. |
| 대상자 멤버십에 대한 계정 스냅샷 | 이제 스냅샷 내보내기의 계정 엔티티에 대한 대상 멤버십 세부 정보가 포함되어 계정 수준 대상 상태, 타임스탬프 및 멤버십 지표에 액세스할 수 있습니다. 프로필(개인) 및 계정 세분화 모델 간의 기능 패리티를 제공합니다. |
| 다중 엔티티 대상의 샌드박스 도구 변경 사항 | B2B 엔티티와 마이그레이션 전에 내보낸 경험 이벤트를 사용하여 다중 엔티티 대상을 가져오는 기능은 더 이상 지원되지 않습니다. 이러한 대상은 가져오기 유효성 검사에 실패하며 자동으로 새 아키텍처로 변환할 수 없습니다. 대상 샌드박스로 가져오기 전에 마이그레이션 후 대상을 다시 내보내야 합니다. 자세한 내용은 샌드박스 도구에 대해 지원되는 개체에 대한 [안내서](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling)를 참조하십시오. |
| B2B 엔티티 API 사용 중단 | B2B 엔터티(계정 사용자 관계, 영업 기회 사용자 관계, 캠페인, 캠페인 멤버, 마케팅 목록 및 마케팅 목록 멤버)에 대한 [!DNL Profile Access] API 조회 작업이 이제 더 이상 사용되지 않습니다. 또한 B2B 엔터티(계정, 계정-사용자 관계, 영업 기회, 영업 기회-사용자 관계, 캠페인, 캠페인 멤버, 마케팅 목록 및 마케팅 목록 멤버)에 대한 [!DNL Profile Access] API 삭제 작업도 더 이상 사용되지 않습니다. 자세한 내용은 [엔터티 끝점 API 안내서](../../profile/api/entities.md)를 참조하십시오. |
| 엔티티 확인을 위한 ID 네임스페이스 업데이트 | 이제 계정 및 영업 기회 엔터티는 특정 ID 네임스페이스와 시간 우선 순위 기반 병합을 사용합니다(계정의 경우 `b2b_account`, 영업 기회의 경우 `b2b_opportunity`). 다른 모든 엔티티는 시간 우선 순위 기반 병합을 사용하여 기본 ID가 겹치게 병합됩니다. 엔터티 확인에 대한 자세한 내용은 [엔터티 끝점 API 안내서](../../profile/api/entities.md)를 참조하십시오. |

자세한 내용은 [Real-Time CDP B2B edition 개요](../../rtcdp/b2b-overview.md)를 참조하세요.

## 샌드박스 {#sandboxes}

Experience Platform은 글로벌 규모로 디지털 경험 애플리케이션을 강화하기 위해 빌드되었습니다. 기업은 여러 디지털 경험 애플리케이션을 동시에 실행하는 경우가 많으며, 운영 규정 준수를 보장하면서 이러한 애플리케이션의 개발, 테스트 및 배포를 처리해야 합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 다중 엔티티 대상 가져오기 변경 사항 | 샌드박스 툴이 새로운 B2B 아키텍처 업그레이드를 지원하도록 업데이트되었습니다. B2B 엔티티 및 경험 이벤트가 포함된 다중 엔티티 대상은 아키텍처 업그레이드 후 샌드박스 도구를 통해 Target 샌드박스로 가져오기 전에 다시 내보내야 합니다. 업그레이드 전 버전을 가져오면 유효성 검사가 실패합니다. 자세한 내용은 샌드박스 도구에 대해 지원되는 개체에 대한 [안내서](../../sandboxes/ui/sandbox-tooling.md#objects-supported-for-sandbox-tooling)를 참조하십시오. |

샌드박스에 대한 자세한 내용은 [샌드박스 개요](../../sandboxes/home.md)를 참조하십시오.

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service]는 고객 기반 내에서 마케팅 가능한 사용자 그룹을 구분하는 기준을 설명하여 프로필의 특정 하위 집합을 정의합니다. 대상자는 기록 데이터(예: 인구 통계 정보) 또는 고객과 브랜드의 상호 작용을 나타내는 시계열 이벤트를 기반으로 할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 외부 대상 API | 외부 대상 API를 사용하여 외부에서 생성된 대상을 프로그래밍 방식으로 Adobe Experience Platform으로 가져올 수 있습니다. 자세한 내용은 [외부 대상 끝점 안내서](../../segmentation/api/external-audiences.md)를 참조하십시오. |

세분화에 대한 자세한 내용은 [세분화 서비스 개요](../../segmentation/home.md)를 참조하세요.

## 소스 {#sources}

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새로운 소스**

| 소스 | 설명 |
| --- | --- |
| [!BADGE 에 대한 &#x200B;]{type=Informative}Beta[!DNL Didomi] 지원(스트리밍 SDK) | [!DNL Didomi] 소스를 사용하여 [!DNL Didomi]에서 동의 및 환경 설정 관리 데이터를 수집하여 개인 정보 보호 규정 준수 및 동의 기반 마케팅 전략을 지원합니다. 설정 방법에 대한 자세한 내용은 [[!DNL Didomi] 소스 개요](../../sources/connectors/consent-and-preferences/didomi.md)를 읽어 보십시오. 원본 연결을 만드는 단계는 [[!DNL Didomi] 원본 연결 안내서](../../sources/tutorials/ui/create/consent-and-preferences/didomi.md)를 참조하세요. |

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [!DNL Flow Service] API를 사용하여 선택한 소스에서 변경 데이터 캡처 지원 | 이제 소스 커넥터를 사용하여 증분 수집을 위한 변경 데이터 캡처를 활성화하는 데이터 흐름을 만들 수 있습니다. 이 기능을 통해 고객은 증분 수집을 위해 데이터 유형을 변경할 수 있으므로 데이터의 안정성을 높이고 처리 오버헤드를 줄일 수 있습니다. 자세한 내용은 [소스에 대한 변경 데이터 캡처 사용](../../sources/tutorials/api/change-data-capture.md)에 대한 설명서를 참조하십시오. |
| [!DNL Salesforce]에서 레코드의 소프트 삭제 지원 | 이제 [!DNL Salesforce] 원본은 선택적 `includeDeletedObjects` 매개 변수를 통해 일시 삭제된 레코드를 포함할 수 있습니다. true로 설정하면 고객은 일시 삭제된 레코드를 [!DNL Salesforce] 쿼리에 포함하고 이러한 레코드를 Experience Platform으로 가져올 수 있습니다. 자세한 내용은 [[!DNL Salesforce] 소스 설명서](../../sources/connectors/crm/salesforce.md)를 참조하십시오. |

자세한 내용은 [소스 개요](../../sources/home.md)를 참조하십시오.
