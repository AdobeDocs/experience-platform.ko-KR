---
title: Adobe Experience Platform 릴리스 정보
description: 2021년 4월 21일자 Experience Platform 릴리스 노트
doc-type: release notes
last-update: April 21, 2021
author: ens72741
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
translation-type: tm+mt
source-git-commit: 9b63a47a8da07830313c0a8e690c7247dc3fbe6b
workflow-type: tm+mt
source-wordcount: '868'
ht-degree: 10%

---


# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2021년 4월 21일**

Adobe Experience Platform의 기존 기능 업데이트:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Experience Data Model (XDM)]](#xdm)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 데이터 엔지니어가 XDM(Experience Data Model)을 통해 데이터를 매핑, 변형 및 확인할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 기존 데이터 파일에 대한 매핑 편집 지원 | 이제 기존 데이터 흐름 매핑 세트를 업데이트할 수 있습니다. 1회 수집으로 예약된 데이터 프롤에 대한 매핑 세트는 업데이트할 수 없습니다. 이 기능은 HTTP API, Adobe Analytics, Adobe Audience Manager 및 [!DNL Marketo Engage]에서 지원되지 않습니다. 자세한 내용은 UI](../../sources/tutorials/ui/update-dataflows.md)에서 소스 데이터 흐름 업데이트에 대한 자습서를 참조하십시오.[ |
| 스트리밍 통합 지원 | 이제 스트리밍 소스 연결을 만들 때 데이터 준비 기능을 사용할 수 있습니다. 자세한 내용은 UI](../../sources/tutorials/ui/create/streaming/http.md)에서 스트리밍 소스 연결 만들기에 대한 자습서를 참조하십시오.[ |

자세한 내용은 [[!DNL Data Prep] 개요](../../data-prep/home.md)를 참조하십시오.

## [!DNL Experience Data Model (XDM)] {#xdm}

XDM(Experience Data Model)은 디지털 경험의 성능을 개선하기 위해 설계된 오픈 소스 사양입니다. Adobe Experience Platform의 서비스와 통신할 수 있도록 모든 응용 프로그램에 대한 공통 구조와 정의를 제공합니다. XDM 표준을 준수함으로써 모든 고객 경험 데이터를 하나의 공통 표현으로 통합하여 보다 빠르고 통합된 방식으로 통찰력을 전달할 수 있습니다. 고객 행동을 통해 유용한 인사이트를 얻고, 세그먼트를 통해 고객 고객을 정의하고, 고객 속성을 개인화를 위해 사용할 수 있습니다.

| 기능 | 설명 |
| --- | --- |
| 업계별 스키마 권장 사항 | 스키마 편집기 UI에서 클래스와 믹스를 선택할 때 새 필터를 사용하여 특정 업계를 기반으로 권장 표준 구성 요소를 볼 수 있습니다. 이러한 구성 요소가 서로 다른 업계 사용 사례에서 서로 연관되는 방법에 대한 자세한 내용은 [업계 데이터 모델](https://www.adobe.com/go/xdm-industry-erds-en)의 설명서를 참조하십시오. |

## [!DNL Intelligent Services] {#intelligent-services}

Intelligent Services를 통해 마케팅 분석가와 전문가는 인공 지능과 머신 러닝을 활용하여 고객 경험 사례를 활용할 수 있습니다. 이를 통해 마케팅 분석가는 데이터 과학 전문 지식 없이도 비즈니스 수준 구성을 사용하여 기업의 요구 사항에 맞는 예측을 설정할 수 있습니다.

### 고객 AI

실시간 고객 데이터 플랫폼에서 제공되는 고객 AI는 개별 프로파일에 대한 이탈 및 전환과 같은 맞춤형 성향 점수를 규모에 맞게 생성하는 데 사용됩니다. 비즈니스 요구 사항을 머신 러닝 문제로 변환하거나 알고리즘을 선택하거나 교육 또는 배포하지 않아도 됩니다.

| 기능 | 설명 |
| ------- | ----------- |
| Adobe Analytics 데이터 지원 | CEE(Consumer Experience Event) 스키마를 따르기 위해 데이터를 ETL할 필요 없이 Analytics 소스 커넥터를 통해 Adobe Analytics 데이터 세트를 지원하는 기능이 업데이트되었습니다. |
| Adobe Audience Manager 데이터 지원 | CEE(Consumer Experience Event) 스키마를 따르기 위해 데이터를 ETL할 필요 없이 Audience Manager 소스 커넥터를 통해 Adobe Audience Manager 데이터 세트를 지원하는 기능이 업데이트되었습니다. |
| 모델 성능 요약 | 이제 고객 AI에 서비스 인스턴스 인사이트 페이지 내에 [모델 성능 요약 탭](../../intelligent-services/customer-ai/user-guide/discover-insights.md#performance-metrics)이 있습니다. 모델 성능 탭에는 모든 실제 전환율과 이탈률이 표시됩니다. 이를 통해 각 성향 버킷에서 발생하는 상황을 해석하고 이해할 수 있습니다. |

지원되는 데이터 집합에 대한 자세한 내용은 [[!DNL Intelligent Services] 데이터 준비 설명서](../../intelligent-services/data-preparation.md)를 참조하십시오.

### Attribution AI

Attribution AI는 전환 이벤트로 연결되는 터치포인트에 크레딧을 적용하는 데 사용됩니다. 이를 통해 마케터는 고객 여정 전반에서 각 개별 마케팅 터치포인트의 마케팅 효과를 수량화할 수 있습니다.

| 기능 | 설명 |
| ------- | ----------- |
| Adobe Analytics 데이터 지원 | CEE(Consumer Experience Event) 스키마를 따르기 위해 데이터를 ETL할 필요 없이 Analytics 소스 커넥터를 통해 Adobe Analytics 데이터 세트를 지원하는 기능이 업데이트되었습니다. |

지원되는 데이터 집합에 대한 자세한 내용은 [[!DNL Intelligent Services] 데이터 준비 설명서](../../intelligent-services/data-preparation.md)를 참조하십시오.

## 세분화 서비스 {#segmentation}

Adobe Experience Platform 세그멘테이션 서비스는 세그먼트를 작성하고 [!DNL Real-time Customer Profile] 데이터에서 대상을 생성할 수 있는 사용자 인터페이스와 RESTful API를 제공합니다. 이러한 세그먼트는 중앙에 구성되고 플랫폼에 유지 관리되므로 모든 Adobe 애플리케이션에서 쉽게 액세스할 수 있습니다.

[!DNL Segmentation Service] 고객 기반 내에서 마케팅 가능한 사용자 그룹을 구분하는 기준을 설명하여 특정 프로필 하위 집합을 정의합니다. 세그먼트는 브랜드 고객과의 상호 작용을 나타내는 레코드 데이터(인구 통계 정보 등) 또는 시간 시리즈 이벤트를 기반으로 할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 추가 집계 함수 | 세그먼트 빌더에 카운트 함수가 추가되었습니다. 카운트 함수를 사용하면 지정된 이벤트가 수행된 횟수를 카운트할 수 있습니다. 카운트 함수에 대한 자세한 내용은 [세그먼트 빌더 안내서](../../segmentation/ui/segment-builder.md#count-functions)의 카운트 함수 섹션에 있습니다. |

[!DNL Segmentation Service]에 대한 자세한 내용은 [세그멘테이션 개요](../../segmentation/home.md)를 참조하십시오.

## [!DNL Sources] {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 인제스트할 수 있는 한편, 플랫폼 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 제3자 소프트웨어 및 CRM 시스템과 같은 다양한 소스의 데이터를 인제스트할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API와 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결할 수 있고 통합 실행에 대한 시간을 설정할 수 있으며 데이터 통합 처리량을 관리할 수 있습니다.

| 기능 | 설명 |
| ------- | ----------- |
| [!DNL Marketo Engage] (베타) | 이제 UI를 사용하여 [!DNL Marketo Engage] 소스 연결을 만들어 B2B 데이터를 플랫폼에 연결된 애플리케이션을 사용하여 최신 상태로 유지할 수 있습니다. 자세한 내용은 [[!DNL Marketo Engage] 소스 커넥터 설명서](../../sources/connectors/adobe-applications/marketo/marketo.md)를 참조하십시오. |

소스에 대한 자세한 내용은 [소스 개요](../../sources/home.md)를 참조하십시오.
