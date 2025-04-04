---
description: Destination SDK으로 빌드된 대상에 대해 지원되는 타겟 ID를 구성하는 방법에 대해 알아봅니다.
title: ID 네임스페이스 구성
exl-id: 30c0939f-b968-43db-b09b-ce5b34349c6e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 3%

---

# ID 네임스페이스 구성

Experience Platform은 id 네임스페이스를 사용하여 특정 id 유형을 설명합니다. 예를 들어 ID 네임스페이스 `Email`은(는) `name@email.com`과(와) 같은 값을 이메일 주소로 식별합니다.

생성하는 대상 유형(스트리밍 또는 파일 기반)에 따라 다음 ID 네임스페이스 요구 사항을 염두에 두십시오.

* Destination SDK을 통해 실시간(스트리밍) 대상을 만들 때 사용자가 프로필 특성과 ID를 매핑할 수 있는 [파트너 스키마를 구성](schema-configuration.md)하는 것 외에도 대상 플랫폼에서 지원하는 *하나 이상의* ID 네임스페이스를 정의해야 합니다. 예를 들어 대상 플랫폼에서 해시된 전자 메일과 [!DNL IDFA]을(를) 수락하는 경우 이러한 두 ID를 [이 문서에 자세히 설명되어 있는](#supported-parameters)(으)로 정의해야 합니다.

  >[!IMPORTANT]
  >
  >대상자를 스트리밍 대상으로 활성화할 때 사용자는 대상 프로필 특성 외에 _하나 이상의 대상 ID_&#x200B;도 매핑해야 합니다. 그렇지 않으면 대상자가 대상 플랫폼에 활성화되지 않습니다.

* Destination SDK을 통해 파일 기반 대상을 만들 때 ID 네임스페이스의 구성은 _선택 사항_&#x200B;입니다.

Experience Platform의 ID 네임스페이스에 대한 자세한 내용은 [ID 네임스페이스 설명서](../../../../identity-service/features/namespaces.md)를 참조하십시오.

대상에 대해 ID 네임스페이스를 구성할 때 다음과 같이 대상에서 지원하는 대상 ID 매핑을 미세 조정할 수 있습니다.

* 사용자가 XDM 속성을 ID 네임스페이스에 매핑할 수 있습니다.
* 사용자가 [표준 ID 네임스페이스](../../../../identity-service/features/namespaces.md#standard)를 자신의 ID 네임스페이스에 매핑하도록 허용합니다.
* 사용자가 [사용자 지정 ID 네임스페이스](../../../../identity-service/features/namespaces.md#manage-namespaces)를 자신의 ID 네임스페이스에 매핑하도록 허용합니다.

이 구성 요소가 Destination SDK으로 만든 통합에 어디에 맞는지 이해하려면 [구성 옵션](../configuration-options.md) 설명서에서 다이어그램을 참조하거나 [Destination SDK을 사용하여 파일 기반 대상을 구성하는 방법](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration)에 대한 안내서를 참조하십시오.

`/authoring/destinations` 끝점을 통해 지원되는 ID 네임스페이스를 구성할 수 있습니다. 이 페이지에 표시된 구성 요소를 구성할 수 있는 자세한 API 호출 예는 다음 API 참조 페이지를 참조하십시오.

* [대상 구성 만들기](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [대상 구성 업데이트](../../authoring-api/destination-configuration/update-destination-configuration.md)

이 문서에서는 대상에 사용할 수 있는 지원되는 모든 ID 네임스페이스 구성 옵션에 대해 설명하고 고객이 Experience Platform UI에서 보게 되는 내용을 보여줍니다.

>[!IMPORTANT]
>
>Destination SDK에서 지원하는 모든 매개 변수 이름과 값은 **대/소문자를 구분합니다**. 대소문자 구분 오류를 방지하려면 설명서에 표시된 대로 매개 변수 이름과 값을 정확히 사용하십시오.

## 지원되는 통합 유형 {#supported-integration-types}

이 페이지에 설명된 기능을 지원하는 통합 유형에 대한 자세한 내용은 아래 표를 참조하십시오.

| 통합 유형 | 기능 지원 |
|---|---|
| 실시간(스트리밍) 통합 | 예(필수) |
| 파일 기반 (일괄 처리) 통합 | 예(선택 사항) |

## 지원되는 매개 변수 {#supported-parameters}

대상이 지원하는 타겟 ID를 정의할 때 아래 표에 설명된 매개 변수를 사용하여 해당 동작을 구성할 수 있습니다.

| 매개변수 | 유형 | 필수/선택적 | 설명 |
|---------|----------|---|------|
| `acceptsAttributes` | 부울 | 선택 사항입니다 | 고객이 표준 프로필 속성을 구성 중인 ID에 매핑할 수 있는지 여부를 나타냅니다. |
| `acceptsCustomNamespaces` | 부울 | 선택 사항입니다 | 고객이 사용자 정의 ID 네임스페이스를 구성 중인 ID 네임스페이스에 매핑할 수 있는지 여부를 나타냅니다. |
| `acceptedGlobalNamespaces` | - | 선택 사항입니다 | 고객이 구성할 ID에 매핑할 수 있는 [표준 ID 네임스페이스](../../../../identity-service/features/namespaces.md#standard)(예: [!UICONTROL IDFA])를 나타냅니다. |
| `transformation` | 문자열 | 선택 사항입니다 | 소스 필드가 XDM 특성이거나 사용자 지정 ID 네임스페이스인 경우 Experience Platform UI에서 [[!UICONTROL 변형 적용]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) 확인란을 표시합니다. 이 옵션을 사용하여 사용자가 내보낼 때 소스 속성을 해시할 수 있도록 합니다. 이 옵션을 사용하려면 값을 `sha256(lower($))`(으)로 설정하십시오. |
| `requiredTransformation` | 문자열 | 선택 사항입니다 | 고객이 이 소스 ID 네임스페이스를 선택하면 [[!UICONTROL 변환 적용]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) 확인란이 매핑에 자동으로 적용되며 고객은 이 확인란을 비활성화할 수 없습니다. 이 옵션을 사용하려면 값을 `sha256(lower($))`(으)로 설정하십시오. |

{style="table-layout:auto"}


```json
"identityNamespaces":{
      "external_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "acceptedGlobalNamespaces":{
            "Email":{
            }
         }
      },
      "another_id":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true
      }
   }
```

고객이 대상으로 내보낼 수 있는 [!DNL Experience Platform] ID를 나타내야 합니다. 일부 예로는 [!DNL Experience Cloud ID], 해시된 이메일, 장치 ID([!DNL IDFA], [!DNL GAID])가 있습니다. 이 값은 고객이 대상에서 ID 네임스페이스에 매핑할 수 있는 [!DNL Experience Platform] ID 네임스페이스입니다.

ID 네임스페이스에는 [!DNL Experience Platform]과(와) 대상 간에 일대일 응답이 필요하지 않습니다.
예를 들어 고객은 대상의 [!DNL IDFA] 네임스페이스에 [!DNL Experience Platform] [!DNL IDFA] 네임스페이스를 매핑하거나 대상의 [!DNL Customer ID] 네임스페이스에 동일한 [!DNL Experience Platform] [!DNL IDFA] 네임스페이스를 매핑할 수 있습니다.

[ID 네임스페이스 개요](../../../../identity-service/features/namespaces.md)에서 ID에 대해 자세히 알아보세요.

## 매핑 고려 사항

고객이 소스 ID 네임스페이스를 선택하고 대상 매핑을 선택하지 않으면 Experience Platform은 자동으로 대상 매핑을 동일한 이름의 속성으로 채웁니다.

## 선택적 소스 필드 해시 구성

Experience Platform 고객은 데이터를 해시된 형식 또는 일반 텍스트로 Experience Platform에 수집하도록 선택할 수 있습니다. 대상 플랫폼에서 해시된 데이터와 해시되지 않은 데이터를 모두 허용하는 경우 고객에게 Experience Platform을 대상으로 내보낼 때 소스 필드 값을 해시할지 여부를 선택하는 옵션을 제공할 수 있습니다.

아래 구성은 매핑 단계에서 Experience Platform UI의 선택적 [변환 적용](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) 옵션을 활성화합니다.

```json {line-numbers="true" highlight="5"}
"identityNamespaces":{
      "Customer_contact":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation": "sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
            },
            "Phone":{
            }
         }
      }
   }
```

해시되지 않은 소스 필드를 사용할 때 이 옵션을 선택하면 Adobe Experience Platform에서 활성화 시 해당 필드를 자동으로 해시할 수 있습니다.

해시되지 않은 소스 특성을 대상이 해시될 것으로 예상하는 대상 특성(예: `email_lc_sha256` 또는 `phone_sha256`)에 매핑할 때 **변환 적용** 옵션을 선택하여 Adobe Experience Platform이 활성화 시 소스 특성을 자동으로 해시하도록 합니다.

## 필수 소스 필드 해시 구성

대상에서 해시된 데이터만 허용하는 경우 내보낸 속성을 Experience Platform에서 자동으로 해시하도록 구성할 수 있습니다. 아래 구성은 `Email` 및 `Phone` ID가 매핑될 때 **변환 적용** 옵션을 자동으로 확인합니다.

```json {line-numbers="true" highlight="8,11"}
"identityNamespaces":{
      "Customer_contact":{
         "acceptsAttributes":true,
         "acceptsCustomNamespaces":true,
         "transformation": "sha256(lower($))",
         "acceptedGlobalNamespaces":{
            "Email":{
               "requiredTransformation": "sha256(lower($))"
            },
            "Phone":{
               "requiredTransformation": "sha256(lower($))"
            }
         }
      }
   }
```

## 다음 단계 {#next-steps}

이 문서를 읽은 후에는 Destination SDK으로 작성한 대상에 대해 ID 네임스페이스를 구성하는 방법을 더 잘 이해할 수 있어야 합니다.

다른 대상 구성 요소에 대한 자세한 내용은 다음 문서를 참조하십시오.

* [고객 인증](customer-authentication.md)
* [OAuth2 인증](oauth2-authorization.md)
* [고객 데이터 필드](customer-data-fields.md)
* [UI 속성](ui-attributes.md)
* [스키마 구성](schema-configuration.md)
* [ID 네임스페이스 구성](identity-namespace-configuration.md)
* [지원되는 매핑 구성](supported-mapping-configurations.md)
* [대상 게재](destination-delivery.md)
* [대상 메타데이터 구성](audience-metadata-configuration.md)
* [집계 정책](aggregation-policy.md)
* [일괄 처리 구성](batch-configuration.md)
* [과거 프로필 자격 요건](historical-profile-qualifications.md)
