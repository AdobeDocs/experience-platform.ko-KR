---
title: Adobe Experience Platform 릴리스 노트 2023년 10월
description: Adobe Experience Platform의 2023년 10월 릴리스 정보입니다.
exl-id: e9cf5299-8350-4b40-8f56-05e598846875
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1057'
ht-degree: 37%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 일자: 2023년 10월 25일 목요일**

Experience Platform의 기존 기능 업데이트:

- [대시보드](#dashboards)
- [데이터 수집](#data-collection)
- [대상](#destinations)
- [샌드박스](#sandboxes)
- [Segmentation Service](#segmentation)
- [소스](#sources)

## 대시보드 {#dashboards}

Adobe Experience Platform은 일일 스냅샷 중에 캡처된 조직 데이터에 대한 중요한 인사이트를 볼 수 있는 여러 대시보드를 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 대상 사용 지표 | 새 계량 지표가 라이선스 사용 대시보드에 추가되었습니다. **[!UICONTROL Audience Activation 크기]** 및 **[!UICONTROL 데이터 내보내기 크기]** 지표를 사용하면 라이선스 사용 권한과 관련하여 Experience Platform에서 내보낸 데이터의 양을 추적할 수 있습니다. 이러한 지표 및 기타 라이선스 사용 지표에 대한 설명은 [사용 가능한 지표](../../dashboards/guides/license-usage.md#available-metrics) 설명서를 참조하십시오. |

{style="table-layout:auto"}

액세스 권한을 부여하고 사용자 정의 위젯을 만드는 방법을 포함해 대시보드에 대한 자세한 내용은 [대시보드 개요](../../dashboards/home.md)를 읽어 보십시오.

## 데이터 수집 {#data-collection}

Adobe Experience Platform은 클라이언트측 고객 경험 데이터를 수집하여 Adobe 또는 비 Adobe 대상으로 보강, 변환 및 배포가 가능한 Adobe Experience Platform Edge Network로 보낼 수 있는 기술 제품군을 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 유형 | 기능 | 설명 |
| --- | --- | --- |
| 확장 | [!DNL Meta] 전환 API 개선 사항 | [메타 전환 API](/help/tags/extensions/server/meta/overview.md) 확장에 대한 세 가지 개선 사항이 있습니다. <ul><li>[[!DNL Meta Business Extension (MBE)]](/help/tags/extensions/server/meta/overview.md#integration-with-meta-business-extension-mbe)과(와) 통합: Adobe과의 전환 API 통합을 위해 pixelID 및 액세스 토큰을 공유할 수 있도록 하여 원활한 로그인 환경을 만듭니다.</li><li>[[!DNL Event Match Quality Score (EMQ)]](/help/tags/extensions/server/meta/overview.md#integration-with-event-quality-match-score-emq)과(와) 통합: 원하는 작업을 완료할 가능성이 높은 사람에게 광고를 게재하고 작업을 게재된 광고에 다시 연결할 수 있습니다.</li><li>[[!DNL LiveRamp (Alpha)]](/help/tags/extensions/server/meta/overview.md#integration-with-liveramp-alpha)과(와) 통합: CIP 필드에 LiveRamp의 RampID를 전달할 수 있으므로 파트너 또는 메타와 직접 PII를 공유할 필요가 없습니다. </li></ul> |
| 확장 | [!DNL LinkedIn] 전환 API | [[!DNL LinkedIn] 전환 API](../../tags/extensions/server/linkedin/overview.md) 확장을 사용하면 Experience Platform 이벤트 데이터를 LinkedIn으로 전달하여 LinkedIn 마케팅 캠페인의 효과를 평가할 수 있습니다. |
| Secret | [!DNL LinkedIn] OAuth 2 암호 | [[!DNL LinkedIn] OAuth 2 암호](../../tags/ui/event-forwarding/secrets.md#linkedin-oauth-2)를 사용하면 이벤트 전달 시 서버-서버 상호 작용을 [!DNL LinkedIn]에 보낼 수 있습니다. |
| 이벤트 전달 | 태그 및 이벤트 전달 업데이트 | Experience Platform에서 [Tags](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=ko) 및 [Event Forwarding](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=ko) 성능을 유지하기 위해 성공 및 실패한 가장 최근 개발 및 단계 빌드만 유지됩니다. 더 이상 사용되지 않는 모든 빌드는 제거됩니다. 또한 제한과 속도 제한은 API를 많이 사용하는 몇 가지가 다른 사용자의 API 성능을 저하시키지 않도록 구현되었습니다. |
| 확장 | 요소, 규칙 및 확장 | [요소, 규칙 및 확장](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/overview.html?lang=ko)이(가) 이제 라이브러리 출력에서 정렬되어 동일한 라이브러리의 여러 빌드와 배포 간에 더 일관성을 유지할 수 있습니다. |

데이터 수집에 대한 자세한 내용은 [데이터 수집 개요](../../tags/home.md)를 참조하십시오.

## 대상 {#destinations}

[!DNL Destinations]는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있는 대상 플랫폼과 사전 설치된 통합입니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타기팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 대상 또는 업데이트된 대상** {#new-updated-destinations}

| 대상 | 새로운 기능 또는 업데이트된 기능 | 설명 |
| ----------- |----------------|----------- |
| [[!DNL MoEngage]](/help/destinations/catalog/mobile-engagement/moengage.md) | 새로운 기능 | Moengage 대상을 사용하여 Adobe 데이터(사용자 특성, 세그먼트 및 이벤트)를 MoEngage에 실시간으로 연결하고 매핑합니다. 그런 다음 고객은 이 데이터에 따라 행동하여 개인화되고 타겟팅된 경험을 제공할 수 있습니다. |
| [[!DNL Qualtrics Automations]](/help/destinations/catalog/survey/qualtrics-automations.md) | 새로운 기능 | Adobe Experience Platform의 여러 운영 데이터 소스 합계를 Qualtrics Experience ID의 입력으로 사용하여 고객을 더 잘 이해하고 의도, 감정 및 경험 드라이버를 이해하는 데 있어 타깃팅된 전달을 통해 간격을 좁힐 수 있습니다. |

{style="table-layout:auto"}

**새로운 기능 또는 업데이트된 기능** {#destinations-new-updated-functionality}

| 기능 | 설명 |
| ----------- | ----------- |
| (Beta) 계산된 필드에서 함수 해싱 지원 | 이제 [배열 내보내기](../../destinations/ui/export-arrays-maps-objects.md) 또는 배열에서 요소에 대한 특정 함수 외에 추가 [해시 함수](../../destinations/ui/export-arrays-maps-objects.md#hashing-functions)를 사용하여 내보낸 파일의 특성을 해시할 수 있습니다. 지원되는 해시 함수는 `sha`, `sha256`, `sha512`, `hash`, `md5`, `crc32`입니다. |
| (제한된 GA) 특정 대상에 대해 계정 대상자 활성화 | Real-Time CDP B2B 고객은 이제 특정 대상에 대해 [계정 대상자](../../segmentation/types/account-audiences.md)를 활성화할 수 있습니다. 이 기능에 대한 자세한 내용은 [계정 대상자 활성화 자습서](/help/destinations/ui/activate-account-audiences.md)를 참조하십시오. |

{style="table-layout:auto"}

**수정 사항 및 개선 사항** {#destinations-fixes-and-enhancements}

대상에 대한 일반적인 정보는 [대상 개요](../../destinations/home.md)를 참조하십시오.

## 샌드박스 {#sandboxes}

Adobe Experience Platform은 전 세계적으로 디지털 체험 애플리케이션을 풍부하게 제공하기 위해 구축되었습니다. 기업은 여러 디지털 경험 애플리케이션을 동시에 실행하는 경우가 많으며, 운영 규정 준수를 보장하면서 이러한 애플리케이션의 개발, 테스트 및 배포를 처리해야 합니다. 이러한 요구 사항을 해결하기 위해 Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 Experience Platform 인스턴스를 별도의 가상 환경으로 분할하는 샌드박스를 제공합니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 샌드박스 도구 | 샌드박스 도구 기능을 사용하면 샌드박스 간 구성 정확도를 높이고 샌드박스 간에 샌드박스 구성을 원활하게 내보내고 가져올 수 있습니다. 샌드박스 도구 기능을 사용하여 다른 개체를 선택하고 패키지로 내보낼 수 있습니다. 자세한 내용은 [샌드박스 도구 UI 안내서](../../sandboxes/ui/sandbox-tooling.md)를 참조하십시오. |

샌드박스에 대한 자세한 내용은 [샌드박스 개요](../../sandboxes/home.md)를 참조하십시오.

## Segmentation Service {#segmentation}

[!DNL Segmentation Service]를 사용하여 개인 사용자(예: 고객, 잠재 고객, 사용자 또는 조직)와 관련된 [!DNL Experience Platform]에 저장된 데이터를 대상자로 세분화할 수 있습니다. 세그먼트 정의 또는 [!DNL Real-Time Customer Profile] 데이터의 다른 소스를 통해 대상자를 만들 수 있습니다. 이러한 대상자는 [!DNL Experience Platform]을 통해 중앙 집중식으로 구성 및 유지 관리되고 모든 Adobe 솔루션에서 쉽게 액세스할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 계정 대상자 (제한된 GA) | 이제 Real-Time Customer Data Platform B2B edition에서 계정 세분화를 사용하여 사람 기반 대상에서 계정 기반 대상으로의 마케팅 세분화 경험을 전체적으로 쉽고 정교하게 할 수 있습니다. 이 기능에 대한 자세한 내용은 [계정 대상자 개요](../../segmentation/types/account-audiences.md)를 참조하십시오. |

세분화 서비스에 대한 자세한 내용은 [세분화 서비스 개요](../../segmentation/home.md)를 참조하세요.

## 소스 {#sources}

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 업데이트된 데이터 랜딩 영역 인증 | 이제 자격 증명을 볼 때 데이터 랜딩 영역의 지정된 만료 날짜를 볼 수 있습니다. 애플리케이션에서 토큰을 계속 사용하려면 만료일 전에 토큰을 새로 고쳐야 합니다. 명시된 만료 날짜 이전에 토큰을 수동으로 새로 고치지 않는 경우, 다음에 자격 증명을 검색할 때 자동으로 새로 고침되고 새 토큰을 제공합니다. 자세한 내용은 [데이터 랜딩 영역 사용](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md)에 대한 설명서를 참조하세요. |

{style="table-layout:auto"}

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md)를 읽어 보십시오.
