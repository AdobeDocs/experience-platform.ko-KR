---
description: Adobe Experience Platform 대상 SDK는 선택한 데이터 및 인증 형식에 따라 Experience Platform이 대상 및 프로필 데이터를 종단점에 전달하도록 대상 통합 패턴을 구성할 수 있도록 해주는 구성 API 세트입니다. 구성은 Experience Platform에 저장되며, 추가 업데이트를 위해 API를 통해 검색할 수 있습니다.
title: Adobe Experience Platform 대상 SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: 2841adc0ce212a945c35ba38209d4c00c519ad7b
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 2%

---

# Adobe Experience Platform 대상 SDK

## 개요 {#destinations-sdk}

Adobe Experience Platform 대상 SDK는 선택한 데이터 및 인증 형식에 따라 Experience Platform이 대상 및 프로필 데이터를 종단점에 제공하기 위한 대상 통합 패턴을 구성할 수 있도록 해주는 구성 API 세트입니다. 구성은 Experience Platform에 저장되며, 추가 업데이트를 위해 API를 통해 검색할 수 있습니다.

대상 SDK 설명서는 Adobe Experience Platform 대상 SDK를 사용하여 Adobe Experience Platform와의 제품 화된 대상 통합을 구성, 테스트 및 출시하고 대상을 계속 증가하는 대상 카탈로그의 일부가 되도록 하는 지침을 제공합니다.

![대상 카탈로그 개요](./assets/destinations-catalog-overview.png)

## 프로덕션 및 사용자 지정 통합 {#productized-custom-integrations}

대상 SDK 파트너는 [Experience Platform 카탈로그](/help/destinations/catalog/overview.md)에 생성된 대상을 추가할 수 있습니다.
1. 사전 구성된 매개 변수로 고객 간의 통합 구성을 표준화하고 고객을 위한 설정 경험을 간소화합니다.
2. 고객 설정 및 인식을 간소화하기 위해 Experience Platform 대상 카탈로그에 브랜드 대상 카드를 도입합니다.
3. Adobe Experience Platform 및 실시간 고객 데이터 플랫폼과 통합된 제품 기반의 대상 제품으로 소개

Experience Platform 고객은 활성화 요구 사항에 가장 적합한 고유한 사용자 지정 대상을 작성할 수 있습니다.

![대상 SDK 시각적 다이어그램](./assets/destination-sdk-visual.png)

<!--

## Types of destinations in Adobe Experience Platform {#types-of-destinations}

In Adobe Experience Platform, we distinguish between two destination types - *connections* and *extensions*. In the user interface, customers can choose between two types of connection destinations, Profile Export destinations and Segment Export destinations. For more details around the difference between the different destination types, read [Destination Types and Categories](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=en).

![Destination types](./assets/types-of-destinations.png)

This documentation set provides you with all the necessary information to add your destination to Adobe Experience Platform, as a *connection*, either Profile Export or Segment Export. To set up an extension, visit the [Experience Platform Launch developer portal](https://developer.adobelaunch.com/extensions/).

-->

## 지원되는 통합 유형 {#supported-integration-types}

대상 SDK를 통해 Adobe Experience Platform은 REST API 엔드포인트가 있는 대상과의 실시간 통합을 지원합니다. Experience Platform과 실시간 통합은 다음과 같은 기능을 지원합니다.
* 메시지 변환 및 집계
* 프로필 채우기
* 대상 설정 및 데이터 전송을 초기화하도록 구성 가능한 메타데이터 통합
* 구성 가능한 인증
* 대상 구성을 테스트 및 반복할 수 있는 테스트 및 유효성 검사 API 세트

[통합 사전 요구 사항](./integration-prerequisites.md) 문서에 있는 대상 측의 기술 요구 사항에 대해 읽어보십시오.


## 대상 SDK에 대한 액세스 권한 얻기 {#get-access}

대상 SDK 액세스는 파트너 또는 Experience Platform 고객의 상태에 따라 다릅니다. 자세한 내용은 아래 표를 참조하십시오.


| 파트너 또는 고객 유형 | 대상 SDK에 액세스하는 방법 |
---------|----------|
| 독립 소프트웨어 공급업체(ISV) | [Adobe Exchange 프로그램](https://partners.adobe.com/exchangeprogram/experiencecloud.html)에 참여하고 대상 SDK에 액세스하기 위해 제공된 Experience Platform 샌드박스 를 가져오도록 요청합니다. |
| 시스템 통합자(SI) | [Adobe 솔루션 파트너 프로그램](https://solutionpartners.adobe.com/home.html)에서 Gold 또는 Platinum 수준에 있어야 하며, Experience Platform 샌드박스가 프로비저닝되고 대상 SDK에 액세스할 수 있습니다. |
| 활성화 패키지의 고객 Experience Platform | 기본적으로 Experience Platform 샌드박스 및 대상 SDK에 액세스할 수 있습니다. |
| 실시간 CDP 패키지에서 고객 Experience Platform | 대상 SDK에 액세스할 수 없지만 대상 SDK를 사용하여 다른 회사가 구성하고 Experience Platform 조직 간에 게시된 모든 제품 대상 항목에 액세스할 수 있습니다. |

{style=&quot;table-layout:auto&quot;}

## 높은 수준의 프로세스 {#process}

Experience Platform에서 대상을 구성하는 프로세스는 다음과 같습니다.

1. ISV 또는 SI인 경우 위의 섹션에서 액세스 정보를 참조하십시오. [Adobe Experience Platform ](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) Activation 고객은 이 단계를 건너뛸 수 있습니다.
2. [Experience Platform 샌드박스를 프로비저닝하고 ](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) 대상 작성 권한을 사용하도록 요청합니다.
3. [제품 ](./configure-destination-instructions.md) 설명서에 따라 통합을 빌드합니다.
4. [제품 ](./test-destination.md) 설명서에 따라 통합을 테스트합니다.
5. [Adobe](./destination-publish-api.md) 의 검토를 위해 통합을 실행합니다(표준 응답 시간은 5영업일).
6. ISV 또는 SI에서 [제품 통합](./overview.md#productized-custom-integrations)을(를) 만드는 경우 [셀프 서비스 설명서 프로세스](./docs-framework/documentation-instructions.md)를 사용하여 대상에 대한 Experience League에 제품 설명서 페이지를 만듭니다.
7. Adobe이 승인하면 통합이 [Experience Platform 카탈로그](/help/destinations/catalog/overview.md)에 표시됩니다.
8. 통합을 업데이트하려면 동일한 프로세스를 따르십시오.

## 참조 {#reference}

Adobe은 다음 Experience Platform 설명서를 읽고 이해할 것을 권장합니다.

* [Adobe Experience Platform 대상 개요](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en)
* [XDM 스키마 구성 기초](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en)
* [ID 네임스페이스 개요](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=ko)
