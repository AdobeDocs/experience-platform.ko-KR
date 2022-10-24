---
description: Adobe Experience Platform Destination SDK은 선택한 데이터 및 인증 형식에 따라 Experience Platform이 대상 및 프로필 데이터를 엔드포인트 또는 저장소 위치에 전달하도록 대상 통합 패턴을 구성할 수 있도록 해주는 구성 API 세트입니다. 구성은 Experience Platform에 저장되며, 추가 업데이트를 위해 API를 통해 검색할 수 있습니다.
title: Adobe Experience Platform Destination SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 2%

---

# Adobe Experience Platform Destination SDK

## 개요 {#destinations-sdk}

Adobe Experience Platform Destination SDK은 선택한 데이터 및 인증 형식을 기반으로 하여 Experience Platform이 대상 및 프로필 데이터를 엔드포인트 또는 저장소 위치에 전달하도록 대상 통합 패턴을 구성할 수 있도록 해주는 구성 API 세트입니다. 구성은 Experience Platform에 저장되며, 추가 업데이트를 위해 API를 통해 검색할 수 있습니다.

Destination SDK 설명서에서는 Adobe Experience Platform Destination SDK을 사용하여 Adobe Experience Platform와의 제품 화된 대상 통합을 구성, 테스트 및 출시하고 대상을 계속 증가하는 대상 카탈로그에 포함하도록 하는 지침을 제공합니다. Destination SDK을 사용하여 고유한 사용자 지정 개인 대상을 만들어 필요에 맞는 데이터를 내보낼 수도 있습니다.

![대상 카탈로그를 보여주는 Experience Platform UI의 스크린샷](./assets/destinations-catalog-overview.png)

## 프로덕션 및 사용자 지정 통합 {#productized-custom-integrations}

>[!IMPORTANT]
>
> 비공개 사용자 지정 대상을 만드는 이 기능은 [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) 고객.

Destination SDK 파트너인 은 제품 대상을 [Experience Platform 카탈로그](/help/destinations/catalog/overview.md):
1. 사전 구성된 매개 변수로 고객 간의 통합 구성을 표준화하고 고객을 위한 설정 경험을 간소화합니다.
2. 고객 설정 및 인식을 간소화하기 위해 Experience Platform 대상 카탈로그에 브랜드 대상 카드를 도입합니다.
3. Adobe Experience Platform 및 Adobe Real-time Customer Data Platform과 통합된 생산형 대상 제품으로 부각됩니다.

Experience Platform 고객은 활성화 요구 사항에 가장 적합한 고유한 사용자 지정 대상을 작성할 수도 있습니다.

![대상 개발자가 Destination SDK과 상호 작용하는 방법 및 Real-Time CDP 고객이 제품 및 개인 대상을 통해 혜택을 받는 방법을 보여주는 개요 다이어그램입니다.](./assets/destination-sdk-visual.png)

## 지원되는 통합 유형 {#supported-integration-types}

Destination SDK을 통해 Adobe Experience Platform은 REST API 종단점이 있는 대상과의 실시간 통합을 지원합니다. Experience Platform과 실시간 통합은 다음과 같은 기능을 지원합니다.
* 메시지 변환 및 집계
* 프로필 채우기
* 대상 설정 및 데이터 전송을 초기화하도록 구성 가능한 메타데이터 통합
* 구성 가능한 인증
* 대상 구성을 테스트 및 반복할 수 있는 테스트 및 유효성 검사 API 세트

Destination SDK을 통해 원하는 저장소 위치로 파일을 주기적으로 내보내도록 통합을 설정할 수도 있습니다. Experience Platform과 실시간 통합은 다음과 같은 기능을 지원합니다.
* 지원되는 여러 형식(CSV, Parquet, JSON)으로 파일 내보내기
* 구성 가능한 파일 형식 옵션. 이 옵션을 사용하면 다운스트림 요구 사항을 충족하도록 내보낸 파일의 형식을 구성할 수 있습니다.

의 대상 측에 있는 기술 요구 사항에 대해 읽어보십시오. [통합 사전 요구 사항](./integration-prerequisites.md) 문서.

## Destination SDK 액세스 권한 얻기 {#get-access}

Destination SDK 액세스는 Real-Time CDP 고객인 파트너 또는 Experience Platform의 상태에 따라 다릅니다. 자세한 내용은 아래 표를 참조하십시오.


| 파트너 또는 고객 유형 | Destination SDK 액세스 방법 |
---------|----------|
| 독립 소프트웨어 공급업체(ISV) | 가입 [Adobe 교환 프로그램](https://partners.adobe.com/exchangeprogram/experiencecloud.html) 및 Destination SDK 액세스를 위해 Experience Platform 샌드박스를 공급하도록 요청합니다. |
| 시스템 통합자(SI) | Gold 또는 Platinum 수준에서 [Adobe 솔루션 파트너 프로그램](https://solutionpartners.adobe.com/home.html)로 설정되면 Experience Platform 샌드박스가 프로비저닝되고 Destination SDK에 액세스할 수 있습니다. |
| 에서 고객 Experience Platform [Real-Time CDP Ultimate 패키지](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) | 기본적으로 Experience Platform 샌드박스 및 Destination SDK에 액세스할 수 있으므로 조직을 위한 개인 대상을 작성할 수 있습니다. |

{style=&quot;table-layout:auto&quot;}

## 높은 수준의 프로세스 {#process}

Experience Platform에서 대상을 구성하는 프로세스는 다음과 같습니다.

1. ISV 또는 SI인 경우 위의 섹션에서 액세스 정보를 참조하십시오. [Adobe Experience Platform 활성화](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) 고객은 이 단계를 건너뛸 수 있습니다.
2. [Experience Platform 샌드박스 제공 요청](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) 대상 작성 권한을 사용하도록 설정합니다.
3. 통합을 구축합니다. 제품 설명서의 지침에 따라 을 구성합니다 [스트리밍 대상](./configure-destination-instructions.md) 또는 [파일 기반 대상](./configure-file-based-destination-instructions.md).
4. 통합을 테스트합니다. 제품 설명서의 지침에 따라 을 테스트합니다 [스트리밍 대상](./test-destination.md) 또는 [파일 기반 대상](./file-based-destination-testing-overview.md).
5. ISV 또는 SI에서 [제품 통합](./overview.md#productized-custom-integrations), [통합 제출](./submit-destination.md) Adobe 검토의 경우(표준 응답 시간은 5영업일).
6. ISV 또는 SI에서 제품 통합을 만드는 경우 [셀프 서비스 설명서 프로세스](./docs-framework/documentation-instructions.md) 대상을 위한 Experience League에 대한 제품 설명서 페이지를 만들려면
7. 프로덕션 통합의 경우, Adobe이 승인하면 통합이 [Experience Platform 카탈로그](/help/destinations/catalog/overview.md).
8. 통합을 업데이트하려면 동일한 프로세스를 따르십시오.

## 참조 {#reference}

Adobe은 다음 Experience Platform 설명서를 읽고 이해할 것을 권장합니다.

* [Adobe Experience Platform 대상 개요](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en)
* [XDM 스키마 구성 기초](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=ko-KR)
* [ID 네임스페이스 개요](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=ko)
