---
description: Adobe Experience Platform Destination SDK은 선택한 데이터 및 인증 형식을 기반으로 대상 및 프로필 데이터를 엔드포인트 또는 스토리지 위치에 전달하도록 Experience Platform에 대한 대상 통합 패턴을 구성할 수 있는 구성 API 세트입니다. 구성은 Experience Platform에 저장되며 추가 업데이트를 위해 API를 통해 검색할 수 있습니다.
title: Adobe Experience Platform Destination SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: 34ae6f0f791a40584c2d476ed715bb7c5b733c42
workflow-type: tm+mt
source-wordcount: '808'
ht-degree: 1%

---

# Adobe Experience Platform Destination SDK

Adobe Experience Platform Destination SDK은 선택한 데이터 및 인증 형식을 기반으로 대상과 프로필 데이터를 엔드포인트 또는 스토리지 위치에 제공하기 위해 Experience Platform에 대한 대상 통합 패턴을 구성할 수 있는 구성 API 세트입니다. 구성은 Experience Platform에 저장되며 추가 업데이트를 위해 API를 통해 검색할 수 있습니다.

Destination SDK 설명서는 Adobe Experience Platform Destination SDK을 사용하여 Adobe Experience Platform과의 제품화된 대상 통합을 구성, 테스트 및 릴리스하고 대상을 지속적으로 성장하는 대상 카탈로그의 일부로 만드는 지침을 제공합니다. 또한 Destination SDK을 사용하여 사용자 지정 개인 대상을 만들어 요구 사항에 맞게 데이터를 내보낼 수도 있습니다.

![대상 카탈로그를 표시하는 Experience Platform UI의 스크린샷입니다.](assets/destinations-catalog-overview.png)

## 프로덕션 및 사용자 정의 통합 {#productized-custom-integrations}

>[!IMPORTANT]
>
> 이 기능을 사용하여 개인 사용자 지정 대상을 만들 수 있는 경우는 [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) 고객.

Destination SDK 파트너는에 제품화된 대상을 추가함으로써 혜택을 받을 수 있습니다. [Experience Platform 카탈로그](../catalog/overview.md):

1. 사전 구성된 매개 변수를 사용하여 고객 간의 통합 구성을 표준화하고 고객의 설정 환경을 간소화합니다.
2. Experience Platform 대상 카탈로그에 브랜드 대상 카드를 도입하여 고객 설정 및 인식을 간소화합니다.
3. Adobe Experience Platform 및 Adobe Real-time Customer Data Platform과의 제품화된 대상 통합으로 특화되어 있습니다.

Experience Platform 고객인 경우 활성화 요구 사항에 가장 적합한 자신만의 개인 사용자 지정 대상을 작성할 수도 있습니다.

![대상 개발자가 Destination SDK과 상호 작용하는 방법과 Real-Time CDP 고객이 제품화된 대상 및 개인 대상의 이점을 활용하는 방법을 보여주는 개요 다이어그램.](assets/destination-sdk-visual.png)

## 지원되는 통합 유형 {#supported-integration-types}

### 실시간(스트리밍) 통합 {#real-time-integrations}

Adobe Experience Platform은 Destination SDK을 통해 REST API 끝점이 있는 대상과 실시간(스트리밍이라고도 함) 통합을 지원합니다. Experience Platform과 실시간 통합은 다음과 같은 기능을 지원합니다.

* 메시지 변환 및 집계
* 프로필 채우기
* 대상 설정 및 데이터 전송을 초기화하기 위한 구성 가능한 메타데이터 통합
* 구성 가능한 인증
* 대상 구성을 테스트하고 반복할 수 있는 테스트 및 유효성 검사 API 세트입니다

### 파일 기반 통합 {#file-based-integrations}

Destination SDK을 통해 통합을 설정하여 정기적으로 파일을 원하는 저장소 위치로 내보낼 수도 있습니다. Experience Platform과 파일 기반의 통합은 다음과 같은 기능을 지원합니다.

* 여러 지원되는 형식(CSV, Parquet, JSON)으로 파일 내보내기
* 다운스트림 요구 사항을 충족하도록 내보낸 파일의 형식을 구성할 수 있는 구성 가능한 파일 형식 옵션

의 대상 쪽에 있는 기술 요구 사항에 대해 알아보십시오. [통합 사전 요구 사항](integration-prerequisites.md) 문서에서 지원되는 모든 구성에 대해 읽어보십시오. [구성 옵션](functionality/configuration-options.md) 기사

## Destination SDK 액세스 권한 얻기 {#get-access}

Destination SDK 액세스 권한은 Real-Time CDP 고객인 파트너 또는 Experience Platform의 상태에 따라 다릅니다. 자세한 내용은 아래 표를 참조하십시오.

| 파트너 또는 고객 유형 | Destination SDK 액세스 방법 |
---------|----------|
| ISV(Independent Software Vendor) | 가입 [Adobe 기술 파트너 프로그램](https://partners.adobe.com/technologyprogram/experiencecloud.html) Destination SDK 액세스를 위해 프로비저닝된 Experience Platform 샌드박스 가져오기를 요청합니다. |
| 시스템 통합자(SI) | 에서 골드 또는 플래티넘 레벨이어야 합니다. [Adobe 솔루션 파트너 프로그램](https://solutionpartners.adobe.com/home.html) Experience Platform 샌드박스가 프로비저닝되고 Destination SDK에 액세스할 수 있도록 합니다. |
| 에서 고객 Experience Platform [Real-Time CDP Ultimate 패키지](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) | 기본적으로 Experience Platform 샌드박스 및 Destination SDK에 액세스하여 조직의 개인 대상을 구축할 수 있습니다. |

{style="table-layout:auto"}

## 고급 프로세스 {#process}

Experience Platform에서 대상을 구성하는 프로세스는 아래에 요약되어 있습니다.

1. ISV 또는 SI인 경우 [액세스 권한을 가져오는 중](#get-access) 위의 섹션에 있는 정보를 참조하십시오. [Real-Time CDP Ultimate 패키지](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) 고객은 이 단계를 건너뛸 수 있습니다.
2. [Experience Platform 샌드박스 프로비전 요청](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) 대상 작성 권한을 활성화합니다.
3. 통합을 빌드합니다. 제품 설명서의 지침에 따라 을 구성합니다. [스트리밍 대상](guides/configure-destination-instructions.md) 또는 [파일 기반 대상](guides/configure-file-based-destination-instructions.md).
4. 통합을 테스트합니다. 제품 설명서의 지침에 따라 테스트하십시오 [스트리밍 대상](testing-api/streaming-destinations/streaming-destination-testing-overview.md) 또는 [파일 기반 대상](testing-api/batch-destinations/file-based-destination-testing-overview.md).
5. ISV 또는 SI에서 [제품화 통합](./overview.md#productized-custom-integrations), [통합 제출](guides/submit-destination.md) Adobe 검토(표준 응답 시간은 영업일 기준 5일).
6. 제품화된 통합을 만드는 ISV 또는 SI의 경우 [셀프서비스 설명서 프로세스](docs-framework/documentation-instructions.md) 대상 Experience League에서 제품 설명서 페이지를 만듭니다.
7. 제품화된 통합의 경우, Adobe에서 승인하면 통합이에 표시됩니다. [Experience Platform 카탈로그](../catalog/overview.md).
8. 통합을 업데이트하려면 동일한 프로세스를 따르십시오.

## 참조 {#reference}

Adobe은 다음 Experience Platform 설명서를 읽고 이해할 것을 권장합니다.

* [Adobe Experience Platform 대상 개요](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=ko)
* [XDM 스키마 컴포지션의 기반](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=ko-KR)
* [ID 네임스페이스 개요](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=ko)
