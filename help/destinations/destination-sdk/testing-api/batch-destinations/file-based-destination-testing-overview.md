---
description: 파일 기반 대상 테스트 API를 사용하여 Destination SDK을 통해 빌드된 파일 기반 대상의 구성을 확인하는 방법에 대해 알아봅니다.
title: 파일 기반 대상 테스트 API
exl-id: 2733fd00-af08-4763-a30e-a53ee56c0a19
source-git-commit: adf75720f3e13c066b5c244d6749dd0939865a6f
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---


# 파일 기반 대상 테스트 API 개요

파일 기반 대상 테스트 API는 Destination SDK을 통해 빌드된 파일 기반 대상의 구성을 확인하는 데 사용할 수 있는 엔드포인트 세트입니다.

Adobe에 검토할 대상을 [제출](../../guides/submit-destination.md)하기 전에 이러한 도구를 사용하여 구성을 확인하는 것이 좋습니다.

최상의 테스트 결과를 얻으려면 아래 흐름 다이어그램에 따라 이 API를 사용하는 것이 좋습니다.

![권장 대상 테스트 흐름을 보여 주는 다이어그램](../../assets/testing-api/batch-destinations/file-based-testing-flow.png)

각 엔드포인트가 수행할 수 있는 작업에 대한 간략한 개요는 아래 섹션을 참조하십시오.

## 샘플 프로필 생성 {#generate-sample-profiles}

`/sample-profiles` API 끝점을 사용하여 기존 원본 스키마를 기반으로 하는 샘플 프로필을 생성합니다.

샘플 프로필은 프로필의 JSON 구조를 이해하는 데 도움이 될 수 있습니다. 또한 추가적인 대상 테스트를 위해 자신의 프로필 데이터로 사용자 정의할 수 있는 기본값을 제공합니다.

샘플 프로필을 생성하는 방법을 알아보려면 [전용 설명서](file-based-sample-profile-generation-api.md)를 참조하세요.

## 대상 구성 테스트 {#test-destination-configuration}

`/testing/destinationInstance` API 끝점을 사용하여 파일 기반 대상이 올바르게 구성되었는지 테스트하고 구성된 대상에 대한 데이터 흐름의 무결성을 확인하십시오.

호출에 [샘플 프로필](file-based-sample-profile-generation-api.md)을(를) 추가하거나 추가하지 않고 테스트 끝점을 요청할 수 있습니다. 요청에 프로필을 보내지 않는 경우 API는 샘플 프로필을 자동으로 생성하여 요청에 추가합니다.

샘플 프로필을 사용하여 대상 구성을 테스트하는 방법을 알아보려면 [전용 설명서](file-based-destination-testing-api.md)를 참조하세요.

## 자세한 활성화 결과 보기 {#view-detailed-activation-results}

`/testing/destinationInstance` API 끝점을 사용하여 파일 기반 대상 테스트 결과에 대한 전체 세부 정보를 볼 수 있습니다.

이 API 끝점은 [흐름 서비스 API](../../../api/update-destination-dataflows.md)를 사용하여 데이터 흐름을 모니터링할 때와 동일한 결과를 반환합니다.

자세한 활성화 결과를 확인하는 방법은 [전용 설명서](file-based-destination-results-api.md)를 참조하세요.

## 고객 데이터 필드 렌더링 {#render-customer-data-fields}

대상 구성에 정의된 템플릿화된 [고객 데이터 필드](../../functionality/destination-configuration/customer-data-fields.md)의 모양을 시각화하려면 `/authoring/testing/template/render` API 끝점을 사용하십시오.

API 끝점은 고객 데이터 필드에 대한 무작위 값을 생성하고 응답에서 반환합니다. 버킷 이름 또는 폴더 경로와 같은 고객 데이터 필드의 의미 체계 구조를 확인하는 데 도움이 됩니다.

고객 데이터 필드에 대한 값을 생성하고 시각화하는 방법을 알아보려면 [전용 설명서](file-based-render-template-api.md)를 참조하세요.
