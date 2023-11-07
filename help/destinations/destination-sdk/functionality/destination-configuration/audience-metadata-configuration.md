---
description: Destination SDK으로 빌드된 대상에 대한 대상 메타데이터 설정을 구성하는 방법에 대해 알아봅니다.
title: 대상 메타데이터 구성
exl-id: ae71df4f-b753-4084-835f-03559b4986cb
source-git-commit: 82ba4e62d5bb29ba4fef22c5add864a556e62c12
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 3%

---

# 대상 메타데이터 구성

Experience Platform에서 대상으로 데이터를 내보낼 때 Experience Platform과 대상 간에 대상 이름 또는 대상 ID와 같은 특정 대상 메타데이터가 공유되어야 할 수 있습니다.

Destination SDK은 대상 플랫폼에서 대상을 프로그래밍 방식으로 생성, 업데이트 또는 삭제하는 데 사용할 수 있는 도구를 제공합니다.

이 구성 요소가 Destination SDK으로 만든 통합에 어디에 맞는지 이해하려면 의 다이어그램을 참조하십시오. [구성 옵션](../configuration-options.md) 설명서 또는 방법에 대한 안내서 참조 [Destination SDK을 사용하여 스트리밍 대상 구성](../../guides/configure-destination-instructions.md#create-destination-configuration).

다음을 통해 대상 메타데이터 템플릿을 구성할 수 있습니다. `/authoring/audience-templates` 엔드포인트. 대상 메타데이터 구성을 만든 후 다음을 사용할 수 있습니다. `/authoring/destinations` 를 구성하는 엔드포인트 `audienceMetadataConfig` 섹션. 이 섹션에서는 대상 템플릿에 매핑해야 하는 대상 메타데이터를 대상에 알려줍니다.

이 페이지에 표시된 구성 요소를 구성할 수 있는 자세한 API 호출 예는 다음 API 참조 페이지를 참조하십시오.

* [대상 구성 만들기](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [대상 구성 업데이트](../../authoring-api/destination-configuration/update-destination-configuration.md)
* [대상자 템플릿 만들기](../../metadata-api/create-audience-template.md)
* [대상자 템플릿 업데이트](../../metadata-api/update-audience-template.md)

>[!IMPORTANT]
>
>Destination SDK에서 지원하는 모든 매개변수 이름 및 값은 다음과 같습니다. **대소문자 구분**. 대소문자 구분 오류를 방지하려면 설명서에 표시된 대로 매개 변수 이름과 값을 정확히 사용하십시오.

## 지원되는 통합 유형 {#supported-integration-types}

이 페이지에 설명된 기능을 지원하는 통합 유형에 대한 자세한 내용은 아래 표를 참조하십시오.

| 통합 유형 | 기능 지원 |
|---|---|
| 실시간(스트리밍) 통합 | 예 |
| 파일 기반 (일괄 처리) 통합 | 예 |

## 지원되는 매개 변수 {#supported-parameters}

대상 메타데이터 구성을 생성할 때 아래 표에 설명된 매개 변수를 사용하여 대상 매핑 설정을 구성할 수 있습니다.

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
| `mapExperiencePlatformSegmentName` | 부울 | 다음 여부를 나타냅니다. [[!UICONTROL 매핑 ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling) 대상 활성화 워크플로의 값은 Experience Platform 대상 이름이어야 합니다. |
| `mapExperiencePlatformSegmentId` | 부울 | 다음 여부를 나타냅니다. [[!UICONTROL 매핑 ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling) 대상 활성화 워크플로의 값은 Experience Platform 대상 ID여야 합니다. |
| `mapUserInput` | 부울 | 다음에 대한 사용자 입력 활성화 또는 비활성화 [[!UICONTROL 매핑 ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling) 대상 활성화 워크플로의 값입니다. 로 설정된 경우 `true`, `audienceTemplateId` 이(가) 있을 수 없습니다. |
| `audienceTemplateId` | 부울 | 다음 `instanceId` / [대상 메타데이터 템플릿](../../metadata-api/create-audience-template.md) 대상에 사용됩니다. |

{style="table-layout:auto"}

## 다음 단계 {#next-steps}

이 문서를 읽은 후에는 대상에 대한 대상 메타데이터를 구성하는 방법을 보다 잘 이해할 수 있어야 합니다.

다른 대상 구성 요소에 대한 자세한 내용은 다음 문서를 참조하십시오.

* [고객 인증 구성](customer-authentication.md)
* [OAuth2 인증](oauth2-authorization.md)
* [고객 데이터 필드](customer-data-fields.md)
* [UI 속성](ui-attributes.md)
* [스키마 구성](schema-configuration.md)
* [ID 네임스페이스 구성](identity-namespace-configuration.md)
* [지원되는 매핑 구성](supported-mapping-configurations.md)
* [대상 게재](destination-delivery.md)
* [집계 정책](aggregation-policy.md)
* [일괄 처리 구성](batch-configuration.md)
* [과거 프로필 자격 요건](historical-profile-qualifications.md)
