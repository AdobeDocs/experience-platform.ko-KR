---
title: Adobe Experience Platform 릴리스 정보 2024년 10월
description: Adobe Experience Platform의 2024년 10월 릴리스 정보입니다.
exl-id: 5e2112b8-2a0a-4c1e-af3e-b00d8cc4f4cf
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1160'
ht-degree: 97%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 일자: 2024년 10월 29일**

Adobe Experience Platform의 기존 기능 및 설명서 업데이트:

- [대시보드](#dashboards)
- [데이터 수집](#data-collection-)
- [대상](#destinations)
- [Segmentation Service](#segmentation-service)
- [샌드박스](#sandboxes)
- [소스](#sources)

## 대시보드 {#dashboards}

Experience Platform은 일일 스냅샷 중에 캡처된 조직 데이터에 대한 중요한 인사이트를 볼 수 있는 여러 대시보드를 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| Data Distiller 템플릿 | 다양한 템플릿을 탐색하여 대상자 데이터에 대한 체계적인 통찰력을 얻으십시오. **고급 [!UICONTROL 대상자 오버랩]**, **[!UICONTROL 대상자 비교]**, **[!UICONTROL 대상자 트렌드]**, **[!UICONTROL 대상자 ID 오버랩]**&#x200B;과 같은 대시보드를 사용하여 데이터 기반 의사 결정을 내리고 세분화를 최적화하며 참여 전략을 강화할 수 있습니다. 자세한 내용은 [Data Distiller 템플릿 안내서](../../dashboards/sql-insights-query-pro-mode/templates/overview.md)를 참조하십시오. |
| 고급 대상자 오버랩 | 특정 대상자에 대한 대상자 교집합을 빠르게 분석하거나 모든 오버랩을 조회하여 전체 대상자 세트에 대한 귀중한 인사이트를 발견하십시오. 이러한 인사이트를 활용하여 세분화를 개선하고 중복되는 메시지를 줄이며 마케팅 효율성 향상을 위한 보다 타기팅된 캠페인을 만들 수 있습니다. 자세한 내용은 [고급 대상자 오버랩 안내서](../../dashboards/sql-insights-query-pro-mode/templates/overlaps.md)를 참조하십시오. |
| 대상자 비교 개선 사항 | **대상자 비교** 대시보드를 사용하여 다양한 대상자 그룹 간의 주요 지표를 나란히 비교해 보십시오. 이 대시보드를 통해 대상자 규모, ID 구성 등의 구체적인 기간과 KPI를 선택하여 대상자 세분화 및 타기팅 전략에 대한 정보에 입각한 결정을 내릴 수 있습니다. 자세한 내용은 [대상자 비교 안내서](../../dashboards/sql-insights-query-pro-mode/templates/comparison.md)를 참조하십시오. |
| 대상자 트렌드 시각화 | **[!UICONTROL 대상자 트렌드]** 대시보드를 사용하여 시간 경과에 따른 대상자 지표를 분석하십시오. 대상자 규모, ID 수, 단일 ID 프로필 수에 대한 트렌드를 시각화하여 대상자의 변화를 모니터링하고, 성장을 측정하고, 참여 전략을 개선하는 데 도움이 됩니다. 자세한 내용은 [대상자 트렌드 안내서](../../dashboards/sql-insights-query-pro-mode/templates/trends.md)를 참조하십시오. |
| ID 오버랩 분석 | **[!UICONTROL 대상자 ID 오버랩]** 대시보드를 사용하여 선택한 대상자의 ID 중복을 분석하십시오. ID 트렌드와 분류를 확인하여 다양한 ID 유형이 대상자 내에서 어떻게 연관되는지 이해하고 ID 결합을 강화하며 고객 세분화의 정확성을 개선할 수 있습니다. 자세한 내용은 [대상자 ID 오버랩 안내서](../../dashboards/sql-insights-query-pro-mode/templates/identity-overlaps.md)를 참조하십시오. |

{style="table-layout:auto"}

액세스 권한을 부여하고 사용자 정의 위젯을 만드는 방법을 포함해 대시보드에 대한 자세한 내용은 [대시보드 개요](../../dashboards/home.md)를 읽어 보십시오.

## 데이터 수집 {#collection}

Adobe Experience Platform은 클라이언트측 고객 경험 데이터를 수집하여 Adobe 또는 비 Adobe 대상으로 보강, 변환 및 배포가 가능한 Experience Platform Edge Network로 보낼 수 있는 기술 제품군을 제공합니다.

**새로운 기능**

| 유형 | 기능 | 설명 |
| --- | --- | --- |
| 태그 및 확장 기능 | Adobe Analytics JSON 보기 | 이제 Adobe Analytics 태그 확장 기능을 사용하여 eVar, prop 및 이벤트 설정을 JSON 형식으로 검사할 수 있으며, 이를 Web SDK 확장 기능에 포함하고 편집하도록 내보낼 수 있습니다. 또한 이 데이터를 업로드하거나 복사하여 디바이스에 저장할 수도 있습니다. 자세한 내용은 [Adobe Analytics 확장 기능 설명서](../../tags/extensions/client/analytics/overview.md)를 참조하십시오. |

{style="table-layout:auto"}

자세한 내용은 [데이터 수집 개요](../../collection/home.md)를 참조하십시오.

## 대상 {#destinations}

[!DNL Destinations]는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있는 대상 플랫폼과 사전 설치된 통합입니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타기팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 기능 또는 업데이트된 기능** {#destinations-new-updated-functionality}

| 기능 | 설명 |
| ----------- | ----------- |
| [배열 내보내기 지원을 일반적으로 사용할 수 있습니다.](../../destinations/ui/export-arrays-maps-objects.md) | 이제 모든 고객은 *파일 기반 대상*&#x200B;에 대한 대상자를 활성화할 때 **[!UICONTROL 계산된 필드 추가]** 옵션을 사용하여 배열 전체 또는 요소를 내보낼 수 있습니다. 대상 파일에서 배열을 문자열로 평면화하려면 `array_to_string` 함수를 사용해야 합니다. <br> ![함수와 필드를 사용하여 계산된 필드 선택을 추가합니다.](../2024/assets/october/array-export.gif "array_to_string 함수와 organizations 배열을 선택하여 계산된 필드를 추가합니다."){width="250" align="center" zoomable="yes"} |
| [스트리밍 대상에 대한 보고 정확도 개선](/help/destinations/ui/export-datasets.md) | Adobe는 2024년 10월부터 스트리밍 대상에 대한 보고 정확도를 높이기 위한 업데이트를 출시할 예정입니다. 이러한 개선을 통해 Experience Platform과 대상 플랫폼 보고 간의 정렬이 더욱 향상됩니다. <br> 이 업데이트 이전에는 **[!UICONTROL ID 실패]**&#x200B;에 모든 활성화 재시도가 포함되었습니다. 이 업데이트 이후에는 마지막 활성화 재시도만 총 횟수에 포함됩니다. <br> 이 개선 사항은 현재 [Google 고객 일치 타기팅 대상](../../destinations/catalog/advertising/google-customer-match.md)에만 적용되지만 점차적으로 다른 Experience Platform 스트리밍 대상에도 적용될 예정입니다. 이러한 개선 사항에 따라 [Google 고객 일치 타기팅 대상](../../destinations/catalog/advertising/google-customer-match.md)을 사용하는 사용자에게는 **[!UICONTROL ID 실패]** 수가 감소한 것으로 표시될 수 있습니다. |
| [배치 대상자 활성화](../../destinations/ui/activate-batch-profile-destinations.md#export-full-files)에 대한 유연한 대상자 평가 영향 | 세그먼트 평가 후 이미 활성화되도록 설정된 대상자에 대해 [유연한 대상자 평가](../../segmentation/ui/audience-portal.md#flexible-audience-evaluation)를 실행하는 경우, 이전에 수행한 일일 활성화 작업과 관계없이 유연한 대상자 평가 작업이 완료되는 즉시 대상자가 활성화됩니다. <br> 이로 인해 수행하는 작업에 따라 하루에 여러 번 대상자가 내보내질 수 있습니다. |

{style="table-layout:auto"}

자세한 내용은 [대상 개요](../../destinations/home.md)를 참조하십시오.

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service]는 고객 기반 내에서 마케팅 가능한 사용자 그룹을 구분하는 기준을 설명하여 프로필의 특정 하위 집합을 정의합니다. 세그먼트는 기록 데이터(예: 인구 통계 정보) 또는 고객과 브랜드의 상호 작용을 나타내는 시계열 이벤트를 기반으로 할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| [!BADGE 제한 공개]{type=Informative} 유연한 대상자 평가 | 유연한 대상자 평가를 통해 긴급 커뮤니케이션 요청 시 새로운 대상자를 신속하게 만들 수 있습니다. 이 새 기능에 대한 자세한 내용은 [대상자 포털 설명서](../../segmentation/ui/audience-portal.md#flexible-audience-evaluation)에서 확인할 수 있습니다. |

{style="table-layout:auto"}

[!DNL Segmentation Service]에 대한 자세한 내용은 [세분화 개요](../../segmentation/home.md)를 참조하십시오.

## 샌드박스 {#sandboxes}

Adobe Experience Platform은 전 세계적으로 디지털 체험 애플리케이션을 풍부하게 제공하기 위해 구축되었습니다. 기업은 여러 디지털 경험 애플리케이션을 동시에 실행하는 경우가 많으며, 운영 규정 준수를 보장하면서 이러한 애플리케이션의 개발, 테스트 및 배포를 처리해야 합니다. 이러한 요구 사항을 해결하기 위해 Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 Experience Platform 인스턴스를 별도의 가상 환경으로 분할하는 샌드박스를 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 샌드박스 도구 패키지 공유 | 이제 샌드박스 도구를 사용하여 여러 조직의 샌드박스 간에 샌드박스 구성을 쉽게 내보내고 가져올 수 있습니다. 이제 두 가지 범주의 공유 패키지를 사용할 수 있습니다.<br><ul><li>**[비공개 패키지](../../sandboxes/ui/sharing-packages-across-orgs.md#private-packages):** 소스 조직의 공유 요청을 승인한 조직과 비공개 패키지 공유를 사용합니다.</li><li>**[공개 패키지](../../sandboxes/ui/sharing-packages-across-orgs.md#public-packages):** 공개 패키지는 추가 승인 없이 공유할 수 있으며 패키지의 페이로드를 사용하여 쉽게 가져올 수 있습니다.</li></ul><br>이러한 기능에 대한 자세한 내용은 [조직 간 패키지 공유](../../sandboxes/ui/sharing-packages-across-orgs.md) 안내서를 참조하십시오. |
| 샌드박스 도구 API의 [패키지 공유](https://experienceleague.adobe.com/ko/docs/experience-platform/sandbox/sandbox-tooling-api/packages#org-linking) | 샌드박스 도구 API를 사용하여 패키지 공유 요청을 가져오고, 만들고, 조직 간 공유하기 위한 두 가지 새로운 엔드포인트인 `/handshake` 및 `/transfer`에 대한 요청을 만들 수 있습니다. 패키지의 페이로드를 검색하기 위한 추가 요청이 `/packages` 엔드포인트에 추가되었습니다. |

{style="table-layout:auto"}

샌드박스에 대한 자세한 내용은 [샌드박스 개요](../../sandboxes/home.md)를 참조하십시오.

## 소스 {#sources}

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

Experience Platform의 소스를 사용하여 Adobe 애플리케이션 또는 서드파티 데이터 소스에서 데이터를 수집합니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [!DNL Marketo Engage]의 표준 활동 엔티티 필터링 지원 | [!DNL Marketo Engage] 소스에서 데이터를 수집할 때 [!DNL Flow Service] API를 사용하여 표준 활동 엔티티를 필터링할 수 있습니다. 자세한 내용은 [ [!DNL Marketo] 표준 활동 데이터 필터링](../../sources/tutorials/api/filter.md#filter-activity-entities-for-marketo-engage)에 대한 안내서를 참조하십시오. |

{style="table-layout:auto"}

자세한 내용은 [소스 개요](../../sources/home.md)를 참조하십시오.
