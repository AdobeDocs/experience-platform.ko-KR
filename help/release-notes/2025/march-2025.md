---
title: Adobe Experience Platform 릴리스 노트 2025년 3월
description: Adobe Experience Platform의 2025년 3월 릴리스 정보.
exl-id: 3da1c912-2581-4afa-bd21-0b8303531dcd
source-git-commit: edcdf84a8cb954c15f7dd235fb14cf14e11e22c8
workflow-type: tm+mt
source-wordcount: '1250'
ht-degree: 24%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 일자: 2025년 3월 26일 목요일**

Adobe Experience Platform의 기존 기능 및 설명서 업데이트:

- [Adobe Experience Platform 릴리스 정보](#adobe-experience-platform-release-notes)
   - [대시보드](#dashboards)
   - [대상](#destinations)
   - [페더레이션된 대상자 구성](#federated-audience-composition)
   - [Segmentation Service](#segmentation-service)
   - [소스](#sources)

## 대시보드 {#dashboards}

Experience Platform은 일일 스냅샷 중에 캡처된 조직 데이터에 대한 중요한 인사이트를 볼 수 있는 여러 대시보드를 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 지표 기반 라이선스 사용 대시보드 | 이제 라이선스 사용 대시보드에 **지표** 및 **제품** 탭의 간소화된 UI가 포함됩니다. 새 **지표** 탭에서는 구매한 제품 전체에 걸쳐 추적할 수 있는 모든 라이선스 지표를 통합적으로 볼 수 있습니다. 각 지표에는 설명 및 관련 제품을 표시하는 인라인 정보 아이콘이 포함되어 있습니다. 사용자는 프로덕션 또는 개발 샌드박스를 선택하고, 대화형 차트에서 이전 사용 트렌드를 보고, 샌드박스별 데이터를 CSV 파일로 내보낼 수 있습니다. 이러한 업데이트는 라이선스 추적을 간소화하고 보다 명확한 통찰력을 제공합니다. 자세한 내용은 [라이선스 사용 대시보드 안내서](../../dashboards/guides/license-usage.md)를 참조하세요. |
| 업데이트된 예측 빈도 | 이제 라이선스 사용 대시보드는 월별이 아닌 사용량 예측 **주별**&#x200B;을(를) 업데이트하여 예상 소비에 대한 보다 정확한 통찰력을 제공합니다. 이러한 예측은 최근 추세를 기반으로 향후 6주 동안의 예상 사용량을 보여줍니다. 이러한 변경으로 신속한 의사 결정, 사전 개입 및 개선된 라이선스 계획을 실현할 수 있습니다. 자세한 내용은 [라이선스 사용 대시보드 안내서](../../dashboards/guides/license-usage.md#predicted-usage)를 참조하세요. |
| UI에서 업데이트된 지표 설명 | 명확성과 일관성을 위해 라이선스 사용 대시보드의 지표 정의가 수정되었습니다. 이제 **지표** 탭에서 각 지표 옆에 있는 인라인 정보 아이콘을 사용하여 업데이트된 설명을 대시보드에서 바로 볼 수 있습니다. 이러한 업데이트를 통해 지표를 추적하는 방법과 지표가 적용되는 제품을 보다 쉽게 이해할 수 있습니다. 자세한 내용은 [라이선스 사용 대시보드 가이드](../../dashboards/guides/license-usage.md#available-metrics)를 참조하세요. |

{style="table-layout:auto"}

액세스 권한을 부여하고 사용자 정의 위젯을 만드는 방법을 포함해 대시보드에 대한 자세한 내용은 [대시보드 개요](../../dashboards/home.md)를 읽어 보십시오.

## 대상 {#destinations}

[!DNL Destinations]는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있는 대상 플랫폼과 사전 설치된 통합입니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타기팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 대상 또는 업데이트된 대상** {#new-updated-destinations}

| 대상 | 설명 |
| --- | --- |
| [Demandbase People 연결](/help/destinations/catalog/advertising/demandbase-people.md) | 대상 타기팅, 개인화 및 제외를 위해 Demandbase 캠페인에 대한 프로필을 활성화하려면 [!DNL Demandbase People] 연결을 사용하십시오. |
| [Bombora 계정 연결](/help/destinations/catalog/advertising/bombora.md) | [계정 대상자](/help/segmentation/types/account-audiences.md)를 기반으로 대상자 타겟팅, 개인화 및 억제에 대한 Bombora 캠페인에 대한 프로필을 활성화하려면 [!DNL Bombora] 연결을 사용하십시오. |
| [비행선 특성](/help/destinations/catalog/mobile-engagement/airship-attributes.md) 업그레이드 | 2025년 3월 25일부터 대상 카탈로그에서 두 개의 **[!UICONTROL 비행선 특성]** 카드를 나란히 볼 수 있습니다. 이는 대상 서비스에 대한 내부 업그레이드 때문입니다. 기존 **[!UICONTROL 비행선 특성]** 대상 커넥터의 이름이 **[!UICONTROL (더 이상 사용되지 않음) 비행선 특성]**(으)로 변경되었으며 이제 이름이 **[!UICONTROL 비행선 특성]**&#x200B;인 새 카드를 사용할 수 있습니다. <br> 카탈로그에서 새 활성화 데이터 흐름에 **[!UICONTROL 비행선 특성]** 연결을 사용합니다. [!DNL (Deprecated) Airship Attributes] 대상에 대한 활성 데이터 흐름이 있는 경우 자동으로 업데이트되므로 사용자의 작업이 필요하지 않습니다. <br> [흐름 서비스 API](https://developer.adobe.com/experience-platform-apis/references/destinations/)를 통해 데이터 흐름을 만드는 경우 [!DNL flow spec ID] 및 [!DNL connection spec ID]을(를) 다음 값으로 업데이트해야 합니다. <ul><li> 흐름 사양 ID: `a862e0be-966e-4e5a-80d3-1bb566461986`</li><li> 연결 사양 ID: `594bc002-4a47-49b7-8a98-ac0d21045502`</li> </ul> |

{style="table-layout:auto"}

**새로운 기능 또는 업데이트된 기능** {#destinations-new-updated-functionality}

| 기능 | 설명 |
| --- | --- |
| [스트리밍 대상에 대한 보고 정확도 개선](../../dataflows/ui/monitor-destinations.md) | 2025년 3월부터 Adobe은 스트리밍 대상에 대한 보고 정확도를 높이기 위해 업데이트를 롤아웃합니다. 이 향상된 기능을 통해 Experience Platform의 보고와 대상 플랫폼 간의 정렬 성능이 향상되었습니다. <br> 이 업데이트 이전에는 **[!UICONTROL ID 실패]**&#x200B;에 모든 활성화 재시도가 포함되었습니다. 이 업데이트 이후에는 마지막 활성화 재시도만 총 횟수에 포함됩니다. <br> 이 개선 사항은 모든 스트리밍 대상에 적용됩니다. <br> 이 개선 사항이 적용되면 스트리밍 대상의 사용자는 **[!UICONTROL ID 실패]** 수가 예상대로 감소할 수 있습니다. |
| [Enterprise 및 Edge 대상에 대한 맵 유형 필드 내보내기 지원](/help/destinations/ui/export-arrays-maps-objects.md) | 이제 데이터를 [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md), [HTTP API](/help/destinations/catalog/streaming/http-destination.md), [Azure Event Hubs](/help/destinations/catalog/cloud-storage/azure-event-hubs.md) 및 [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) 대상으로 내보낼 때 활성화 워크플로의 매핑 단계에서 내보낼 맵 유형 필드를 선택할 수 있습니다. <br> ![맵 유형 필드를 Enterprise 대상으로 내보냅니다.](../2025/assets/march/export-map.png "맵 유형 필드를 Enterprise 대상으로 내보냅니다."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

자세한 내용은 [대상 개요](../../destinations/home.md)를 참조하십시오.

## 페더레이션된 대상자 구성 {#federated-audience-composition}

Federated Audience Composition의 최신 업데이트에 대한 자세한 내용은 여기에서 [전용 릴리스 노트](https://experienceleague.adobe.com/ko/docs/federated-audience-composition/using/release-notes)를 읽어 보십시오.

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service]는 고객 기반 내에서 마케팅 가능한 사용자 그룹을 구분하는 기준을 설명하여 프로필의 특정 하위 집합을 정의합니다. 세그먼트는 기록 데이터(예: 인구 통계 정보) 또는 고객과 브랜드의 상호 작용을 나타내는 시계열 이벤트를 기반으로 할 수 있습니다.

| 기능 | 설명 |
| ------- | ----------- |
| 계정 대상자 빌더 개선 사항 | 이제 Audience Builder 내에서 속성을 필터링하여 채워진 속성만 표시하고 이러한 채워진 속성에 대한 요약 데이터를 볼 수 있습니다. 이러한 개선 사항에 대한 자세한 내용은 [대상 빌더](../../rtcdp/segmentation/audience-builder.md) 설명서에서 확인할 수 있습니다. |
| 유연한 대상 평가 일반 가용성 | 이제 유연한 대상 평가를 일반적으로 사용할 수 있습니다! 유연한 대상 평가를 사용하여 시간에 민감한 커뮤니케이션에 대한 요청에 따라 새로운 대상을 만들 수 있습니다. 유연한 대상 평가에 대한 자세한 내용은 [유연한 대상 평가 개요](../../segmentation/methods/flexible-audience-evaluation.md)에서 확인할 수 있습니다. |

[!DNL Segmentation Service]에 대한 자세한 내용은 [세분화 개요](../../segmentation/home.md)를 참조하십시오.

## 소스 {#sources}

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

Experience Platform의 소스를 사용하여 Adobe 애플리케이션 또는 서드파티 데이터 소스에서 데이터를 수집합니다.

**새로운 소스**

| 기능 | 설명 |
| --- | --- |
| [!DNL Bombora Intent] | 이제 소스 카탈로그에서 [!DNL Bombora Intent] 소스를 사용할 수 있습니다. 이 소스를 사용하여 다음을 수행합니다. <ul><li>Bombora의 Company Surge Intent 데이터를 통합하여 제품 또는 서비스를 활발하게 연구하는 계정을 식별합니다.</li><li>마켓 내 계정의 우선 순위를 지정하여 정확한 세그먼트를 만들고 과다 타겟팅된 ABM 캠페인을 실행하여 전환 가능성이 가장 높은 해당 계정에 마케팅 노력이 집중할 수 있습니다.</li><li>인텐트 기반 전략을 활용하여 광고 지출을 최적화하고 참여를 증진하며 ROI를 극대화할 수 있습니다.</li></ul> 자세한 내용은 [계정을 Experience Platform에 연결](../../sources/tutorials/ui/create/data-partners/bombora.md)에 대한 안내서를 참조하십시오. [!DNL Bombora]  |
| [!DNL Demandbase Intent] | 소스 카탈로그에서 [!DNL Demandbase Intent]개의 다시 소스를 사용할 수 있습니다. 이 소스를 사용하여 다음을 수행합니다. <ul><li>Demandbase의 Account Intent 데이터를 통합하여 실시간 참여를 기반으로 고금리 계정을 식별합니다.</li><li>가장 강력한 의도 신호의 우선 순위를 지정하여 정확한 세그먼트를 만들고 하이퍼 타겟팅 캠페인을 제공하여 마케팅 활동이 전환 가능성이 가장 높은 계정에 집중할 수 있습니다.</li><li>인텐트 기반 전략을 활성화하여 광고 지출의 최적화, 참여 증가 및 ROI 향상을 가능하게 합니다.</li></ul> 자세한 내용은 [계정을 Experience Platform에 연결](../../sources/tutorials/ui/create/data-partners/demandbase.md)에 대한 안내서를 참조하십시오. [!DNL Demandbase]  |

{style="table-layout:auto"}

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [!DNL Google Ads] 소스에 대한 개선 사항 | 이제 [[!DNL Google Ads] 소스](../../sources/connectors/advertising/ads.md)를 사용하여 집계 데이터를 수집할 수 있습니다. [!DNL Google Ads Query Builder]을(를) 사용하여 Experience Platform으로 수집할 특성, 세그먼트 및 리소스를 지정할 수 있습니다. 자세한 내용은 [계정을 Experience Platform에 연결](../../sources/tutorials/ui/create/advertising/ads.md)에 대한 안내서를 참조하십시오. [!DNL Google Ads]  |
| [!DNL Microsoft Dynamics] 소스에 대한 개선 사항 | 이제 데이터의 내용과 구조를 조사할 때 지정된 [!DNL Microsoft Dynamics] 테이블의 기본 키를 지정할 수 있습니다. 이 기능을 사용하여 [!DNL Microsoft Dynamics] 원본으로 쿼리를 최적화합니다. 자세한 내용은 [API를 사용하여  [!DNL Microsoft Dynamics] 소스를 Experience Platform에 연결](../../sources/tutorials/api/create/crm/ms-dynamics.md)에 대한 안내서를 참조하십시오. |
| 셀프 서비스 소스에서 API 키 인증 지원(일괄 SDK) | 이제 새 소스를 셀프 서비스 소스(일괄 SDK)와 통합할 때 API 키 인증을 인증 유형으로 사용할 수 있습니다. 자세한 내용은 [일괄 SDK에서 인증 사양 구성](../../sources/sources-sdk/config/authspec.md)에 대한 안내서를 참조하십시오. |
| 소스에서 속성 기반 액세스 제어 지원 | 이제 소스 데이터 흐름에 대해 속성 기반 액세스 제어 기능을 사용할 수 있습니다. 자세한 내용은 다음 안내서를 참조하십시오. <ul><li>[API를 사용하여 소스 데이터 흐름에 레이블을 적용](../../sources/tutorials/api/labels.md)</li><li>[UI를 사용하여 소스 데이터 흐름에 레이블을 적용](../../sources/tutorials/ui/labels.md)합니다. |

{style="table-layout:auto"}

자세한 내용은 [소스 개요](../../sources/home.md)를 참조하십시오.
