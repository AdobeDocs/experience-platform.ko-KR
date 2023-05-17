---
description: Experience Platform이 스트리밍 대상에서 반환한 다양한 유형의 오류를 처리하는 방법과 대상 플랫폼으로 데이터를 다시 보내는 방법을 알아봅니다.
title: Destination SDK으로 빌드된 스트리밍 대상에 대한 속도 제한 및 다시 시도 정책
source-git-commit: 8c8026b1180775dddd9517fc88727749678a5613
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# Destination SDK으로 빌드된 스트리밍 대상에 대한 속도 제한 및 다시 시도 정책

파트너가 빌드한 대상은 다양한 오류를 반환하고 다양한 속도 제한 정책을 가질 수 있습니다. 이 페이지에서는 Experience Platform이 스트리밍 대상에서 반환되는 다양한 유형의 오류를 처리하는 방법을 설명합니다.

Destination SDK을 사용하여 대상을 구성할 때 두 집계 유형 중에서 선택할 수 있습니다. [최상의 작업 집계](../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation) 및 [구성 가능한 합계](../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation). 선택한 합계 유형에 따라 Experience Platform이 오류 및 비율 제한을 처리하는 방법 아래의 를 참조하십시오.

## 최상의 노력 집계 {#best-effort-aggregation}

실패한 대상에 대한 모든 HTTP 호출의 경우 Experience Platform은 첫 번째 호출 직후 다시 호출을 시도합니다. 두 번째 시도에서 여전히 호출이 실패하면 Experience Platform은 호출을 삭제하고 세 번째 다시 시도하지 않습니다.

## 구성 가능한 집계 {#configurable-aggregation}

구성 가능한 집계를 사용하여 설정된 대상 플랫폼의 경우 Experience Platform은 플랫폼에서 반환한 오류 유형을 구별합니다.

* 플랫폼으로 데이터를 전송하기 위해 Experience Platform이 다시 시도하는 오류:
   * HTTP 응답 코드 420 및 429
   * 500보다 큰 HTTP 응답 코드
* Experience Platform 오류 *포함하지 않음* 플랫폼으로 데이터를 전송하려면 다시 시도하십시오. 플랫폼에서 반환한 다른 모든 항목

### 다시 시도 접근 방법 설명 {#retry-approach}

구성 가능한 집계에 대한 Experience Platform 접근 방식은 아래에 설명되어 있습니다. 이 예에서는 Experience Platform이 분당 50k 이상의 요청을 받는 경우 429 오류 코드를 반환하기 시작하는 대상 플랫폼에 데이터를 전송한다고 가정합니다.

* 1분: Experience Platform은 대상 플랫폼으로 전송하기 위해 프로필과 함께 40k 배치를 집계합니다. Experience Platform은 40k HTTP 요청을 수행하며 모든 것이 성공적으로 수행됩니다.
* 2분: Experience Platform은 프로필과 함께 70k 배치를 집계하여 대상 플랫폼으로 보냅니다. Experience Platform은 70k HTTP 요청을 수행하고 50k가 성공했습니다. 다른 20k는 종단점에서 속도 제한 오류를 수신하고 30분 후에 다시 시도됩니다.
* 3분: Experience Platform은 프로필과 함께 30k 배치를 집계하여 대상 플랫폼으로 보냅니다. Experience Platform은 30k HTTP 요청을 수행하며 모든 요청이 성공했습니다.
* ...
* ...
* 32분: Experience Platform이 2분에 실패한 20k 일괄 처리를 다시 시도합니다. 모든 호출이 성공했습니다.

## 다음 단계 {#next-steps}

이제 Experience Platform이 스트리밍 대상을 구성할 때 선택한 집계 정책에 따라 대상 플랫폼에서 오류 및 비율 제한을 처리하는 방법을 알 수 있습니다. 다음으로, 다음 설명서를 검토할 수 있습니다.

* [대상 구성 테스트](../testing-api/streaming-destinations/streaming-destination-testing-overview.md)
* [Destination SDK에서 작성된 대상을 검토하도록 제출](../guides/submit-destination.md)
