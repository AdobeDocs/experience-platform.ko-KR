---
solution: Experience Platform
title: Adobe Experience Platform Destination SDK 용어집
description: Experience Platform Destination SDK을 사용하여 대상을 작성할 때의 중요한 용어를 이해합니다.
source-git-commit: 3dae91fbe46dc3e23c6ac0cfb10c25ac8473876a
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 1%

---


# Adobe Experience Platform Destination SDK 용어집

Destination SDK에 사용되는 용어에 대한 정의는 이 용어집을 참조하십시오. 기타 Adobe Experience Platform 용어의 경우 다음을 참조하십시오. [Experience Platform 용어집](/help/landing/glossary.md).

## A

**집계 정책**: 실시간 스트리밍 대상으로 데이터를 내보내는 방법을 구성할 때 대상 플랫폼으로 전송되기 전에 프로필 데이터가 집계되는 방법을 정의할 수 있습니다. 이렇게 하면 데이터 레코드를 특정 기준에 따라 그룹화하여 데이터 전달을 최적화하고, API 호출 빈도를 줄이고, 전반적인 효율성을 개선하는 데 도움이 됩니다. 다양한 대상 요구 사항을 충족하도록 다양한 정책을 구성할 수 있으므로 데이터를 가장 효과적인 방식으로 패키징하고 전달할 수 있습니다. [자세히 보기](/help/destinations/destination-sdk/functionality/destination-configuration/aggregation-policy.md).

**대상 메타데이터 구성**: 대상 메타데이터 구성은 지정된 대상에서 대상 세그먼트를 프로그래밍 방식으로 생성, 업데이트 및 삭제할 수 있도록 Adobe Experience Platform 내에 정의된 구조화된 설정 및 매개 변수를 나타냅니다. 이 구성은 대상 플랫폼의 마케팅 API 사양에 맞게 대상 메타데이터 템플릿을 사용합니다. 자세한 내용 [대상 메타데이터 구성](/help/destinations/destination-sdk/functionality/audience-metadata-management.md) 및 [사용 가능한 매크로](/help/destinations/destination-sdk/functionality/audience-metadata-management.md#macros).

## D

**대상 구성 끝점**: Adobe Experience Platform의 대상 구성 엔드포인트, 특히 `/authoring/destinations` API 끝점은 대상에 대한 구성을 만들고, 검색하고, 업데이트하고, 삭제하는 데 사용됩니다. 이러한 구성은 Adobe Experience Platform의 데이터가 마케팅 플랫폼, 클라우드 스토리지 서비스 또는 기타 데이터 처리 엔드포인트와 같은 다양한 외부 시스템 또는 대상으로 전달되는 방식을 정의합니다. 자세한 내용 [사용 가능한 구성 옵션](/help/destinations/destination-sdk/functionality/configuration-options.md#destination-configuration) 및 보기 [참조 설명서](/help/destinations/destination-sdk/authoring-api/destination-configuration/create-destination-configuration.md).

**대상 인스턴스**: Experience Platform UI를 통해 생성 및 관리되는 Adobe Experience Platform의 대상 구성에 대한 특정 설정입니다. 여기에는 데이터를 대상에 연결하고 전송하는 데 필요한 모든 매개 변수와 자격 증명이 포함됩니다. 대상에 대한 연결을 설정한 후 다음과 같은 경우 대상 인스턴스 ID를 가져올 수 있습니다. [대상과의 연결 검색](/help/destinations/ui/destination-details-page.md).

![UI 이미지 대상 인스턴스 ID를 가져오는 방법](/help/destinations/destination-sdk/assets/testing-api/get-destination-instance-id.png)

## P

**[!DNL Pebble]템플릿**: A [!DNL Pebble] 템플릿은 Adobe Experience Platform에서 내보낸 데이터를 대상 플랫폼에서 요구하는 형식으로 변환하는 데 사용됩니다. 다음을 사용합니다. [!DNL Pebble] 템플릿 언어: 다음과 같은 함수를 통해 동적 데이터 변환 `filter`, `for`, `if`, 및 `set`. Adobe Experience Platform에는 다음과 같은 추가 사용자 정의 기능이 포함되어 있습니다 `addedSegments` 및 `removedSegments`. 이러한 템플릿은 타임스탬프 및 대상 멤버십과 같은 데이터 요소의 서식을 대상의 사양을 충족하는 데 도움이 됩니다. 자세히 알아보기 [여기](/help/destinations/destination-sdk/functionality/destination-server/message-format.md) 및 [여기](/help/destinations/destination-sdk/functionality/destination-server/templating-specs.md).

**비공개 대상**: 개별 Adobe Experience Platform 고객이 만든 사용자 정의 통합. 이러한 구성 요소는 특정 비즈니스 요구 사항에 맞게 조정되며 고객의 조직 내에서만 액세스할 수 있으므로 데이터 내보내기 구성에 유연성을 제공합니다. 비공개 대상은 Real-Time CDP Ultimate 고객만 사용할 수 있습니다. [자세히 보기](/help/destinations/destination-sdk/overview.md#productized-custom-integrations).

**공개 대상**: Adobe Experience Platform 카탈로그에서 공개적으로 사용 가능한 통합. 이러한 대상은 표준화되고 브랜딩되며 사전 구성된 매개 변수를 제공하여 고객 설정을 단순화합니다. Adobe Experience Platform을 사용하는 모든 고객이 액세스할 수 있습니다. [자세히 보기](/help/destinations/destination-sdk/overview.md#productized-custom-integrations).

## S

**셀프서비스 설명서 템플릿**: 셀프서비스 설명서 템플릿은 대상을 문서화하는 데 사용할 수 있는 구조화된 형식을 제공합니다. 여기에는 개요, 사용 사례, 사전 요구 사항, 지원되는 ID, 대상, 내보내기 유형 및 빈도에 대한 섹션과 대상에 연결하는 단계, 대상을 활성화하는 단계 및 속성을 매핑하는 단계가 포함됩니다. 이 템플릿을 사용하면 대상 사용을 빠르게 시작하고 제공된 사용 사례를 이해할 수 있으므로 포괄적이고 일관된 설명서를 보장할 수 있습니다. 자세한 내용 [대상을 문서화하는 방법](/help/destinations/destination-sdk/docs-framework/documentation-instructions.md), [최신 셀프서비스 설명서 템플릿 다운로드](/help/destinations/destination-sdk/assets/docs-framework/yourdestination-template.zip), 및 [렌더링 방법 보기](/help/destinations/destination-sdk/docs-framework/self-service-template.md).

## T

**템플릿 사양 및 템플릿 전략**: 템플릿 사양은 Adobe Experience Platform에서 대상으로 전송된 HTTP 요청의 형식을 지정하는 데 사용되는 구성입니다. XDM 스키마의 프로필 속성 필드를 대상 플랫폼에서 지원하는 형식으로 변환합니다. 다음과 유사한 템플릿 언어 사용 [!DNL Jinja], 이러한 사양을 사용하면 특정 규칙 및 입력 데이터에 따라 동적 데이터 변환이 가능합니다. [자세히 알아보기](/help/destinations/destination-sdk/functionality/destination-server/templating-specs.md).

**API 테스트**: 테스트 API를 사용하면 게시 요청을 제출하기 전에 대상 구성의 유효성을 검사할 수 있습니다. 샘플 프로필을 생성하고 데이터 흐름을 테스트하는 도구를 제공하여 구성이 대상의 요구 사항과 일치하도록 합니다. API는 스트리밍 및 파일 기반(일괄 처리) 대상을 모두 지원하여 데이터를 시뮬레이션하고 설정 프로세스에서 잠재적인 문제를 해결하는 방법을 제공합니다. 의 테스트 API에 대해 자세히 알아보십시오. [스트리밍](/help/destinations/destination-sdk/testing-api/streaming-destinations/streaming-destination-testing-overview.md) 및 [파일 기반 대상](/help/destinations/destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md).

**변환 템플릿**: 변환 템플릿은 Adobe XDM 스키마에서 대상의 예상 형식으로 데이터 형식을 사용자 정의합니다. [자세히 알아보기](/help/destinations/destination-sdk/functionality/destination-server/message-format.md).