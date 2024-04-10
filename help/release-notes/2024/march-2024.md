---
title: Adobe Experience Platform 릴리스 노트 2024년 3월
description: Adobe Experience Platform의 2024년 3월 릴리스 정보입니다.
exl-id: cab47a76-04f3-48ec-82aa-d17645e4eb15
source-git-commit: d698bf0b8b0dbdb85909008bb3b60efb0575accc
workflow-type: tm+mt
source-wordcount: '1191'
ht-degree: 33%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 일자: 2024년 3월 19일 수요일**

>[!TIP]
>
>사용 [Adobe Experience Platform 용어](/help/landing/glossary.md) Real-time Customer Data Platform 및 Adobe Experience Platform에 사용되는 용어를 숙지합니다. 찾고 있는 특정 용어를 찾을 수 없는 경우 페이지의 피드백 옵션을 사용하여 용어집에 새 용어를 추가하도록 요청합니다.

Experience Platform의 기존 기능 업데이트:

- [카탈로그 서비스](#catalog-service)
- [데이터 수집](#data-collection)
- [데이터 준비](#data-prep)
- [대상](#destinations)
- [경험 데이터 모델 (XDM)](#xdm)
- [Segmentation Service](#segmentation)
- [소스](#sources)

## 카탈로그 서비스 {#catalog-service}

카탈로그 서비스는 Adobe Experience Platform 내의 데이터 위치 및 계보에 대한 레코드 시스템입니다. Experience Platform에 수집되는 모든 데이터는 파일 및 디렉터리로 데이터 레이크에 저장되지만, 카탈로그는 조회 및 모니터링을 위해 이러한 파일 및 디렉터리에 대한 메타데이터 및 설명을 보유합니다.

| 기능 | 설명 |
| --- | --- |
| 추가 작업 | 이제 세부 정보 보기에서 &quot;추가 작업&quot; 기능을 사용하여 데이터 세트에 대한 추가 작업을 수행하여 작업을 보다 유연하게 하고 데이터를 관리할 수 있습니다. 선택한 데이터 세트의 세부 정보 페이지에서 데이터 세트를 삭제하거나 실시간 고객 프로필에 사용하도록 설정할 수 있습니다.<br>**참고:** 프로필 수집을 위해 데이터 세트를 활성화하는 경우, 데이터 세트의 스키마가 실시간 고객 프로필과 호환되어야 합니다.<br>![를 사용하는 데이터 세트 작업 공간 [!UICONTROL ... 자세히] 드롭다운 메뉴가 강조 표시됩니다.](../2024/assets/march/more-actions.png "기타 드롭다운 메뉴가 강조 표시된 데이터 세트 작업 영역입니다."){width="100" zoomable="yes"}.<br>읽기 [데이터 세트 사용 안내서](../../catalog/datasets/user-guide.md) 추가 정보에 대한 설명서입니다. |

{style="table-layout:auto"}

카탈로그 서비스에 대한 자세한 내용은 [카탈로그 서비스 개요](../../catalog/home.md)를 참조하십시오.

## 데이터 수집 {#data-collection}

Adobe Experience Platform은 클라이언트측 고객 경험 데이터를 수집하여 Adobe 또는 비 Adobe 대상으로 보강, 변환 및 배포가 가능한 Adobe Experience Platform Edge Network로 보낼 수 있는 기술 제품군을 제공합니다.

**새로운 기능**

| 유형 | 기능 | 설명 |
| --- | --- | --- |
| 확장 | [!DNL Merkury] 태그 확장 | 다음 [[!DNL Merkury] 태그 확장](https://exchange.adobe.com/apps/ec/600027/merkury-tag) 은 익명의 웹 사이트 방문자에게 업계 최고의 일치율을 제공합니다. [!DNL Merkury] ID 브랜드는 의 기능을 활용할 수 있습니다. [!DNL Merkury] 태그와 Adobe을 통해 개인화된 실시간 웹 사이트 경험을 제공할 수 있습니다. 또한 [!DNL Merkury] tag를 사용하면 연결된 온라인 및 오프라인 고객 프로필과 함께 자사 디지털 데이터를 확장할 수 있습니다. |

{style="table-layout:auto"}

데이터 수집에 대한 자세한 내용은 [데이터 수집 개요](../../tags/home.md).

## 데이터 준비 {#data-prep}

데이터 준비를 사용하면 데이터 엔지니어가 XDM(Experience Data Model)과의 데이터를 매핑, 변환 및 확인할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| Adobe Analytics용 새로운 매퍼 함수 | 이제 다음 함수를 사용하여 Adobe Analytics에서 이벤트 데이터를 추출할 수 있습니다. <ul><li>`aa_get_event_id`</li><li>`aa_get_event_value`</li><li>`aa_get_product_categories`</li><li>`aa_get_product_names`</li><li>`aa_get_product_quantities`</li><li>`aa_get_product_prices`</li><li>`aa_get_product_event_values`</li><li>`aa_get_product_evars`</li></ul> 이러한 함수에 대한 자세한 내용은 [데이터 준비 기능 안내서](../../data-prep/functions.md#analytics-functions) |

{style="table-layout:auto"}

데이터 준비에 대한 자세한 내용은 [데이터 준비 개요](../../data-prep/home.md).

## 대상 {#destinations}

[!DNL Destinations]는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있는 대상 플랫폼과 사전 설치된 통합입니다. 대상을 사용해 교차 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새 대상 및 업데이트된 대상** {#new-updated-destinations}

| 대상 | 유형 | 설명 |
| ----------- | --------- | ----------- |
| [(베타) Acxiom 데이터 개선 연결](../../destinations/catalog/data-partner/acxiom-data-enhancement.md) | 새로운 기능 | 이 커넥터를 사용하여 데이터 강화를 위해 Real-Time CDP에서 Acxiom으로 자사 프로필을 활성화하고 마케팅 채널 전반에서 사용할 수 있습니다. 그런 다음 Acxiom 소스를 사용하여 고급 데이터가 포함된 프로필을 가져오고 Real-Time CDP에서 작업할 수 있습니다. |
| [(Beta) Acxiom 잠재 고객 억제 연결](../../destinations/catalog/data-partner/acxiom-prospect-suppression.md) | 새로운 기능 | Acxiom 대상에 자사 대상을 내보내고 Acxiom이 알려지거나 전환된 고객을 억제하도록 합니다. 그런 다음 를 사용합니다. [Acxiom 전망 데이터 가져오기](../../sources/connectors/data-partners/acxiom-prospecting-data-import.md) 알려진 또는 전환된 고객이 제거된 Acxiom의 잠재 고객 목록을 수집하고 활성화하기 위한 소스 커넥터 |
| [Amazon 광고 연결](../../destinations/catalog/advertising/amazon-ads.md) | 업데이트 | 이제 Amazon 광고 대상으로 데이터를 내보낼 때 Amazon DSP 또는 Amazon Marketing Cloud(신규)로 데이터를 라우팅할 수 있습니다. |
| [LiveRamp 온보드 연결](../../destinations/catalog/advertising/liveramp-onboarding.md) | 업데이트 | 이제 LiveRamp 온보딩 대상은 유럽 및 오스트레일리아로 배달할 수 있습니다 [!DNL LiveRamp] [!DNL SFTP] 인스턴스. 내보낸 최대 파일 크기도 1,000만 행(이전 500만 행에서)으로 증가했습니다. |

{style="table-layout:auto"}

<!--

**New or updated functionality** {#destinations-new-updated-functionality}

-->

대상에 대한 일반적인 정보는 [대상 개요](../../destinations/home.md)를 참조하십시오.

## 경험 데이터 모델 (XDM) {#xdm}

XDM은 Adobe Experience Platform으로 가져오는 데이터에 대한 공통 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수하여 모든 고객 경험 데이터를 공통된 표현에 통합해 보다 빠르고 통합된 방식으로 인사이트를 제공할 수 있습니다. 고객 조치에서 귀중한 인사이트를 얻고, 세그먼트를 통해 고객 대상자를 정의하고, 개인 설정 목적으로 고객 속성을 사용할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| Experience Platform UI 맵 데이터 유형 지원 | Platform UI에서 맵 필드를 정의하여 XDM(Experience Data Model) 데이터 구조를 추가로 사용자 지정합니다. 이제 스키마 편집기에서 맵 필드를 만들어 유연한 데이터 구조를 모델링하거나 키-값 쌍을 효율적으로 저장할 수 있습니다. 새 필드를 정의할 때 유형 드롭다운에서 &quot;맵&quot;을 선택하여 하위 필드를 구성하고 필드 그룹에 지정합니다. 지원되는 맵 값 유형은 문자열 및 정수입니다.<br>![유형 및 맵 값 유형 필드가 강조 표시된 스키마 편집기.](../2024/assets/march/maps.png "유형 및 맵 값 유형 필드가 강조 표시된 스키마 편집기."){width="100" zoomable="yes"}<br> 방법 알아보기 [ui에서 맵 필드 정의](../../xdm/ui/fields/map.md)UI 안내서를 참조하십시오. |

{style="table-layout:auto"}

Platform의 XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md)를 참조하십시오.

## Segmentation Service {#segmentation}

[!DNL Segmentation Service]를 사용하여 개인 사용자(예: 고객, 잠재 고객, 사용자 또는 조직)와 관련된 [!DNL Experience Platform]에 저장된 데이터를 대상자로 세분화할 수 있습니다. 세그먼트 정의 또는 [!DNL Real-Time Customer Profile] 데이터의 다른 소스를 통해 대상자를 만들 수 있습니다. 이러한 대상자는 [!DNL Platform]을 통해 중앙 집중식으로 구성 및 유지 관리되고 모든 Adobe 솔루션에서 쉽게 액세스할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 대량 작업 | 이제 대상 인벤토리가 일괄 작업을 지원합니다. 일괄 작업을 사용하면 여러 대상을 빠르게 선택하여 폴더로 이동하거나, 태그를 적용하거나, 액세스 레이블을 적용하거나, 삭제할 수 있습니다. <br> ![대상자 UI 작업 영역의 일괄 작업.](../2024/assets/march/bulk-actions.png "대상자 UI 작업 영역의 일괄 작업."){width="100" zoomable="yes"} <br>이 기능에 대한 자세한 내용은 [세그먼테이션 서비스 UI 안내서](../../segmentation/ui/overview.md#bulk-actions). |

{style="table-layout:auto"}

세분화 서비스에 대해 자세히 알아보려면 [세그먼테이션 서비스 개요](../../segmentation/home.md).

## 소스 {#sources}

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새 소스 및 업데이트된 소스**

| 기능 | 유형 | 설명 |
| --- | --- | --- |
| [!BADGE 베타]{type=Informative} [!DNL Acxiom Data Ingestion] | 새로운 기능 | 사용 [[!DNL Acxiom Data Ingestion] 소스](../../sources/tutorials/ui/create/data-partners/acxiom-data-ingestion.md) 수집 [!DNL Acxiom] 데이터를 Real-time Customer Data Platform으로 가져와서 자사 프로필을 보강합니다. 그러면 다음을 사용할 수 있습니다. [!DNL Acxiom]-향상된 자사 프로필을 통해 대상자를 개선하고 마케팅 채널 전반에서 활성화합니다. <br> ![Acxiom 데이터 섭취 소스.](../2024/assets/march/acxiom-data-ingestion.png "새로운 Acxiom 데이터 수집 소스."){width="100" zoomable="yes"} <br> 읽기 [[!DNL Acxiom Data Ingestion] 개요](../../sources/connectors/data-partners/acxiom-data-ingestion.md) 을 참조하십시오. |
| [!BADGE 베타]{type=Informative} [!DNL Stripe] | 새로운 기능 | 사용 [[!DNL Stripe] 소스](../../sources/connectors/payments/stripe.md) 고객이 구매 플로우 중에 캡처한 데이터를 Experience Platform으로 수집 수집되면 이 데이터를 사용하여 개인화된 오퍼를 만들고 더 풍부한 비즈니스 통찰력을 확보할 수 있습니다. <br> ![Stripe 소스.](../2024/assets/march/stripe.png "새 Stripe 소스."){width="100" zoomable="yes"} <br> 읽기 [[!DNL Stripe] 개요](../../sources/connectors/payments/stripe.md) 을 참조하십시오. |
| 에 대한 UI 지원 [!DNL Snowflake Streaming] | 새로운 기능 | 이제 다음을 사용할 수 있습니다. [[!DNL Snowflake Streaming] 소스](../../sources/tutorials/ui/create/databases/snowflake-streaming.md) Experience Platform UI에서, [!DNL Snowflake] 데이터베이스. <br> ![Snowflake 스트리밍 소스.](../2024/assets/march/snowflake-streaming.png "새 Snowflake 문자열 소스입니다."){width="100" zoomable="yes"} <br> 읽기 [[!DNL Snowflake Streaming] 개요](../../sources/connectors/databases/snowflake-streaming.md) 을 참조하십시오. |

{style="table-layout:auto"}

소스에 대한 자세한 내용은 [소스 개요](../../sources/home.md).
