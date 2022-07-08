---
description: 파일 기반 대상 테스트 API는 Destination SDK을 통해 빌드된 파일 기반 대상의 구성을 확인하는 데 사용할 수 있는 엔드포인트 컬렉션입니다.
title: 파일 기반 대상 테스트 API
source-git-commit: d2d362f4b61e04fc2fa4d9cd9db70ed94a850642
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---


# 파일 기반 대상 테스트 API

## 개요 {#overview}

파일 기반 대상 테스트 API는 Destination SDK을 통해 빌드된 파일 기반 대상의 구성을 확인하는 데 사용할 수 있는 엔드포인트 세트입니다.

이러한 도구를 사용하여 먼저 구성을 확인하는 것이 좋습니다 [제출](submit-destination.md) Adobe에 대한 검토 대상입니다.

최상의 테스트 결과를 얻으려면 아래 흐름 다이어그램을 기반으로 이 API를 사용하는 것이 좋습니다.

![권장 대상 테스트 흐름을 보여주는 다이어그램](assets/file-based-testing-flow.png)

각 종단점에서 수행할 수 있는 작업에 대한 간단한 개요를 알려면 아래 섹션을 참조하십시오.

## 샘플 생성 끝점 {#sample-generation-endpoint}

이 종단점은 기존 소스 스키마를 기반으로 샘플 프로필을 생성하는 데 도움이 됩니다.

샘플 프로필은 프로필의 JSON 구조를 이해하는 데 도움이 되는 것입니다. 또한 추가적인 대상 테스트를 위해 자체 프로필 데이터로 사용자 지정할 수 있는 백본을 제공합니다.

자세한 내용은 [전용 설명서](file-based-sample-profile-generation-api.md) 샘플 프로필을 생성하는 방법을 알아봅니다.

## 대상 구성 테스트 끝점 {#destination-configuration-testing-endpoint}

이 종단점은 파일 기반 대상이 올바르게 구성되었는지 테스트하고 구성된 대상에 데이터 흐름의 무결성을 확인하는 데 도움이 됩니다.

를 추가하거나 추가하지 않고 테스트 종단점에 요청을 수행할 수 있습니다 [샘플 프로필](file-based-sample-profile-generation-api.md) 호출 요청에 대해 프로필을 보내지 않는 경우 API가 샘플 프로필을 자동으로 생성하여 요청에 추가합니다.

자세한 내용은 [전용 설명서](file-based-destination-testing-api.md) 샘플 프로필로 대상 구성을 테스트하는 방법을 알아봅니다.

## 활성화 결과 끝점 {#activation-results}

이 종단점은 파일 기반 대상 테스트 결과의 전체 세부 사항을 보는 데 도움이 됩니다.

이 API 종단점은 를 사용할 때와 동일한 결과를 반환합니다 [Flow Service API](../api/update-destination-dataflows.md) 데이터 흐름을 모니터링하려면 다음을 수행하십시오.

자세한 내용은 [전용 설명서](file-based-destination-results-api.md) 자세한 활성화 결과를 보는 방법을 알아봅니다.

## 고객 필드 렌더링 끝점 {#customer-fields-rendering-endpoint}

이 종단점은 템플릿을 시각화하는 데 도움이 됩니다 [고객 데이터 필드](file-based-destination-configuration.md#customer-data-fields) 대상 구성에 정의된 모양은 다음과 같습니다.

종단점은 고객 데이터 필드에 대한 임의 값을 생성하여 응답에서 반환합니다. 이렇게 하면 버킷 이름 또는 폴더 경로와 같은 고객 데이터 필드의 의미 체계 구조를 확인할 수 있습니다.

자세한 내용은 [전용 설명서](file-based-render-template-api.md) 자세한 활성화 결과를 보는 방법을 알아봅니다.