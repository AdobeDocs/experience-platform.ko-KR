---
title: 데이터 신호를 추적하여 고객 라이프타임 값을 생성합니다.
description: 이 안내서에서는 Real-time Customer Data Platform에서 데이터 Distiller 및 사용자 정의 대시보드를 사용하여 고객 라이프타임 값을 측정하고 시각화하는 방법에 대한 엔드 투 엔드 데모를 제공합니다.
source-git-commit: 2346f2d9450bc24e10419c09ee3dbcfb35bd5778
workflow-type: tm+mt
source-wordcount: '1296'
ht-degree: 0%

---

# 데이터 신호를 추적하여 고객 라이프타임 값을 생성합니다

Real-time Customer Data Platform을 사용하여 고객 라이프타임 값(CLV)을 추적하고 사용자 정의 대시보드를 사용하여 해당 지표를 시각화할 수 있습니다. 데이터 Distiller 및 사용자 정의 대시보드를 사용하여 고객 관계의 전체 과정에서 고객이 회사에 얼마나 중요한지 측정할 수 있습니다. CLV를 파악하면 기존 고객을 그대로 유지하고 수익 수익을 유지하면서 신규 고객을 확보할 수 있는 비즈니스 전략을 개발할 수 있습니다.

다음 인포그래픽은 마케팅 캠페인을 개선하기 위해 고성능 데이터를 생성하는 데이터 수집, 조작, 분석 및 작동 주기를 나타냅니다.

![관찰에서 분석까지의 데이터의 라운드 트립 정보.](../images/use-cases/infographic-use-case-cycle.png)

이 엔드 투 엔드 사용 사례는 데이터 신호를 캡처하고 수정하여 고객 라이프타임 값 파생 속성을 계산하는 방법을 보여줍니다. 그런 다음 이러한 파생된 특성을 Real-Time CDP 프로필 데이터에 적용할 수 있으며, 사용자 정의 대시보드에서 사용하여 인사이트 분석을 위한 대시보드를 만들 수 있습니다. Data Distiller을 통해 Real-Time CDP 인사이트 데이터 모델을 확장하고 CLV 파생 속성과 대시보드 인사이트를 사용하여 새 세그먼트를 작성하고 원하는 대상으로 활성화할 수 있습니다. 그런 다음 이러한 세그먼트를 사용하여 고성능 대상을 만들어 다음 마케팅 캠페인을 수행할 수 있습니다.

이 안내서는 CLV를 구동하는 주요 터치포인트 간에 데이터 신호를 측정하고 유사한 사용 사례를 사용자 환경에서 구현하여 고객 경험을 더 잘 이해할 수 있도록 설계되었습니다. 전체 프로세스는 아래 이미지에 요약되어 있습니다.

![고객 라이프타임 값을 활용하는 데 필요한 광범위한 단계의 인포그래피입니다.](../images/use-cases/implementation-steps.png)

## 시작하기 {#getting-started}

이 안내서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [쿼리 서비스](../home.md): SQL 쿼리를 사용하여 데이터를 분석하고 보강할 수 있는 사용자 인터페이스 및 RESTful API를 제공합니다.
* [세분화 서비스](../../segmentation/home.md): 실시간 고객 프로필 데이터에서 세그먼트를 작성하고 대상을 생성할 수 있습니다.

## 사전 요구 사항

이 안내서를 사용하려면 [데이터 Distiller](../data-distiller/overview.md) 패키지 제품의 일부로 SKU를 제공합니다. 이 권한이 있는지 확실하지 않은 경우 Adobe 서비스 담당자에게 문의하십시오.

## 파생 속성 만들기 {#create-derived-attribute}

CLV를 설정하는 첫 번째 단계는 사용자 작업에서 캡처된 데이터 신호로부터 파생된 속성을 만드는 것입니다. 이 특정 사용 사례는 항공 충성도 체계에 대한 별도의 문서에 캡처됩니다. 방법을 알아보려면 안내서를 참조하십시오 [쿼리 서비스를 사용하여 프로필 데이터와 함께 사용할 데이터 기반 파생 특성을 만듭니다](./deciles-use-case.md). 다음 단계를 설명하는 문서에 전체 예와 설명이 제공됩니다.

* 그룹 지정을 위한 스키마를 만듭니다.
* Query Service를 사용하여 ID 파일을 만듭니다.
* 데이터 세트 생성.
* 실시간 고객 프로필에서 사용할 스키마를 사용하도록 설정합니다.
* ID 네임스페이스를 만들어 기본 식별자로 표시합니다.
* 전환 확인 기간 동안 분류를 계산하는 쿼리를 만듭니다.

## 인사이트 데이터 모델 및 업데이트 예약 {#extend-data-model-and-set-refresh-schedule}

그런 다음 CLV 보고 인사이트를 활용하려면 사용자 지정 데이터 모델을 구축하거나 기존 Adobe Real-Time CDP 데이터 모델을 확장해야 합니다. 방법을 알아보려면 설명서 를 참조하십시오. [가속화된 저장소 데이터 및 사용자 정의 대시보드와 함께 사용할 수 있도록 Query Service를 통해 보고 인사이트 데이터 모델을 작성합니다](../data-distiller/query-accelerated-store/reporting-insights-data-model.md#build-a-reporting-insights-data-model). 이 자습서에서는 다음 단계를 다룹니다.

* Data Distiller을 사용하여 보고 인사이트를 위한 모델을 만듭니다.
* 테이블 만들기, 관계 만들기 및 데이터 채우기
* 보고 인사이트 데이터 모델을 질의합니다.
* Real-Time CDP 인사이트 데이터 모델로 데이터 모델을 확장합니다.
* 보고 통찰력 모델을 확장하려면 차원 테이블을 만듭니다.
* 확장 가속 저장소 보고 통찰력 데이터 모델 쿼리

자세한 내용은 Real-time Customer Data Platform 인사이트 데이터 모델 설명서를 참조하십시오 [SQL 쿼리 템플릿을 사용자 지정하여 마케팅 및 KPI(주요 성과 지표) 사용 사례를 위한 Real-Time CDP 보고서를 만들 수 있습니다](../../dashboards/cdp-insights-data-model.md).

정기적으로 사용자 지정 데이터 모델을 새로 고침하기 위한 일정을 설정해야 합니다. 이렇게 하면 데이터가 필요한 경우 수집 파이프라인의 일부로 다시 들어오고 사용자 정의 대시보드를 채웁니다. 자세한 내용은 [쿼리 예약 안내서](../ui/query-schedules.md#create-schedule) 일정을 설정하는 방법을 알아봅니다.

## 통찰력을 캡처할 대시보드 만들기 {#build-a-custom-dashboard}

사용자 지정 데이터 모델을 만들었으므로 이제 사용자 지정 쿼리 및 사용자 정의 대시보드를 사용하여 데이터를 시각화할 준비가 되었습니다. 방법에 대한 전체 지침은 사용자 정의 대시보드 개요 를 참조하십시오. [사용자 지정 대시보드 작성](../../dashboards/user-defined-dashboards.md). UI 안내서에는 다음 사항에 대한 세부 사항이 포함되어 있습니다.

* 위젯을 만드는 방법.
* 위젯 작성기를 사용하는 방법.

아래에 십진수 버킷을 사용하는 사용자 지정 CLV 위젯의 예를 볼 수 있습니다.

![사용자 지정 데코일 기반 CLTV 위젯의 모음입니다.](../images/use-cases/deciles-user-defined-dashboard.png)

## 세그먼트를 만들고 활성화하여 고성능 대상 작성 {#create-and-activate-segments}

다음 단계는 실시간 고객 프로필 데이터에서 세그먼트를 작성하고 대상을 생성하는 것입니다. 자세한 내용은 세그먼트 빌더 UI 안내서 를 참조하십시오 [platform에서 세그먼트 생성 및 활성화](../../segmentation/ui/segment-builder.md). 이 안내서에서는 다음 방법에 대한 섹션을 제공합니다.

* 특성, 이벤트 및 기존 대상을 빌딩 블록으로 조합하여 세그먼트 정의를 만듭니다.
* 규칙 빌더 캔버스 및 컨테이너를 사용하여 세그먼트 규칙이 실행되는 순서를 제어합니다.
* 필요에 따라 세그먼트 정의를 조정할 수 있도록 예상 대상에 대한 예측을 봅니다.
* 예약된 세그먼테이션에 대해 모든 세그먼트 정의를 활성화합니다.
* 스트리밍 세그멘테이션에 지정된 세그먼트 정의를 사용합니다.

또한, [세그먼트 빌더 비디오 튜토리얼](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html) 자세한 내용은 를 참조하십시오.

## 이메일 캠페인용 세그먼트 활성화 {#activate-segment-for-campaign}

세그먼트를 빌드하면 대상으로 활성화할 수 있습니다. 플랫폼에서는 프로모션 이메일 캠페인 전송과 같은 이메일 마케팅 활동을 관리할 수 있는 다양한 ESP(이메일 서비스 공급자)를 지원합니다.

을(를) 확인합니다. [이메일 마케팅 대상 개요](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/email-marketing/overview.html?lang=en#connect-destination) (예: [Oracle 언달라](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/email-marketing/oracle-eloqua-api.html?lang=en) 페이지).

## 캠페인에서 반환된 분석 데이터를 참조하십시오 {#post-campaign-data-analysis}

이제 소스의 데이터는 [증분 처리](../essential-concepts/incremental-load.md) 가속 데이터 저장소에서 데이터 모델에 대한 예약된 새로 고침의 일부로, 고객이 발생할 때 또는 일괄로 고객의 모든 응답 이벤트를 Adobe Experience Platform에 수집할 수 있습니다. 데이터 모델은 설정 또는 소스 커넥터에 따라 한 번 또는 하루에 여러 번 새로 고칠 수 있습니다. 자세한 내용은 [배치 수집 API 개요](../../ingestion/batch-ingestion/api-overview.md) 또는 [스트리밍 수집 개요](../../ingestion/streaming-ingestion/overview.md) 추가 정보.

데이터 모델이 업데이트되면 사용자 지정 대시보드 위젯은 고객 라이프타임 값을 측정하고 시각화할 수 있는 의미 있는 신호를 제공합니다.

![세그먼트 및 이메일 캠페인에 따라 열린 이메일 수를 표시하는 사용자 지정 위젯입니다.](../images/use-cases/post-activation-and-email-response-kpis.png)

사용자 지정 분석을 위해 다양한 시각화 옵션이 제공됩니다.

![캠페인 버킷 위젯에서 연 이메일.](../images/use-cases/email-opened-by-campaign-buckets.png)

이러한 인사이트를 통해 후속 캠페인을 위한 비즈니스 전략을 개발할 수 있습니다.

![이메일 캠페인 결과를 자세히 설명하는 사용자 지정된 4개의 위젯의 모음입니다.](../images/use-cases/example-widgets.png)

## 다음 단계

이 문서를 다 읽으면 Real-time Customer Data Platform을 사용하여 CLV(고객 라이프타임 값) 지표를 추적하고 시각화하는 방법을 보다 잘 이해할 수 있어야 합니다. Query Service 및 Experience Platform을 통해 제공되는 많은 비즈니스 사용 사례에 대해 자세히 알아보려면 다음 문서를 읽는 것이 좋습니다.

* [Query Service의 다기능성과 이점을 보여주는 처음부터 끝까지 중단된 찾아보기 사용 사례 예입니다.](./abandoned-browse.md)
* [Query Service 및 기계 학습을 사용하여 정품 온라인 웹 사이트 방문자 트래픽에서 보트 활동을 확인하고 필터링하는 방법](./bot-filtering.md)
* [선택한 문자열을 대략 일치시켜 여러 데이터 세트의 결과를 결합하는 플랫폼 데이터에 대해 일치 기능을 수행하는 방법입니다.](./fuzzy-match.md)

<!-- "Data signals are actions taken by consumers while online that offer clues about intent that can be acted upon. This includes anything from visiting a website to filling out a change of address or clicking an ad."  -->

<!-- "Customer touchpoints are your brand's points of customer contact, from start to finish." -->
