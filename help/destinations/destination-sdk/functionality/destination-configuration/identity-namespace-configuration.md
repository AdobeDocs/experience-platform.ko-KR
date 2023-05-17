---
description: Destination SDK으로 빌드된 대상에 대해 지원되는 Target ID를 구성하는 방법을 알아봅니다.
title: ID 네임스페이스 구성
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 4%

---


# ID 네임스페이스 구성

Experience Platform은 ID 네임스페이스를 사용하여 특정 ID의 유형을 설명합니다. 예를 들어 `Email` 와 같은 값을 식별합니다 `name@email.com` 이메일 주소로.

Destination SDK을 통해 대상을 만들 때 [파트너 스키마 구성](schema-configuration.md) 사용자가 프로필 속성 및 ID를 에 매핑할 수 있도록 대상 플랫폼에서 지원하는 ID 네임스페이스를 정의할 수도 있습니다.

이 경우 대상 프로필 속성 외에 타겟 ID를 선택할 수 있는 선택 사항이 추가되었습니다.

Experience Platform의 ID 네임스페이스에 대한 자세한 내용은 [id 네임스페이스 설명서](../../../../identity-service/namespaces.md).

대상에 대한 ID 네임스페이스를 구성할 때 다음과 같이 대상에서 지원하는 대상 ID 매핑을 미세 조정할 수 있습니다.

* 사용자가 XDM 속성을 ID 네임스페이스에 매핑할 수 있도록 해줍니다.
* 사용자가 매핑할 수 있도록 허용 [표준 id 네임스페이스](../../../../identity-service/namespaces.md#standard) 자신의 ID 네임스페이스에 기여합니다.
* 사용자가 매핑할 수 있도록 허용 [사용자 지정 ID 네임스페이스](../../../../identity-service/namespaces.md#manage-namespaces) 자신의 ID 네임스페이스에 기여합니다.

이 구성 요소가 Destination SDK과 함께 작성된 통합에 어떤 영향을 주는지 이해하려면 [구성 옵션](../configuration-options.md) 설명서 또는 방법에 대한 안내서를 참조하십시오. [Destination SDK을 사용하여 파일 기반 대상 구성](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

를 통해 지원되는 ID 네임스페이스를 구성할 수 있습니다 `/authoring/destinations` 엔드포인트. 이 페이지에 표시된 구성 요소를 구성할 수 있는 자세한 API 호출 예는 다음 API 참조 페이지를 참조하십시오.

* [대상 구성 만들기](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [대상 구성 업데이트](../../authoring-api/destination-configuration/update-destination-configuration.md)

이 문서에서는 대상에 사용할 수 있는 지원되는 모든 ID 네임스페이스 구성 옵션에 대해 설명하고 고객이 Platform UI에서 보게 되는 내용을 보여줍니다.

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

대상이 지원하는 대상 ID를 정의할 때 아래 표에 설명된 매개 변수를 사용하여 해당 동작을 구성할 수 있습니다.

| 매개변수 | 유형 | 필수/선택적 | 설명 |
|---------|----------|---|------|
| `acceptsAttributes` | 부울 | 선택 사항입니다 | 고객이 표준 프로필 속성을 구성 중인 ID에 매핑할 수 있는지 여부를 나타냅니다. |
| `acceptsCustomNamespaces` | 부울 | 선택 사항입니다 | 고객이 사용자 지정 ID 네임스페이스를 구성 중인 ID 네임스페이스에 매핑할 수 있는지 여부를 나타냅니다. |
| `acceptedGlobalNamespaces` | - | 선택 사항입니다 | 다음 항목을 나타냅니다. [표준 id 네임스페이스](../../../../identity-service/namespaces.md#standard) (예: [!UICONTROL IDFA]) 고객은 구성 중인 ID에 매핑할 수 있습니다. |
| `transformation` | 문자열 | 선택 사항입니다 | 를 표시합니다 [[!UICONTROL 변형 적용]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) 소스 필드가 XDM 속성 또는 사용자 지정 id 네임스페이스인 경우 Platform UI에서 확인란을 선택합니다. 이 옵션을 사용하여 내보낼 때 소스 속성을 해시할 수 있습니다. 이 옵션을 사용하려면 값을 로 설정합니다. `sha256(lower($))`. |
| `requiredTransformation` | 문자열 | 선택 사항입니다 | 고객이 이 소스 ID 네임스페이스를 선택하면 [[!UICONTROL 변형 적용]](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) 이 확인란은 매핑에 자동으로 적용되며 고객이 비활성화할 수 없습니다. 이 옵션을 사용하려면 값을 로 설정합니다. `sha256(lower($))`. |

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

어떤 것을 표시해야 합니다 [!DNL Platform] id 고객은 대상으로 내보낼 수 있습니다. 몇 가지 예는 다음과 같습니다 [!DNL Experience Cloud ID], 해시된 이메일, 장치 ID ([!DNL IDFA], [!DNL GAID]). 이러한 값은 [!DNL Platform] 고객이 대상의 ID 네임스페이스에 매핑할 수 있는 ID 네임스페이스입니다.

ID 네임스페이스에는 1-1의 서신이 필요하지 않습니다 [!DNL Platform] 및 대상을 선택합니다.
예를 들어 고객이 [!DNL Platform] [!DNL IDFA] 네임스페이스에 [!DNL IDFA] 대상의 네임스페이스이거나, 동일한 네임스페이스를 매핑할 수 있습니다 [!DNL Platform] [!DNL IDFA] 네임스페이스 [!DNL Customer ID] 네임스페이스가 대상에 있습니다.

에서 ID에 대해 자세히 알아보십시오 [id 네임스페이스 개요](../../../../identity-service/namespaces.md).

## 매핑 고려 사항

고객이 소스 ID 네임스페이스를 선택하고 대상 매핑을 선택하지 않으면 Platform에서 자동으로 동일한 이름의 속성으로 대상 매핑을 채웁니다.

## 선택적 소스 필드 해싱 구성

Experience Platform 고객은 데이터를 해시된 형식 또는 일반 텍스트로 플랫폼으로 수집하도록 선택할 수 있습니다. 대상 플랫폼에서 해시된 데이터와 해시되지 않은 데이터를 모두 허용하는 경우 대상으로 내보낼 때 플랫폼에서 소스 필드 값을 해시해야 하는지 여부를 선택할 수 있는 옵션을 제공할 수 있습니다.

아래 구성에서는 선택 사항을 사용할 수 있습니다 [변형 적용](../../../ui/activate-segment-streaming-destinations.md#apply-transformation) 옵션이 포함되어 있습니다.

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

해시되지 않은 소스 속성을 대상이 해시될 대상 속성에 매핑하는 경우(예: `email_lc_sha256` 또는 `phone_sha256`), 을(를) 선택합니다. **변형 적용** Adobe Experience Platform이 활성화 시 소스 속성을 자동으로 해시하도록 하는 옵션입니다.

## 필수 소스 필드 해싱 구성

대상이 해시된 데이터만 수락하는 경우 내보낸 속성을 Platform에서 자동으로 해시하도록 구성할 수 있습니다. 아래 구성은 **변형 적용** 선택 사항 `Email` 및 `Phone` ID가 매핑됩니다.

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

이 문서를 읽은 후에는 Destination SDK으로 빌드된 대상에 대해 ID 네임스페이스를 구성하는 방법을 더 잘 이해할 수 있어야 합니다.

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
* [내역 프로필 자격](historical-profile-qualifications.md)
