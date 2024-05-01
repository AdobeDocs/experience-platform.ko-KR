---
title: 데이터 신호를 추적하여 고객 생애 가치 생성
description: 이 안내서에서는 Data Distiller 및 Real-time Customer Data Platform과 함께 사용자 정의 대시보드를 사용하여 고객 생애 가치를 측정하고 시각화하는 방법에 대한 전체적인 데모를 제공합니다.
exl-id: c74b5bff-feb2-4e21-9ee4-1e0973192570
source-git-commit: e0af1f0110ceb514a5b249c42a05bf780ea834c6
workflow-type: tm+mt
source-wordcount: '1263'
ht-degree: 0%

---

# 데이터 신호를 추적하여 고객 생애 가치 생성

Real-time Customer Data Platform을 사용하여 고객 생애 가치(CLV)를 추적하고 사용자 정의 대시보드를 사용하여 해당 지표를 시각화할 수 있습니다. Data Distiller 및 사용자 정의 대시보드를 사용하여 전체 관계에서 고객이 회사에 얼마나 중요한지 측정할 수 있습니다. CLV를 알면 기존 고객을 유지하고 이윤을 유지하면서 새로운 고객을 확보하기 위한 비즈니스 전략을 개발하는 데 도움이 될 수 있습니다.

다음 인포그래픽은 마케팅 캠페인을 개선하기 위해 고성능 데이터를 생성하는 데이터 수집, 조작, 분석 및 작동 주기를 보여 줍니다.

![관찰에서 분석, 실행에 이르기까지 데이터의 왕복 인포그래픽입니다.](../images/use-cases/infographic-use-case-cycle.png)

이 엔드 투 엔드 사용 사례는 고객 라이프타임 값 파생 특성을 계산하기 위해 데이터 신호를 캡처하고 수정하는 방법을 보여 줍니다. 그런 다음 이러한 파생된 데이터 세트를 Real-Time CDP 프로필 데이터에 적용하고 인사이트 분석을 위한 대시보드를 빌드하는 사용자 정의 대시보드와 함께 사용할 수 있습니다. Data Distiller을 통해 Real-Time CDP 인사이트 데이터 모델을 확장하고 CLV 파생 데이터 세트 및 대시보드 인사이트를 사용하여 새 대상을 구축하고 원하는 대상으로 활성화할 수 있습니다. 그런 다음 이러한 고성능 대상을 사용하여 다음 마케팅 캠페인을 강화할 수 있습니다.

이 안내서는 CLV를 구동하는 주요 접점에서 데이터 신호를 측정하여 고객 경험을 더 잘 이해하고 환경에서 유사한 사용 사례를 구현하는 데 도움이 되도록 설계되었습니다. 전체 프로세스는 아래 이미지에 요약되어 있습니다.

![고객 생애 가치를 활용하는 데 필요한 광범위한 단계에 대한 인포그래픽입니다.](../images/use-cases/implementation-steps.png)

## 시작하기 {#getting-started}

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 잘 알고 있어야 합니다.

* [쿼리 서비스](../home.md): SQL 쿼리를 사용하여 데이터를 분석하고 보강할 수 있는 사용자 인터페이스와 RESTful API를 제공합니다.
* [세분화 서비스](../../segmentation/home.md): 실시간 고객 프로필 데이터에서 대상자를 생성할 수 있습니다.

## 전제 조건

이 안내서에서는 다음을 수행해야 합니다. [데이터 Distiller](../data-distiller/overview.md) 패키지 제품의 일부인 SKU입니다. 이러한 권한이 있는지 확실하지 않은 경우 Adobe 서비스 담당자에게 문의하십시오.

## 파생 데이터 세트 만들기 {#create-derived-dataset}

CLV를 설정하는 첫 번째 단계는 사용자 작업에서 캡처한 데이터 신호로부터 파생된 데이터 세트를 만드는 것입니다. 이 특정 사용 사례는 항공사 충성도 체계에 대한 별도의 문서에 캡처되어 있습니다. 방법을 알아보려면 안내서 참조 [쿼리 서비스를 사용하여 프로필 데이터에 사용할 십분위수 기반 파생 데이터 세트를 만드십시오](./deciles-use-case.md). 다음 단계를 설명하는 문서에 전체 예제와 설명이 제공됩니다.

* 십분위수 버킷팅을 허용하는 스키마를 만듭니다.
* 쿼리 서비스를 사용하여 십분위수를 만듭니다.
* 십분위수 데이터 세트를 생성합니다.
* 실시간 고객 프로필에서 사용할 스키마를 활성화합니다.
* ID 네임스페이스를 만들고 기본 식별자로 표시합니다.
* 전환 확인 기간 동안 십분위수를 계산하는 쿼리를 만듭니다.

## Insights 데이터 모델 확장 및 업데이트 예약 {#extend-data-model-and-set-refresh-schedule}

그런 다음 사용자 지정 데이터 모델을 구축하거나 기존 Adobe Real-Time CDP 데이터 모델을 확장하여 CLV 보고 통찰력에 참여해야 합니다. 방법을 알아보려면 설명서 를 참조하십시오 [가속화된 저장소 데이터 및 사용자 정의 대시보드와 함께 사용할 수 있도록 쿼리 서비스를 통해 보고 통찰력 데이터 모델을 구축합니다](../data-distiller/customizable-insights/reporting-insights-data-model.md#build-a-reporting-insights-data-model). 이 자습서에서는 다음 단계를 다룹니다.

* Data Distiller을 사용하여 보고 통찰력에 대한 모델을 만듭니다.
* 테이블, 관계를 만들고 데이터를 채웁니다.
* 보고 인사이트 데이터 모델을 쿼리합니다.
* Real-Time CDP 통찰력 데이터 모델을 사용하여 데이터 모델을 확장합니다.
* 차원 테이블을 생성하여 보고 통찰력 모델을 확장합니다.
* 확장 가속 저장소 보고 통찰력 데이터 모델 쿼리

다음 방법에 대해 알아보려면 Real-time Customer Data Platform 통찰력 데이터 모델 설명서 를 참조하십시오 [sql 쿼리 템플릿을 사용자 정의하여 마케팅 및 KPI(주요 성능 지표) 사용 사례에 대한 Real-Time CDP 보고서를 생성합니다.](../../dashboards/data-models/cdp-insights-data-model-b2c.md).

정기적으로 사용자 지정 데이터 모델을 새로 고치도록 일정을 설정해야 합니다. 이렇게 하면 데이터가 필요에 따라 수집 파이프라인의 일부로 다시 들어오고 사용자 정의 대시보드가 채워집니다. 다음을 참조하십시오. [일정 쿼리 안내서](../ui/query-schedules.md#create-schedule) 을(를) 사용하여 일정을 설정하는 방법을 알아보십시오.

## 통찰력을 캡처할 대시보드 구축 {#build-a-custom-dashboard}

사용자 정의 데이터 모델을 만들었으므로 이제 사용자 정의 쿼리 및 사용자 정의 대시보드를 사용하여 데이터를 시각화할 준비가 되었습니다. 방법에 대한 전체 지침은 사용자 정의 대시보드 개요 를 참조하십시오. [사용자 지정 대시보드 작성](../../dashboards/user-defined-dashboards.md). UI 안내서에는 다음에 대한 세부 사항이 포함되어 있습니다.

* 위젯을 만드는 방법.
* 위젯 작성기를 사용하는 방법.

십분위수 버킷을 사용하는 사용자 정의 CLV 위젯의 예는 아래에서 볼 수 있습니다.

![사용자 지정 십분위수 기반 CLTV 위젯의 컬렉션입니다.](../images/use-cases/deciles-user-defined-dashboard.png)

## 고성능 대상자 만들기 및 활성화 {#create-and-activate-audiences}

다음 단계는 세그먼트 정의를 작성하고 실시간 고객 프로필 데이터에서 대상을 생성하는 것입니다. 자세한 내용은 세그먼트 빌더 UI 안내서 를 참조하십시오 [Platform에서 대상자 만들기 및 활성화](../../segmentation/ui/segment-builder.md). 이 안내서에서는 다음 방법에 대한 섹션을 제공합니다.

* 속성, 이벤트 및 기존 대상의 조합을 빌딩 블록으로 사용하여 세그먼트 정의를 만듭니다.
* 규칙 빌더 캔버스 및 컨테이너를 사용하여 세그먼테이션 규칙이 실행되는 순서를 제어합니다.
* 예상 대상의 예상치를 보고 필요에 따라 세그먼트 정의를 조정할 수 있습니다.
* 예약된 세분화에 대해 모든 세그먼트 정의를 활성화합니다.
* 스트리밍 세분화에 대해 지정된 세그먼트 정의를 활성화합니다.

또는 다음 항목도 있습니다 [세그먼트 빌더 비디오 튜토리얼](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-segments.html) 을 참조하십시오.

## 이메일 캠페인에 대한 대상자 활성화 {#activate-audience-for-campaign}

대상을 빌드했으면 대상에 대해 활성화할 준비가 된 것입니다. Platform은 프로모션 이메일 캠페인 전송과 같은 이메일 마케팅 활동을 관리할 수 있도록 해주는 다양한 이메일 서비스 공급자(ESP)를 지원합니다.

다음 확인: [이메일 마케팅 대상 개요](../../destinations/catalog/email-marketing/overview.md#connect-destination) 데이터를 내보내려는 지원되는 대상 목록(예: [Oracle Eloqua](../../destinations/catalog/email-marketing/oracle-eloqua-api.md) page).

## 캠페인에서 반환된 분석 데이터를 확인합니다 {#post-campaign-data-analysis}

이제 소스의 데이터는 다음과 같을 수 있습니다 [증분 처리됨](../key-concepts/incremental-load.md) 가속화된 데이터 저장소에서 데이터 모델에 대한 예약된 새로 고침의 일부로. 고객의 모든 응답 이벤트는 발생 시 또는 일괄적으로 Adobe Experience Platform에 수집될 수 있습니다. 데이터 모델은 설정 또는 소스 커넥터에 따라 하루에 한 번 또는 여러 번 새로 고쳐질 수 있습니다. 다음을 참조하십시오. [일괄 처리 수집 API 개요](../../ingestion/batch-ingestion/api-overview.md) 또는 [스트리밍 수집 개요](../../ingestion/streaming-ingestion/overview.md) 추가 정보.

데이터 모델이 업데이트되면 사용자 정의 대시보드 위젯은 고객 생애 가치를 측정하고 시각화할 수 있는 의미 있는 신호를 제공합니다.

![대상자 및 이메일 캠페인에 따라 열린 이메일 수를 표시하는 사용자 지정 위젯.](../images/use-cases/post-activation-and-email-response-kpis.png)

사용자 정의 분석을 위한 다양한 시각화 옵션이 제공됩니다.

![캠페인 버킷 위젯에서 연 이메일.](../images/use-cases/email-opened-by-campaign-buckets.png)

이러한 통찰력은 결과적으로 후속 캠페인에 대한 비즈니스 전략을 개발하는 데 도움이 될 수 있습니다.

![이메일 캠페인 결과를 자세히 설명하는 4가지 사용자 정의 위젯의 컬렉션입니다.](../images/use-cases/example-widgets.png)

## 다음 단계

이 문서를 읽은 후에는 Real-time Customer Data Platform을 사용하여 고객 생애 가치(CLV) 지표를 추적하고 시각화하는 방법을 더 잘 이해할 수 있어야 합니다. 쿼리 서비스 및 Experience Platform을 통해 제공되는 다양한 비즈니스 사용 사례에 대해 자세히 알아보려면 다음 문서를 읽는 것이 좋습니다.

* [쿼리 서비스의 다용성과 이점을 보여 주는 중단된 찾아보기 사용 사례의 전체적인 예입니다.](./abandoned-browse.md)
* [쿼리 서비스 및 머신 러닝을 사용하여 정품 온라인 웹 사이트 방문자 트래픽에서 봇 활동을 결정하고 필터링하는 방법](./bot-filtering.md)
* [선택한 문자열과 거의 일치하여 여러 데이터 세트의 결과를 결합하는 Platform 데이터에 대해 일치 작업을 수행하는 방법입니다.](./fuzzy-match.md)

<!-- "Data signals are actions taken by consumers while online that offer clues about intent that can be acted upon. This includes anything from visiting a website to filling out a change of address or clicking an ad."  -->

<!-- "Customer touchpoints are your brand's points of customer contact, from start to finish." -->
