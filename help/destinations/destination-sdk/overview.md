---
description: Adobe Experience Platform Destination SDK은 선택한 데이터 및 인증 형식에 따라 Experience Platform이 대상 및 프로필 데이터를 종단점에 제공할 대상 통합 패턴을 구성할 수 있도록 해주는 구성 API 세트입니다. 구성은 Experience Platform에 저장되며, 추가 업데이트를 위해 API를 통해 검색할 수 있습니다.
title: Adobe Experience Platform Destination SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: 85b308b3f92a734fed0c885a574b71fa05684bb4
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 2%

---

# Adobe Experience Platform Destination SDK

## 개요 {#destinations-sdk}

Adobe Experience Platform Destination SDK은 선택한 데이터 및 인증 형식에 따라 Experience Platform이 대상 및 프로필 데이터를 종단점에 제공할 대상 통합 패턴을 구성할 수 있도록 해주는 구성 API 세트입니다. 구성은 Experience Platform에 저장되며, 추가 업데이트를 위해 API를 통해 검색할 수 있습니다.

Destination SDK 설명서에서는 Adobe Experience Platform Destination SDK을 사용하여 Adobe Experience Platform와의 제품 화된 대상 통합을 구성, 테스트 및 출시하고 대상을 계속 증가하는 대상 카탈로그에 포함하도록 하는 지침을 제공합니다.

![대상 카탈로그 개요](./assets/destinations-catalog-overview.png)

## 프로덕션 및 사용자 지정 통합 {#productized-custom-integrations}

Destination SDK 파트너인 은 제품 대상을 [Experience Platform 카탈로그](/help/destinations/catalog/overview.md):
1. 사전 구성된 매개 변수로 고객 간의 통합 구성을 표준화하고 고객을 위한 설정 경험을 간소화합니다.
2. 고객 설정 및 인식을 간소화하기 위해 Experience Platform 대상 카탈로그에 브랜드 대상 카드를 도입합니다.
3. Adobe Experience Platform 및 Real-time Customer Data Platform과 통합된 생산형 대상 제품으로 부각됩니다.

Experience Platform 고객은 활성화 요구 사항에 가장 적합한 고유한 사용자 지정 대상을 작성할 수 있습니다.

![Destination SDK 시각적 다이어그램](./assets/destination-sdk-visual.png)

<!--

## Types of destinations in Adobe Experience Platform {#types-of-destinations}

In Adobe Experience Platform, we distinguish between two destination types - *connections* and *extensions*. In the user interface, customers can choose between two types of connection destinations, Profile Export destinations and Segment Export destinations. For more details around the difference between the different destination types, read [Destination Types and Categories](https://experienceleague.adobe.com/docs/experience-platform/destinations/destination-types.html?lang=en).

![Destination types](./assets/types-of-destinations.png)

This documentation set provides you with all the necessary information to add your destination to Adobe Experience Platform, as a *connection*, either Profile Export or Segment Export. To set up an extension, visit the [Experience Platform Launch developer portal](https://developer.adobelaunch.com/extensions/).

-->

## 지원되는 통합 유형 {#supported-integration-types}

Destination SDK을 통해 Adobe Experience Platform은 REST API 종단점이 있는 대상과의 실시간 통합을 지원합니다. Experience Platform과 실시간 통합은 다음과 같은 기능을 지원합니다.
* 메시지 변환 및 집계
* 프로필 채우기
* 대상 설정 및 데이터 전송을 초기화하도록 구성 가능한 메타데이터 통합
* 구성 가능한 인증
* 대상 구성을 테스트 및 반복할 수 있는 테스트 및 유효성 검사 API 세트

의 대상 측에 있는 기술 요구 사항에 대해 읽어보십시오. [통합 사전 요구 사항](./integration-prerequisites.md) 문서.


## Destination SDK 액세스 권한 얻기 {#get-access}

Destination SDK 액세스는 파트너 또는 Experience Platform 고객의 상태에 따라 다릅니다. 자세한 내용은 아래 표를 참조하십시오.


| 파트너 또는 고객 유형 | Destination SDK 액세스 방법 |
---------|----------|
| 독립 소프트웨어 공급업체(ISV) | 가입 [Adobe 교환 프로그램](https://partners.adobe.com/exchangeprogram/experiencecloud.html) 및 Destination SDK 액세스를 위해 Experience Platform 샌드박스를 공급하도록 요청합니다. |
| 시스템 통합자(SI) | Gold 또는 Platinum 수준에서 [Adobe 솔루션 파트너 프로그램](https://solutionpartners.adobe.com/home.html)로 설정되면 Experience Platform 샌드박스가 프로비저닝되고 Destination SDK에 액세스할 수 있습니다. |
| 에서 고객 Experience Platform [활성화 패키지](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) | 기본적으로 Experience Platform 샌드박스 및 Destination SDK에 액세스할 수 있습니다. |
| 에서 고객 Experience Platform [실시간 CDP 패키지](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) | Destination SDK에 액세스할 수 없지만 Destination SDK을 사용하여 다른 회사가 구성하고 Experience Platform 조직 간에 게시된 모든 프로덕션 대상에 액세스할 수 있습니다. |

{style=&quot;table-layout:auto&quot;}

## 높은 수준의 프로세스 {#process}

Experience Platform에서 대상을 구성하는 프로세스는 다음과 같습니다.

1. ISV 또는 SI인 경우 위의 섹션에서 액세스 정보를 참조하십시오. [Adobe Experience Platform 활성화](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) 고객은 이 단계를 건너뛸 수 있습니다.
2. [Experience Platform 샌드박스 제공 요청](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) 대상 작성 권한을 사용하도록 설정합니다.
3. [통합 빌드](./configure-destination-instructions.md) 제품 설명서를 참조합니다.
4. [통합 테스트](./test-destination.md) 제품 설명서를 참조합니다.
5. [통합 제출](./submit-destination.md) Adobe 검토(표준 응답 시간은 5영업일).
6. ISV 또는 SI에서 [제품 통합](./overview.md#productized-custom-integrations)를 사용하려면 [셀프 서비스 설명서 프로세스](./docs-framework/documentation-instructions.md) 대상을 위한 Experience League에 대한 제품 설명서 페이지를 만들려면
7. Adobe이 승인하면 통합에 [Experience Platform 카탈로그](/help/destinations/catalog/overview.md).
8. 통합을 업데이트하려면 동일한 프로세스를 따르십시오.

## 참조 {#reference}

Adobe은 다음 Experience Platform 설명서를 읽고 이해할 것을 권장합니다.

* [Adobe Experience Platform 대상 개요](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en)
* [XDM 스키마 구성 기초](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en)
* [ID 네임스페이스 개요](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=ko)
