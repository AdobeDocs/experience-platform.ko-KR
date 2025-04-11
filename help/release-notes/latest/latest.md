---
title: Adobe Experience Platform 릴리스 정보 2025년 3월
description: Adobe Experience Platform의 2025년 3월 릴리스 정보입니다.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: f0879683629ba10ed1b799e52f0adf332f079daf
workflow-type: tm+mt
source-wordcount: '1250'
ht-degree: 98%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 일자: 2025년 3월 26일**

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
| 지표 기반 라이선스 사용 대시보드 | 이제 라이선스 사용 대시보드에는 **지표** 및 **제품** 탭이 있는 간소화된 UI가 포함됩니다. 새로운 **지표** 탭을 통해 구매한 제품의 모든 추적 가능한 라이선스 지표를 통합적으로 볼 수 있습니다. 각 지표에는 설명과 관련 제품을 표시하는 인라인 정보 아이콘이 포함되어 있습니다. 사용자는 프로덕션 또는 개발 샌드박스를 선택하고, 대화형 차트에서 이전 사용 추세를 보고, 샌드박스별 데이터를 CSV 파일로 내보낼 수 있습니다. 이러한 업데이트를 통해 라이선스 추적이 간소화되고 더 명확한 인사이트를 확보할 수 있습니다. 자세한 내용은 [라이선스 사용 대시보드 안내서](../../dashboards/guides/license-usage.md)에서 확인하십시오. |
| 업데이트된 예측 빈도 | 이제 라이선스 사용 대시보드는 사용량 예측을 매월이 아닌 **매주** 업데이트하여 예상 사용량에 대한 보다 정확한 인사이트를 제공합니다. 이들 예측은 최근 추세를 바탕으로 향후 6주 동안의 예상 사용량을 보여 줍니다. 이러한 변경 사항을 통해 더욱 신속한 의사 결정, 조기 개입 및 향상된 라이선스 계획 수립이 가능합니다. 자세한 내용은 [라이선스 사용 대시보드 안내서](../../dashboards/guides/license-usage.md#predicted-usage)를 참조하십시오. |
| 업데이트된 UI 지표 설명 | 명확성과 일관성을 위해 라이선스 사용 대시보드의 지표 정의가 수정되었습니다. 이제 **지표** 탭의 각 지표 옆에 있는 인라인 정보 아이콘을 사용하여 대시보드에서 직접 업데이트된 설명을 볼 수 있습니다. 이러한 업데이트를 통해 지표를 추적하는 방법과 지표가 적용되는 제품을 더 쉽게 이해할 수 있습니다. 자세한 내용은 [라이선스 사용 대시보드 안내서](../../dashboards/guides/license-usage.md#available-metrics)를 참조하십시오. |

{style="table-layout:auto"}

액세스 권한을 부여하고 사용자 정의 위젯을 만드는 방법을 포함해 대시보드에 대한 자세한 내용은 [대시보드 개요](../../dashboards/home.md)를 읽어 보십시오.

## 대상 {#destinations}

[!DNL Destinations]는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있는 대상 플랫폼과 사전 설치된 통합입니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타기팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 대상 또는 업데이트된 대상** {#new-updated-destinations}

| 대상 | 설명 |
| --- | --- |
| [Demandbase People 연결](/help/destinations/catalog/advertising/demandbase-people.md) | [!DNL Demandbase People] 연결을 사용하면 대상자 타기팅, 개인화 및 금지를 위한 Demandbase 캠페인 프로필을 활성화할 수 있습니다. |
| [Bombora 계정 연결](/help/destinations/catalog/advertising/bombora.md) | [!DNL Bombora] 연결을 사용하면 [계정 대상자](/help/segmentation/types/account-audiences.md)를 기반으로 대상자 타기팅, 개인화 및 금지를 위한 Bombora 캠페인 프로필을 활성화할 수 있습니다. |
| [Airship 속성](/help/destinations/catalog/mobile-engagement/airship-attributes.md) 업그레이드 | 2025년 3월 25일부터 대상 카탈로그에 두 개의 **[!UICONTROL Airship 속성]** 카드가 나란히 표시됩니다. 이는 대상 서비스의 내부 업그레이드로 인한 변경 사항입니다. 기존 **[!UICONTROL Airship 속성]** 대상 커넥터의 이름이 **[!UICONTROL (더 이상 사용되지 않음) Airship 속성]**&#x200B;으로 변경되었으며, 이제 **[!UICONTROL Airship 속성]**&#x200B;이라는 이름의 새로운 카드가 제공됩니다. <br> 새로운 활성화 데이터 흐름을 위해 카탈로그의 **[!UICONTROL Airship 속성]** 연결을 사용하십시오. [!DNL (Deprecated) Airship Attributes] 대상으로의 활성 데이터 흐름이 있는 경우 해당 데이터 흐름은 자동으로 업데이트되므로 다른 조치가 필요하지 않습니다. <br> [Flow Service API](https://developer.adobe.com/experience-platform-apis/references/destinations/)를 통해 데이터 흐름을 생성하는 경우 [!DNL flow spec ID] 및 [!DNL connection spec ID]를 다음 값으로 업데이트해야 합니다. <ul><li> 흐름 사양 ID: `a862e0be-966e-4e5a-80d3-1bb566461986`</li><li> 연결 사양 ID: `594bc002-4a47-49b7-8a98-ac0d21045502`</li> </ul> |

{style="table-layout:auto"}

**새로운 기능 또는 업데이트된 기능** {#destinations-new-updated-functionality}

| 기능 | 설명 |
| --- | --- |
| [스트리밍 대상에 대한 보고 정확도 개선](../../dataflows/ui/monitor-destinations.md) | Adobe는 2025년 3월부터 스트리밍 대상에 대한 보고 정확도를 높이기 위한 업데이트를 출시할 예정입니다. 이러한 개선을 통해 Experience Platform과 대상 플랫폼 보고 간의 정렬이 더욱 향상됩니다. <br> 이 업데이트 이전에는 **[!UICONTROL ID 실패]**&#x200B;에 모든 활성화 재시도가 포함되었습니다. 이 업데이트 이후에는 마지막 활성화 재시도만 총 횟수에 포함됩니다. <br> 이 개선 사항은 모든 스트리밍 대상에 적용됩니다. <br> 이러한 개선 사항에 따라 스트리밍 대상을 사용하는 사용자에게는 **[!UICONTROL ID 실패]** 수가 감소한 것으로 표시될 수 있습니다. |
| [엔터프라이즈 및 에지 대상지에 대한 맵 유형 필드 내보내기 지원](/help/destinations/ui/export-arrays-maps-objects.md) | 이제 [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md), [HTTP API](/help/destinations/catalog/streaming/http-destination.md), [Azure Event Hubs](/help/destinations/catalog/cloud-storage/azure-event-hubs.md) 및 [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) 대상으로 데이터를 내보낼 때 활성화 워크플로의 매핑 단계에서 내보낼 맵 유형 필드를 선택할 수 있습니다. <br> ![맵 유형 필드를 엔터프라이즈 대상으로 내보냅니다.](../2025/assets/march/export-map.png "맵 유형 필드를 엔터프라이즈 대상으로 내보냅니다."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

자세한 내용은 [대상 개요](../../destinations/home.md)를 참조하십시오.

## 페더레이션된 대상자 구성 {#federated-audience-composition}

페더레이션된 대상자 구성의 최신 업데이트에 대한 자세한 내용은 [전용 릴리스 정보](https://experienceleague.adobe.com/ko/docs/federated-audience-composition/using/release-notes)를 참조하십시오.

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service]는 고객 기반 내에서 마케팅 가능한 사용자 그룹을 구분하는 기준을 설명하여 프로필의 특정 하위 집합을 정의합니다. 세그먼트는 기록 데이터(예: 인구 통계 정보) 또는 고객과 브랜드의 상호 작용을 나타내는 시계열 이벤트를 기반으로 할 수 있습니다.

| 기능 | 설명 |
| ------- | ----------- |
| 계정 대상자 빌더 개선 사항 | 이제 대상자 빌더에서 속성을 필터링하여 채워진 속성만 표시하고 채워진 속성에 대한 요약 데이터를 볼 수 있습니다. 이러한 개선 사항에 대한 자세한 내용은 [대상자 빌더](../../rtcdp/segmentation/audience-builder.md) 설명서에서 확인할 수 있습니다. |
| 유연한 대상자 평가 제한된 가용성 | 이제 유연한 대상자 평가를 일반적으로 사용할 수 있습니다. 유연한 대상자 평가를 통해 긴급 커뮤니케이션 요청 시 새로운 대상자를 만들 수 있습니다. 유연한 대상자 평가에 대한 자세한 내용은 [유연한 대상자 평가 개요](../../segmentation/methods/flexible-audience-evaluation.md)에서 확인할 수 있습니다. |

[!DNL Segmentation Service]에 대한 자세한 내용은 [세분화 개요](../../segmentation/home.md)를 참조하십시오.

## 소스 {#sources}

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

Experience Platform의 소스를 사용하여 Adobe 애플리케이션 또는 서드파티 데이터 소스에서 데이터를 수집합니다.

**새로운 소스**

| 기능 | 설명 |
| --- | --- |
| [!DNL Bombora Intent] | 이제 소스 카탈로그에서 [!DNL Bombora Intent] 소스를 사용할 수 있습니다. 이 소스를 사용하면 다음 작업을 수행할 수 있습니다. <ul><li>Bombora의 Company Surge Intent 데이터를 통합하여 제품이나 서비스를 적극적으로 조사하는 계정을 식별할 수 있습니다.</li><li>시장 내 계정에 우선순위를 부여하여 정확한 세그먼트를 만들고 고도로 타기팅된 ABM 캠페인을 실행함으로써 전환 가능성이 가장 높은 계정에 마케팅 활동을 집중할 수 있습니다.</li><li>의도 중심 전략을 활용하여 광고 지출을 최적화하고, 참여를 확대하고, ROI를 극대화할 수 있습니다.</li></ul> 자세한 내용은 [ [!DNL Bombora] 계정을 Experience Platform으로 연결하기](../../sources/tutorials/ui/create/data-partners/bombora.md)에 대한 안내서를 참조하십시오. |
| [!DNL Demandbase Intent] | 소스 카탈로그에서 [!DNL Demandbase Intent] 다시 소스를 사용할 수 있습니다. 이 소스를 사용하면 다음 작업을 수행할 수 있습니다. <ul><li>Demandbase의 Account Intent 데이터를 통합하여 실시간 참여를 기반으로 관심도가 높은 계정을 식별할 수 있습니다.</li><li>가장 강력한 의도 신호에 우선순위를 부여함으로써 정확한 세그먼트를 만들고 고도로 타기팅된 캠페인을 제공하여 전환 가능성이 가장 높은 계정에 마케팅 활동을 집중할 수 있습니다.</li><li>의도 중심 전략을 활성화하여 광고 지출을 최적화하고, 참여를 늘리고, ROI를 높일 수 있습니다.</li></ul> 자세한 내용은 [ [!DNL Demandbase] 계정을 Experience Platform으로 연결하기](../../sources/tutorials/ui/create/data-partners/demandbase.md)에 대한 안내서를 참조하십시오. |

{style="table-layout:auto"}

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [!DNL Google Ads] 소스에 대한 개선 사항 | 이제 [[!DNL Google Ads] 소스](../../sources/connectors/advertising/ads.md)를 사용하여 집계 데이터를 수집할 수 있습니다. [!DNL Google Ads Query Builder]를 사용하여 Experience Platform에 수집하고자 하는 속성, 세그먼트 및 리소스를 지정할 수 있습니다. 자세한 내용은 [ [!DNL Google Ads] 계정을 Experience Platform으로 연결하기](../../sources/tutorials/ui/create/advertising/ads.md)에 대한 안내서를 참조하십시오. |
| [!DNL Microsoft Dynamics] 소스에 대한 개선 사항 | 이제 데이터의 콘텐츠와 구조를 살펴볼 때 특정 [!DNL Microsoft Dynamics] 테이블의 기본 키를 지정할 수 있습니다. 이 기능을 사용하면 [!DNL Microsoft Dynamics] 소스를 사용하여 쿼리를 최적화할 수 있습니다. 자세한 내용은 [API를 사용하여 [!DNL Microsoft Dynamics] 소스를 Experience Platform으로 연결하기](../../sources/tutorials/api/create/crm/ms-dynamics.md)에 대한 안내서를 참조하십시오. |
| 셀프서비스 소스(Batch SDK)에서의 API 키 인증 지원 | 이제 새 소스를 셀프서비스 소스(Batch SDK)와 통합할 때 API 키 인증을 인증 유형으로 사용할 수 있습니다. 자세한 내용은 [Batch SDK에서 인증 사양을 구성하기](../../sources/sources-sdk/config/authspec.md)에 대한 안내서를 참조하십시오. |
| 소스에서의 속성 기반 액세스 제어 지원 | 이제 소스 데이터 흐름에 대해 속성 기반 액세스 제어 기능을 사용할 수 있습니다. 자세한 내용은 다음 안내서를 읽어보십시오. <ul><li>[API를 사용하여 소스 데이터 흐름에 레이블 적용](../../sources/tutorials/api/labels.md)</li><li>[UI를 사용하여 소스 데이터 흐름에 레이블 적용](../../sources/tutorials/ui/labels.md) |

{style="table-layout:auto"}

자세한 내용은 [소스 개요](../../sources/home.md)를 참조하십시오.
