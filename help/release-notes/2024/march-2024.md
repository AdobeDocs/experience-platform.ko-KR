---
title: Adobe Experience Platform 릴리스 정보 2024년 3월
description: Adobe Experience Platform의 2024년 3월 릴리스 정보.
exl-id: cab47a76-04f3-48ec-82aa-d17645e4eb15
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: ht
source-wordcount: '1192'
ht-degree: 100%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 일자: 2024년 3월 19일**

>[!TIP]
>
>[Adobe Experience Platform 용어집](/help/landing/glossary.md)을 사용하여 Real-Time Customer Data Platform과 Adobe Experience Platform에서 사용되는 용어를 살펴보십시오. 찾고 있는 특정 용어가 없다면 페이지의 피드백 옵션을 사용하여 용어집에 새 용어를 추가할 것을 요청할 수 있습니다.

Experience Platform의 기존 기능 업데이트:

- [카탈로그 서비스](#catalog-service)
- [데이터 수집](#data-collection)
- [데이터 준비](#data-prep)
- [대상](#destinations)
- [경험 데이터 모델 (XDM)](#xdm)
- [Segmentation Service](#segmentation)
- [소스](#sources)

## 카탈로그 서비스 {#catalog-service}

카탈로그 서비스는 Adobe Experience Platform 내의 데이터 위치 및 계보에 대한 레코드 시스템입니다. Experience Platform에 수집된 모든 데이터는 데이터 레이크에 파일 및 디렉터리로 저장되지만 카탈로그는 조회 및 모니터링 목적으로 해당 파일 및 디렉터리에 대한 메타데이터와 설명을 제공합니다.

| 기능 | 설명 |
| --- | --- |
| 기타 액션 | 보다 유연하게 운영하고 데이터를 관리할 수 있도록 이제 세부 정보 보기에서 “기타 액션” 기능을 사용하여 데이터 세트에 대한 추가 작업을 수행할 수 있습니다. 선택한 데이터 세트의 세부 정보 페이지에서 데이터 세트를 삭제하거나 실시간 고객 프로필과 함께 사용하도록 설정할 수 있습니다.<br>**참고:** 프로필 수집을 위해 데이터 세트를 활성화하는 경우 데이터 세트의 스키마가 실시간 고객 프로필과 호환되어야 합니다.<br>![[!UICONTROL ... 자세히] 드롭다운 메뉴가 강조 표시된 데이터 세트 작업 영역.](../2024/assets/march/more-actions.png "... 자세히 드롭다운 메뉴가 강조 표시된 데이터 세트 작업 영역."){width="100" zoomable="yes"}.<br>자세한 내용은 [데이터 세트 사용 안내서](../../catalog/datasets/user-guide.md) 설명서를 참조하십시오. |

{style="table-layout:auto"}

카탈로그 서비스에 대한 자세한 내용은 [카탈로그 서비스 개요](../../catalog/home.md)를 참조하십시오.

## 데이터 준비 {#data-prep}

데이터 준비를 사용하면 데이터 엔지니어가 XDM(Experience Data Model)과의 데이터를 매핑, 변환 및 확인할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| Adobe Analytics를 위한 새로운 매퍼 기능 | 이제 다음 기능을 사용하여 Adobe Analytics에서 이벤트 데이터를 추출할 수 있습니다. <ul><li>`aa_get_event_id`</li><li>`aa_get_event_value`</li><li>`aa_get_product_categories`</li><li>`aa_get_product_names`</li><li>`aa_get_product_quantities`</li><li>`aa_get_product_prices`</li><li>`aa_get_product_event_values`</li><li>`aa_get_product_evars`</li></ul> 이들 기능에 대한 자세한 내용은 [데이터 준비 기능 안내서](../../data-prep/functions.md#analytics-functions)를 참조하십시오. |

{style="table-layout:auto"}

데이터 준비에 대한 자세한 내용은 [데이터 준비 개요](../../data-prep/home.md)를 참조하십시오.

## 데이터 수집 {#data-collection}

Adobe Experience Platform은 클라이언트측 고객 경험 데이터를 수집하여 Adobe 또는 비 Adobe 대상으로 보강, 변환 및 배포가 가능한 Adobe Experience Platform Edge Network로 보낼 수 있는 기술 제품군을 제공합니다.

**새로운 기능**

| 유형 | 기능 | 설명 |
| --- | --- | --- |
| 확장 | [!DNL Merkury] 태그 확장 기능 | [[!DNL Merkury] 태그 확장 기능](https://exchange.adobe.com/apps/ec/600027/merkury-tag)은 [!DNL Merkury] ID로 방문하는 익명의 웹 사이트 방문자에 대해 업계 최고 수준의 매칭률을 제공합니다. 브랜드는 [!DNL Merkury] 태그와 Adobe의 강력한 기능을 활용하여 실시간 맞춤형 웹 사이트 경험을 제공해 줍니다. 또한 [!DNL Merkury] 태그를 통해 연결된 온라인 및 오프라인 고객 프로필과 함께 자사 디지털 데이터를 성장시킬 수 있습니다. |

{style="table-layout:auto"}

데이터 수집에 대해 자세히 알아보려면 [데이터 수집 개요](../../tags/home.md)를 참조하십시오.

## 대상 {#destinations}

[!DNL Destinations]는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있는 대상 플랫폼과 사전 설치된 통합입니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 대상 및 업데이트된 대상** {#new-updated-destinations}

| 대상 | 유형 | 설명 |
| ----------- | --------- | ----------- |
| [(Beta) Acxiom 데이터 강화 연결](../../destinations/catalog/data-partner/acxiom-data-enhancement.md) | 새로운 기능 | 이 커넥터를 사용하여 Real-Time CDP에서 Acxiom에 이르는 자사 프로필을 활성화하여 데이터를 강화하고 마케팅 채널 전반에서 사용할 수 있습니다. 그런 다음 Acxiom 소스를 사용하여 향상된 데이터로 프로필을 가져와 Real-Time CDP에서 함께 작업할 수 있습니다. |
| [(Beta) Acxiom Prospect Suppression 연결](../../destinations/catalog/data-partner/acxiom-prospect-suppression.md) | 새로운 기능 | 자사 대상자를 Acxiom 대상으로 내보내면 Acxiom이 알려진 고객 또는 전환 고객을 제외할 수 있습니다. 그런 다음 [Acxiom 잠재 고객 데이터 가져오기](../../sources/connectors/data-partners/acxiom-prospecting-data-import.md) 소스 커넥터를 사용하여 알려진 고객 또는 전환 고객을 제거하고 Acxiom에서 잠재 고객 목록을 수집하고 활성화합니다. |
| [Amazon 광고 연결](../../destinations/catalog/advertising/amazon-ads.md) | 업데이트 | 이제 데이터를 Amazon 광고 대상으로 내보낼 때 데이터를 Amazon DSP 또는 Amazon Marketing Cloud(신규)로 라우팅할 수 있습니다. |
| [LiveRamp 온보딩 연결](../../destinations/catalog/advertising/liveramp-onboarding.md) | 업데이트 | 이제 LiveRamp 온보딩 대상은 유럽과 호주 [!DNL LiveRamp] [!DNL SFTP] 인스턴스로의 게재를 지원합니다. 내보낼 수 있는 파일 최대 크기도 이전의 500만 행에서 1,000만 행으로 증가했습니다. |

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
| Experience Platform UI 맵 데이터 유형 지원 | Experience Platform UI에서 맵 필드를 정의하여 경험 데이터 모델(XDM) 데이터 구조를 더욱 세부적으로 사용자 정의할 수 있습니다. 이제 스키마 편집기에서 맵 필드를 만들어 유연한 데이터 구조를 모델링하거나 키-값 쌍을 효율적으로 저장할 수 있습니다. 하위 필드를 구성하고 필드 그룹에 할당할 새 필드를 정의할 때 유형 드롭다운에서 “맵”을 선택합니다. 지원되는 맵 값 유형은 문자열과 정수입니다.<br>![유형 및 맵 값 유형 필드가 강조 표시된 스키마 편집기.](../2024/assets/march/maps.png "유형 및 맵 값 유형 필드가 강조 표시된 스키마 편집기."){width="100" zoomable="yes"}<br> [UI에서 맵 필드를 정의](../../xdm/ui/fields/map.md)하는 방법을 알아보려면 UI 안내서를 참조하십시오. |

{style="table-layout:auto"}

Experience Platform의 XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md)를 참조하십시오.

## Segmentation Service {#segmentation}

[!DNL Segmentation Service]를 사용하여 개인 사용자(예: 고객, 잠재 고객, 사용자 또는 조직)와 관련된 [!DNL Experience Platform]에 저장된 데이터를 대상자로 세분화할 수 있습니다. 세그먼트 정의 또는 [!DNL Real-Time Customer Profile] 데이터의 다른 소스를 통해 대상자를 만들 수 있습니다. 이러한 대상자는 [!DNL Experience Platform]을 통해 중앙 집중식으로 구성 및 유지 관리되고 모든 Adobe 솔루션에서 쉽게 액세스할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 일괄 액션 | 이제 대상자 인벤토리에서 일괄 액션이 지원됩니다. 일괄 액션을 사용하면 여러 대상자를 빠르게 선택하여 폴더로 이동하거나 태그를 적용하거나 액세스 레이블을 적용하거나 삭제할 수 있습니다. <br> ![대상자 UI 작업 영역에서의 일괄 액션.](../2024/assets/march/bulk-actions.png "대상자 UI 작업 영역에서의 일괄 액션."){width="100" zoomable="yes"} <br>이 기능에 대한 자세한 내용은 [대상자 포털 개요](../../segmentation/ui/audience-portal.md#bulk-actions)를 참조하십시오. |

{style="table-layout:auto"}

세분화 서비스에 대한 자세한 내용은 [세분화 서비스 개요](../../segmentation/home.md)를 참조하십시오.

## 소스 {#sources}

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**새로운 소스 및 업데이트된 소스**

| 기능 | 유형 | 설명 |
| --- | --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Acxiom Data Ingestion] | 새로운 기능 | [[!DNL Acxiom Data Ingestion] 소스](../../sources/tutorials/ui/create/data-partners/acxiom-data-ingestion.md)를 사용하여 [!DNL Acxiom] 데이터를 Real-Time CDP에 수집하고 자사 프로필을 강화합니다. 그런 다음 [!DNL Acxiom] 강화 자사 프로필을 사용하여 대상자를 늘리고 마케팅 채널 전반에서 활성화할 수 있습니다. <br> ![Acxiom 데이터 수집 소스.](../2024/assets/march/acxiom-data-ingestion.png "새로운 Acxiom 데이터 수집 소스."){width="100" zoomable="yes"} <br> 시작하는 방법에 대한 자세한 내용은 [[!DNL Acxiom Data Ingestion] 개요](../../sources/connectors/data-partners/acxiom-data-ingestion.md)를 참조하십시오. |
| [!BADGE Beta]{type=Informative} [!DNL Stripe] | 새로운 기능 | [[!DNL Stripe] 소스](../../sources/connectors/payments/stripe.md)를 사용하여 고객의 구매 흐름 중에 제공받은 데이터를 Experience Platform으로 수집합니다. 이 데이터를 수집하면 맞춤형 오퍼를 만들고 더 풍부한 비즈니스 인사이트를 확보할 수 있습니다. <br> ![Stripe 소스.](../2024/assets/march/stripe.png "새로운 Stripe 소스."){width="100" zoomable="yes"} <br> 시작하는 방법에 대한 자세한 내용은 [[!DNL Stripe] 개요](../../sources/connectors/payments/stripe.md)를 참조하십시오. |
| [!DNL Snowflake Streaming] UI 지원 | 새로운 기능 | 이제 Experience Platform UI의 [[!DNL Snowflake Streaming] 소스](../../sources/tutorials/ui/create/databases/snowflake-streaming.md)를 사용하여 [!DNL Snowflake] 데이터베이스의 데이터를 스트리밍할 수 있습니다. <br> ![Snowflake 스트리밍 소스.](../2024/assets/march/snowflake-streaming.png "새로운 Snowflake 스트리킹 소스."){width="100" zoomable="yes"} <br> 시작하는 방법에 대한 자세한 내용은 [[!DNL Snowflake Streaming] 개요](../../sources/connectors/databases/snowflake-streaming.md)를 참조하십시오. |

{style="table-layout:auto"}

소스에 대한 자세한 내용은 [소스 개요](../../sources/home.md)를 참조하십시오.
