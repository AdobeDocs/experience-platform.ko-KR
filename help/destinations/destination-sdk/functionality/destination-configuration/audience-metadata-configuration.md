---
description: Destination SDK으로 빌드된 대상에 대한 대상 메타데이터 설정을 구성하는 방법을 알아봅니다.
title: 대상 메타데이터 구성
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 2%

---


# 대상 메타데이터 구성

데이터를 Experience Platform에서 대상으로 내보낼 때 Experience Platform과 대상 간에 공유하려면 세그먼트 이름 또는 세그먼트 ID와 같은 특정 대상 메타데이터가 필요할 수 있습니다.

Destination SDK은 대상 플랫폼에서 대상을 프로그래밍 방식으로 만들거나, 업데이트하거나, 삭제하는 데 사용할 수 있는 도구를 제공합니다.

이 구성 요소가 Destination SDK과 함께 작성된 통합에 어떤 영향을 주는지 이해하려면 [구성 옵션](../configuration-options.md) 설명서 또는 방법에 대한 안내서를 참조하십시오. [Destination SDK을 사용하여 스트리밍 대상 구성](../../guides/configure-destination-instructions.md#create-destination-configuration).

를 통해 대상 메타데이터 템플릿을 구성할 수 있습니다 `/authoring/audience-templates` 엔드포인트. 대상 메타데이터 구성을 만든 후 `/authoring/destinations` 구성할 엔드포인트 `audienceMetadataConfig` 섹션을 참조하십시오. 이 섹션에서는 대상에 대상 템플릿에 매핑해야 하는 세그먼트 메타데이터를 알려줍니다.

이 페이지에 표시된 구성 요소를 구성할 수 있는 자세한 API 호출 예는 다음 API 참조 페이지를 참조하십시오.

* [대상 구성 만들기](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [대상 구성 업데이트](../../authoring-api/destination-configuration/update-destination-configuration.md)
* [대상 템플릿 만들기](../../metadata-api/create-audience-template.md)
* [대상 템플릿 업데이트](../../metadata-api/update-audience-template.md)

>[!IMPORTANT]
>
>Destination SDK에서 지원하는 모든 매개 변수 이름 및 값은 **대소문자 구분**. 대/소문자 구분 오류가 발생하지 않도록 하려면 설명서에 표시된 대로 매개 변수 이름과 값을 정확히 사용하십시오.

## 지원되는 통합 유형 {#supported-integration-types}

이 페이지에 설명된 기능을 지원하는 통합 유형에 대한 자세한 내용은 아래 표를 참조하십시오.

| 통합 유형 | 기능 지원 |
|---|---|
| 실시간(스트리밍) 통합 | 예 |
| 파일 기반(일괄 처리) 통합 | 예 |

## 지원되는 매개 변수 {#supported-parameters}

대상 메타데이터 구성을 만들 때 아래 표에 설명된 매개 변수를 사용하여 세그먼트 매핑 설정을 구성할 수 있습니다.

```json
  "audienceMetadataConfig":{
   "mapExperiencePlatformSegmentName":false,
   "mapExperiencePlatformSegmentId":false,
   "mapUserInput":false,
   "audienceTemplateId":"YOUR_AUDIENCE_TEMPLATE_ID"
}
```

| 매개변수 | 유형 | 설명 |
|---------|----------|------|
| `mapExperiencePlatformSegmentName` | 부울 | 다음을 [[!UICONTROL 매핑 ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling) 대상 활성화 워크플로우의 값은 Experience Platform 세그먼트 이름이어야 합니다. |
| `mapExperiencePlatformSegmentId` | 부울 | 다음을 [[!UICONTROL 매핑 ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling) 대상 활성화 워크플로우의 값은 Experience Platform 세그먼트 ID여야 합니다. |
| `mapUserInput` | 부울 | 에 대한 사용자 입력을 활성화하거나 비활성화합니다 [[!UICONTROL 매핑 ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling) 대상 활성화 워크플로우의 값입니다. 로 설정된 경우 `true`, `audienceTemplateId` 없습니다. |
| `audienceTemplateId` | 부울 | 다음 `instanceId` 의 [대상 메타데이터 템플릿](../../metadata-api/create-audience-template.md) 대상에 사용됩니다. |

{style="table-layout:auto"}

## 다음 단계 {#next-steps}

이 문서를 읽은 후에는 대상에 대한 대상 메타데이터를 구성하는 방법을 더 잘 이해할 수 있어야 합니다.

다른 대상 구성 요소에 대해 자세히 알려면 다음 문서를 참조하십시오.

* [고객 인증 구성](customer-authentication.md)
* [OAuth2 인증](oauth2-authentication.md)
* [고객 데이터 필드](customer-data-fields.md)
* [UI 속성](ui-attributes.md)
* [스키마 구성](schema-configuration.md)
* [ID 네임스페이스 구성](identity-namespace-configuration.md)
* [지원되는 매핑 구성](supported-mapping-configurations.md)
* [대상 게재](destination-delivery.md)
* [집계 정책](aggregation-policy.md)
* [배치 구성](batch-configuration.md)
* [내역 프로필 자격](historical-profile-qualifications.md)