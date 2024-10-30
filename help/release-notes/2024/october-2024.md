---
title: Adobe Experience Platform 릴리스 노트 2024년 10월
description: Adobe Experience Platform의 2024년 10월 릴리스 정보.
source-git-commit: 5fc786058a187b161a147a8bd361d19c5f35105d
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 34%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 날짜: 2024년 10월 29일**

Adobe Experience Platform의 기존 기능 및 설명서 업데이트:

- [대시보드 {#dashboards}](#dashboards-dashboards)<!-- omit in toc -->
- [데이터 수집 {#collection}](#data-collection-collection)
- [대상 {#destinations}](#destinations-destinations)
- [세분화 서비스 {#segmentation-service}](#segmentation-service-segmentation-service)
- [샌드박스 {#sandboxes}](#sandboxes-sandboxes)
- [소스 {#sources}](#sources-sources)

## 대시보드 {#dashboards}

Experience Platform은 일일 스냅샷 중에 캡처된 조직 데이터에 대한 중요한 인사이트를 볼 수 있는 여러 대시보드를 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 데이터 Distiller 템플릿 | 여러 템플릿을 탐색하여 대상 데이터에 대한 구조화된 통찰력을 얻을 수 있습니다. **고급 [!UICONTROL 대상 중복]**, **[!UICONTROL 대상 비교]**, **[!UICONTROL 대상 트렌드]** 및 **[!UICONTROL 대상 ID 중복]**&#x200B;과 같은 대시보드를 사용하여 데이터 기반 결정을 내리고, 세그먼테이션을 최적화하고, 참여 전략을 향상시킵니다. 자세한 내용은 [데이터 Distiller 템플릿 안내서](../../dashboards/sql-insights-query-pro-mode/templates/overview.md)를 참조하세요. |
| 고급 대상자 오버랩 | 특정 대상에 대한 대상 교차를 빠르게 분석하거나 모든 중복을 확인하여 전체 대상 세트에서 귀중한 통찰력을 찾아냅니다. 이러한 통찰력을 사용하여 세그먼테이션을 세분화하고, 중복 메시지를 줄이고, 더 많은 타겟팅 캠페인을 만들어 마케팅 효율성을 높일 수 있습니다. 자세한 내용은 [고급 대상 중복 가이드](../../dashboards/sql-insights-query-pro-mode/templates/overlaps.md)를 참조하십시오. |
| 대상 비교 개선 사항 | **대상 비교** 대시보드를 사용하여 서로 다른 대상 그룹 간의 주요 지표를 나란히 비교합니다. 이 대시보드를 사용하여 대상 크기 및 ID 구성과 같은 특정 시간대 및 KPI를 선택하여 대상 세분화 및 타기팅 전략에 대해 보다 현명한 결정을 내릴 수 있습니다. 자세한 내용은 [대상 비교 안내서](../../dashboards/sql-insights-query-pro-mode/templates/comparison.md)를 참조하십시오. |
| 대상 트렌드 시각화 | **[!UICONTROL 대상 트렌드]** 대시보드를 사용하여 시간에 따른 대상 지표를 분석합니다. 대상 크기, ID 수 및 단일 ID 프로필 수에 대한 트렌드를 시각화하여 대상 진화를 모니터링하고, 성장을 측정하고, 참여 전략을 구체화하는 데 도움이 됩니다. 자세한 내용은 [대상 트렌드 가이드](../../dashboards/sql-insights-query-pro-mode/templates/trends.md)를 참조하세요. |
| ID 중복 분석 | 선택한 대상에서 ID가 **[!UICONTROL 대상 ID 중복]** 대시보드와 겹치도록 분석합니다. ID 트렌드 및 분류를 보고 다양한 ID 유형이 대상 내에서 어떻게 관련되는지 이해함으로써 ID 결합을 향상시키고 고객 세그멘테이션의 정확도를 향상시킵니다. 자세한 내용은 [대상 ID 중복 가이드](../../dashboards/sql-insights-query-pro-mode/templates/identity-overlaps.md)를 참조하십시오. |

{style="table-layout:auto"}

액세스 권한을 부여하고 사용자 정의 위젯을 만드는 방법을 포함해 대시보드에 대한 자세한 내용은 [대시보드 개요](../../dashboards/home.md)를 읽어 보십시오.

## 데이터 수집 {#collection}

Adobe Experience Platform은 클라이언트측 고객 경험 데이터를 수집하여 Adobe 또는 비 Adobe 대상으로 보강, 변환 및 배포가 가능한 Experience Platform Edge Network로 보낼 수 있는 기술 제품군을 제공합니다.

**새로운 기능**

| 유형 | 기능 | 설명 |
| --- | --- | --- |
| 태그 및 확장 | Adobe Analytics JSON 보기 | 이제 Adobe Analytics 태그 확장 기능을 사용하여 eVar, Prop 및 이벤트 설정을 JSON으로 검사할 수 있습니다. JSON은 이제 Web SDK 확장 기능에 포함되고 편집을 위해 내보낼 수 있습니다. 이 데이터를 업로드하거나 복사하여 디바이스에 저장할 수도 있습니다. 자세한 내용은 [Adobe Analytics 확장 설명서](../../tags/extensions/client/analytics/overview.md)를 참조하십시오. |

{style="table-layout:auto"}

자세한 내용은 [데이터 수집 개요](../../collection/home.md)를 참조하십시오.

## 대상 {#destinations}

[!DNL Destinations]는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있는 대상 플랫폼과 사전 설치된 통합입니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 기능 또는 업데이트된 기능** {#destinations-new-updated-functionality}

| 기능 | 설명 |
| ----------- | ----------- |
| [일반적으로 사용할 수 있는 배열 내보내기 지원](../../destinations/ui/export-arrays-calculated-fields.md) | 이제 모든 고객은 *파일 기반 대상으로*&#x200B;를 활성화하여 전체 배열 또는 배열 요소를 내보낼 때 **[!UICONTROL 계산된 필드 추가]** 옵션을 사용할 수 있습니다. 배열을 대상 파일의 문자열로 병합하려면 `array_to_string` 함수를 사용해야 합니다. <br> ![함수 및 필드가 있는 계산된 필드 선택 항목을 추가합니다.](../2024/assets/october/array-export.gif "array_to_string 함수 및 조직 배열을 선택하여 계산된 필드를 추가합니다."){width="250" align="center" zoomable="yes"} |
| [스트리밍 대상에 대한 보고 정확도 개선](/help/destinations/ui/export-datasets.md) | 2024년 10월부터 Adobe은 스트리밍 대상에 대한 보고 정확도를 높이기 위한 업데이트를 롤아웃합니다. 이러한 향상된 기능을 통해 Experience Platform과 대상 플랫폼 보고 간의 정렬 성능이 향상되었습니다. <br> 이 업데이트 전에 **[!UICONTROL ID 실패]**&#x200B;에 모든 활성화 다시 시도가 포함되었습니다. 이 업데이트 후에는 마지막 활성화 재시도만 총 횟수에 포함됩니다. <br> 이 개선 사항은 현재 [Google Customer Match 대상](../../destinations/catalog/advertising/google-customer-match.md)에 적용되지만 다른 Experience Platform 스트리밍 대상으로 점진적으로 롤아웃됩니다. 이 개선 사항에 따라 [Google 고객 일치 대상](../../destinations/catalog/advertising/google-customer-match.md)의 사용자는 **[!UICONTROL ID 실패]** 수가 예상대로 감소할 수 있습니다. |
| [일괄 대상 활성화](../../destinations/ui/activate-batch-profile-destinations.md#export-full-files)에 대한 유연한 대상 평가 영향 | 세그먼트 평가 후 이미 활성화되도록 설정된 대상에 대해 [유연한 대상 평가](../../segmentation/ui/audience-portal.md#flexible-audience-evaluation)를 실행하면 이전의 모든 일일 활성화 작업에 관계없이 유연한 대상 평가 작업이 완료되는 즉시 대상이 활성화됩니다. <br> 이로 인해 사용자의 작업에 따라 대상을 하루에 여러 번 내보낼 수 있습니다. |

{style="table-layout:auto"}

자세한 내용은 [대상 개요](../../destinations/home.md)를 참조하십시오.

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service]는 고객 기반 내에서 마케팅 가능한 사용자 그룹을 구분하는 기준을 설명하여 프로필의 특정 하위 집합을 정의합니다. 세그먼트는 기록 데이터(예: 인구 통계 정보) 또는 고객과 브랜드의 상호 작용을 나타내는 시계열 이벤트를 기반으로 할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| [!BADGE 제한된 가용성]{type=Informative} 유연한 대상 평가 | 유연한 대상 평가를 통해 시간에 민감한 커뮤니케이션에 대한 요청에 따라 새로운 대상을 신속하게 만들 수 있습니다. 이 새 기능에 대한 자세한 내용은 [Audience Portal 설명서](../../segmentation/ui/audience-portal.md#flexible-audience-evaluation)에서 확인할 수 있습니다. |

{style="table-layout:auto"}

[!DNL Segmentation Service]에 대한 자세한 내용은 [세분화 개요](../../segmentation/home.md)를 참조하십시오.

## 샌드박스 {#sandboxes}

Adobe Experience Platform은 전 세계적으로 디지털 체험 애플리케이션을 풍부하게 제공하기 위해 구축되었습니다. 기업은 여러 디지털 경험 애플리케이션을 동시에 실행하는 경우가 많으며, 운영 규정 준수를 보장하면서 이러한 애플리케이션의 개발, 테스트 및 배포를 처리해야 합니다. 이러한 필요를 처리하기 위해 Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 샌드박스를 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 샌드박스 도구 패키지 공유 | 이제 샌드박스 도구 를 사용하여 여러 조직의 샌드박스 간에 샌드박스 구성을 쉽게 내보내고 가져올 수 있습니다. 이제 두 가지 범주의 공유 패키지를 사용할 수 있습니다. <br><ul><li>**[비공개 패키지](../../sandboxes/ui/sharing-packages-across-orgs.md#private-packages):** 원본 조직의 공유 요청을 승인한 조직과 비공개 패키지 공유를 사용합니다.</li><li>**[공용 패키지](../../sandboxes/ui/sharing-packages-across-orgs.md#public-packages):** 공용 패키지는 추가 승인 없이 공유할 수 있으며 패키지의 페이로드를 사용하여 쉽게 가져올 수 있습니다.</li></ul><br>이러한 기능에 대한 자세한 내용은 [조직 간 패키지 공유](../../sandboxes/ui/sharing-packages-across-orgs.md)에 대한 안내서를 참조하십시오. |
| 샌드박스 도구 API의 [패키지 공유](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/sandbox-tooling-api/packages#org-linking) | 샌드박스 도구 API를 사용하여 조직 간 공유, 가져오기 및 패키지 공유 요청 생성을 위해 두 개의 새 엔드포인트 `/handshake` 및 `/transfer`에 대한 요청을 만듭니다. 패키지의 페이로드를 검색하기 위해 `/packages` 끝점에 요청이 추가되었습니다. |

{style="table-layout:auto"}

샌드박스에 대한 자세한 내용은 [샌드박스 개요](../../sandboxes/home.md)를 참조하십시오.

## 소스 {#sources}

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

Experience Platform의 소스를 사용하여 Adobe 애플리케이션 또는 서드파티 데이터 소스에서 데이터를 수집합니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [!DNL Marketo Engage]에서 표준 활동 엔터티 필터링 지원 | [!DNL Marketo Engage] 원본에서 데이터를 수집할 때 [!DNL Flow Service] API를 사용하여 표준 활동 엔터티를 필터링할 수 있습니다. 자세한 내용은 [필터링 [!DNL Marketo] 표준 활동 데이터](../../sources/tutorials/api/filter.md#filter-activity-entities-for-marketo-engage)에 대한 안내서를 참조하십시오. |

{style="table-layout:auto"}

자세한 내용은 [소스 개요](../../sources/home.md)를 참조하십시오.
