---
title: Adobe Experience Platform 릴리스 정보 2024년 11월
description: Adobe Experience Platform의 2024년 11월 릴리스 정보입니다.
exl-id: e3969f8b-70b2-40f8-bb9b-5be6e3d8f722
source-git-commit: f71fc1d4ad51af52046caeee289546e05967d5bd
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 98%

---

# Adobe Experience Platform 릴리스 정보

>[!TIP]
>
>이제 새로운 [AI Assistant 제품 설명서](../../ai-assistant/landing.md)를 사용할 수 있습니다. 이 페이지를 모든 AI 어시스턴트 관련 리소스의 허브로 사용해 보십시오.

**릴리스 날짜: 2024년 11월 26일**

Adobe Experience Platform의 기존 기능 및 설명서 업데이트:

- [AI 어시스턴트](#ai-assistant)
- [대상](#destinations)
- [쿼리 서비스](#query-service)
- [샌드박스](#sandboxes)
- [설명서 업데이트](#documentation-updates)
   - [대화형 Experience Platform API 설명서](#interactive-experience-platform-api-documentation)
   - [Experience League의 새로운 목차](#new-table-of-contents-on-experience-league)
   - [새 AI 어시스턴트 랜딩 페이지](#new-ai-assistant-landing-page)

## AI 어시스턴트 {#ai-assistant}

Adobe Experience Platform의 AI 어시스턴트는 Adobe 애플리케이션에서 워크플로를 가속화하는 데 사용할 수 있는 대화형 환경입니다. AI 어시스턴트를 사용하여 제품 지식을 더 잘 이해하고, 문제를 해결하거나, 정보를 검색하여 운영 인사이트를 얻을 수 있습니다. AI 어시스턴트는 Experience Platform, Real-Time CDP, Adobe Journey Optimizer 및 Customer Journey Analytics를 지원합니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| [!BADGE 알파]{type=Informative} 중요한 변화 모니터링 및 대상자 성장 예측 | AI 어시스턴트를 사용하여 중요한 변경 사항을 모니터링하고 대상자 및 데이터 세트 규모에 대한 성장 예측을 제공합니다. 그런 다음 이 정보를 사용하여 대상자 데이터의 무결성을 보장하고 미래 예측을 제공하여 데이터에 기반한 의사 결정을 지원할 수 있습니다. 자세한 내용은 [중요한 변화 모니터링 및 대상자 성장 예측](../../ai-assistant/new-features/audience-forecasting.md)에 관한 안내서를 읽어 보십시오. |
| [!BADGE 알파]{type=Informative} 자연어 추정 | AI 어시스턴트의 자연어 추정 기능을 사용하여 간단한 대화형 질문을 기반으로 대상자 규모를 추정하고 대상자 성향을 예측합니다. 자세한 내용은 [AI 어시스턴트로 자연어 추정 사용](../../ai-assistant/new-features/natural-language.md)에 대한 안내서를 읽어 보십시오. |

{style="table-layout:auto"}

## 대상 {#destinations}

[!DNL Destinations]는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있는 대상 플랫폼과 사전 설치된 통합입니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타기팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 대상 또는 업데이트된 대상** {#new-updated-destinations}

| 대상 | 설명 |
| --- | --- |
| [Magnite 스트리밍 실시간](/help/destinations/catalog/advertising/magnite-streaming.md) | Magnite 스트리밍 플랫폼에서 활성화, 타기팅 또는 억제를 위해 대상자를 내보냅니다. 대상자를 Magnite로 올바르게 내보내려면 실시간 대상과 배치 대상을 모두 사용해야 합니다. |
| [Magnite 스트리밍 배치](/help/destinations/catalog/advertising/magnite-batch.md) | Magnite 스트리밍 플랫폼에서 활성화, 타기팅 또는 억제를 위해 대상자를 내보냅니다. 대상자를 Magnite로 올바르게 내보내려면 실시간 대상과 배치 대상을 모두 사용해야 합니다. |

{style="table-layout:auto"}

**새로운 기능 또는 업데이트된 기능** {#destinations-new-updated-functionality}

| 기능 | 설명 |
| --- | --- |
| [Edge에서 실시간으로 프로필 속성 조회](/help/destinations/ui/activate-edge-profile-lookup.md) | 사용자 정의 개인화 대상 및 Edge Network API를 사용하여 다운스트림 애플리케이션을 통해 개인화 경험을 제공하거나 의사 결정 규칙을 알리기 위해 실시간으로 Edge 프로필 속성을 조회하는 방법을 알아봅니다. |

{style="table-layout:auto"}

자세한 내용은 [대상 개요](../../destinations/home.md)를 참조하십시오.

## 쿼리 서비스 {#query-service}

쿼리 서비스가 포함된 표준 SQL을 사용하여 Adobe Experience Platform 데이터 레이크에서 데이터를 쿼리합니다. 데이터 세트를 원활하게 결합하고 쿼리 결과에서 새로운 데이터 세트를 생성하여 보고를 강화하고, 데이터 과학 워크플로를 활성화하거나, 실시간 고객 프로필로 수집할 수 있습니다. 예를 들어 고객 거래 데이터와 행동 데이터를 병합하여 타기팅된 마케팅 캠페인의 가치가 높은 대상자를 파악할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| Dater Distiller 인증 API | 쿼리 서비스 샌드박스에 대한 IP 기반 액세스 제한을 관리하고 적용하여 데이터 보안을 강화하고 조직 정책을 준수하도록 합니다. 주요 특징과 기능에 대한 자세한 내용은 [Data Distiller 인증 API 안내서](../../query-service/auth-api/overview.md)를 참조하거나, 엔드포인트 세부 정보, 매개변수 목록, 요청/응답 예제 및 테스트 기능을 포함한 포괄적인 정보는 [OpenAPI 설명서](https://developer.adobe.com/experience-platform-apis/references/data-distiller-auth/)를 참조하십시오. |

[!DNL Query Service]에 대한 자세한 내용은 [[!DNL Query Service] 개요](../../query-service/home.md)를 참조하십시오.

## 샌드박스 {#sandboxes}

Adobe Experience Platform은 전 세계적으로 디지털 체험 애플리케이션을 풍부하게 제공하기 위해 구축되었습니다. 기업은 여러 디지털 경험 애플리케이션을 동시에 실행하는 경우가 많으며, 운영 규정 준수를 보장하면서 이러한 애플리케이션의 개발, 테스트 및 배포를 처리해야 합니다. 이러한 필요를 처리하기 위해 Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 샌드박스를 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 샌드박스 도구 API와 패키지 공유 | 샌드박스 도구 API를 사용하여 요청 승인, 패키지 가시성, 패키지 가져오기 등 조직 전반의 패키지 공유를 처리하려면 두 개의 새로운 API 엔드포인트인 [`/handshake`](../../sandboxes/sandbox-tooling-api/packages.md#org-linking) 및 [`/transfers`](../../sandboxes/sandbox-tooling-api/packages.md#transfer-packages)을 사용합니다. |

샌드박스에 대한 자세한 내용은 [샌드박스 개요](../../sandboxes/home.md)를 참조하십시오.

## 설명서 업데이트 {#documentation-updates}

### 대화형 Experience Platform API 설명서 {#interactive-api-documentation}

이제 [Experience Platform API 설명서](https://developer.adobe.com/experience-platform-apis/)가 완전히 대화형으로 제공되므로 API 참조 설명서 페이지에서 직접 API를 인증하고 탐색할 수 있습니다. 이제 원하는 API 참조 설명서 페이지로 이동하여 API 인증 자격 증명을 만들거나 가져와 **[!UICONTROL 사용해 보기]** 블록에 붙여넣고 호출을 실행할 수 있습니다. 한 페이지에서 모두 가능합니다. 기능에 대해 [자세히 알아보십시오](/help/landing/api-authentication.md#get-credentials-functionality).

### Experience League의 새로운 목차 {#new-table-of-contents-on-experience-league}

필요한 정확한 페이지를 검색할 수 있는 키워드 필터, 모든 페이지 확장 기능 등 독자에게 더 나은 경험을 제공하기 위해 Experience League 설명서 페이지의 목차가 개선되었습니다. <br> ![키워드 필터와 모든 페이지 확장 기능을 포함한 새로운 목차 환경.](../2024/assets/november/new-toc-experience.gif "키워드 필터와 모든 페이지 확장 기능을 포함한 새로운 목차 환경."){width="250" align="center" zoomable="yes"}

### 새 AI 어시스턴트 랜딩 페이지 {#new-ai-assistant-landing-page}

새로운 [AI 어시스턴트 제품 설명서](../../ai-assistant/landing.md) 페이지를 AI 어시스턴트에 대한 허브로 사용할 수 있습니다. AI 어시스턴트에 관한 비디오 튜토리얼, 기술 문서, 사용 사례 및 블로그 게시물 링크는 제품 설명서를 참조하십시오.
