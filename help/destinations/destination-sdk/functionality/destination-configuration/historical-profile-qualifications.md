---
description: Destination SDK으로 빌드된 대상에서 지원하는 내역 프로필 자격에 대해 알아봅니다.
title: 내역 프로필 자격
source-git-commit: 65a658208b48a50184e55a6d64cdf7ad6de0f04f
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 1%

---


# 내역 프로필 자격

Destination SDK을 통해 생성된 모든 대상은 기본적으로 이전 프로필 자격을 지원합니다. 즉, 사용자가 대상에 대해 활성화 데이터 플로우를 처음 설정할 때 첫 번째 내보내기에 해당 세그먼트에 대해 자격이 있는 세그먼트의 모든 구성원이 포함됩니다.

이 동작은 `"backfillHistoricalProfileData":true` 매개 변수 를 참조하십시오.

>[!IMPORTANT]
>
>Destination SDK 및 `backfillHistoricalProfileData` 매개 변수는 사용자가 구성할 수 없습니다.

## 지원되는 통합 유형 {#supported-integration-types}

이 페이지에 설명된 기능을 지원하는 통합 유형에 대한 자세한 내용은 아래 표를 참조하십시오.

| 통합 유형 | 기능 지원 |
|---|---|
| 실시간(스트리밍) 통합 | 예 |
| 파일 기반(일괄 처리) 통합 | 예 |



<!-- 
|Parameter | Type | Description|
|---------|----------|------|
|`backfillHistoricalProfileData` | Boolean | Controls whether historical profile data is exported when segments are activated to the destination. <br> <ul><li> `true`: [!DNL Platform] sends the historical user profiles that qualified for the segment before the segment is activated. </li><li> `false`: [!DNL Platform] only includes user profiles that qualify for the segment after the segment is activated. </li></ul> |

{style="table-layout:auto"} -->


## 다음 단계 {#next-steps}

이 문서를 읽은 후에는 세그먼트를 대상으로 처음 내보낼 때 Experience Platform에서 활성화된 세그먼트에 자격을 부여받은 모든 프로필의 내역 모집단을 자동으로 내보내내는지 확인해야 합니다. 이 옵션은 Destination SDK 또는 Experience Platform UI에서 구성할 수 없습니다.

다른 대상 구성 요소에 대해 자세히 알려면 다음 문서를 참조하십시오.

* [고객 인증](customer-authentication.md)
* [OAuth2 인증](oauth2-authentication.md)
* [고객 데이터 필드](customer-data-fields.md)
* [UI 속성](ui-attributes.md)
* [스키마 구성](schema-configuration.md)
* [ID 네임스페이스 구성](identity-namespace-configuration.md)
* [지원되는 매핑 구성](supported-mapping-configurations.md)
* [대상 게재](destination-delivery.md)
* [대상 메타데이터 구성](audience-metadata-configuration.md)
* [집계 정책](aggregation-policy.md)
* [배치 구성](batch-configuration.md)