---
description: 내보낸 데이터의 위치와 데이터가 도착하는 위치에서 사용되는 인증 규칙을 나타내기 위해 Destination SDK으로 작성한 대상에 대한 대상 게재 설정을 구성하는 방법에 대해 알아봅니다.
title: 대상 게재
exl-id: ade77b6b-4b62-4b17-a155-ef90a723a4ad
source-git-commit: 8f430fa3949c19c22732ff941e8c9b07adb37e1f
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 2%

---

# 대상 게재

대상으로 내보낸 데이터의 위치를 더 세밀하게 제어할 수 있도록 Destination SDK에서 대상 게재 설정을 지정할 수 있습니다.

대상 게재 섹션은 내보낸 데이터의 위치와 데이터가 도착하는 위치에서 사용되는 인증 규칙을 나타냅니다.

<!-- When configuring a destination, you must specify an authentication rule and one or more `destinationServerId` parameters, corresponding to the destination servers that define where the data will be delivered to. In most cases, the authentication rule that you should use is `CUSTOMER_AUTHENTICATION`.  -->

이 구성 요소가 Destination SDK으로 만든 통합에 어디에 맞는지 이해하려면 의 다이어그램을 참조하십시오. [구성 옵션](../configuration-options.md) 설명서 또는 다음 대상 구성 개요 페이지를 참조하십시오.

* [Destination SDK을 사용하여 스트리밍 대상 구성](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Destination SDK을 사용하여 파일 기반 대상 구성](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

다음을 통해 대상 게재 설정을 구성할 수 있습니다. `/authoring/destinations` 엔드포인트. 이 페이지에 표시된 구성 요소를 구성할 수 있는 자세한 API 호출 예는 다음 API 참조 페이지를 참조하십시오.

* [대상 구성 만들기](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [대상 구성 업데이트](../../authoring-api/destination-configuration/update-destination-configuration.md)

이 문서에서는 대상에 사용할 수 있는 지원되는 모든 대상 게재 옵션에 대해 설명합니다.

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

대상 게재 설정을 구성할 때 아래 표에 설명된 매개 변수를 사용하여 내보낸 데이터를 전송해야 하는 위치를 정의할 수 있습니다.

| 매개변수 | 유형 | 설명 |
|---------|----------|------|
| `authenticationRule` | 문자열 | 방법을 나타냅니다. [!DNL Platform] 대상에 연결해야 합니다. 지원되는 값:<ul><li>`CUSTOMER_AUTHENTICATION`: Platform 고객이 설명된 인증 방법을 통해 시스템에 로그인한 경우 이 옵션을 사용합니다 [여기](customer-authentication.md).</li><li>`PLATFORM_AUTHENTICATION`: Adobe과 대상 및 간 글로벌 인증 시스템이 있는 경우 이 옵션을 사용합니다. [!DNL Platform] 고객은 대상에 연결하기 위해 인증 자격 증명을 제공할 필요가 없습니다. 이 경우 다음을 사용하여 자격 증명 개체를 만들어야 합니다 [자격 증명 API](../../credentials-api/create-credential-configuration.md) 구성. </li><li>`NONE`: 데이터를 대상 플랫폼으로 보내는 데 인증이 필요하지 않은 경우 이 옵션을 사용합니다. </li></ul> |
| `destinationServerId` | 문자열 | 다음 `instanceId` / [대상 서버](../../authoring-api/destination-server/create-destination-server.md) 데이터를 내보내려는 대상. |
| `deliveryMatchers.type` | 문자열 | <ul><li>파일 기반 대상에 대한 대상 전달을 구성할 때 항상 이 설정을 로 설정하십시오. `SOURCE`.</li><li>스트리밍 대상에 대한 대상 게재를 구성할 때 `deliveryMatchers` 섹션은 필수가 아닙니다.</li></ul> |
| `deliveryMatchers.value` | 문자열 | <ul><li>파일 기반 대상에 대한 대상 전달을 구성할 때 항상 이 설정을 로 설정하십시오. `batch`.</li><li>스트리밍 대상에 대한 대상 게재를 구성할 때 `deliveryMatchers` 섹션은 필수가 아닙니다.</li></ul> |

{style="table-layout:auto"}

## 스트리밍 대상에 대한 대상 게재 설정 {#destination-delivery-streaming}

아래 예는 스트리밍 대상에 대한 대상 게재 설정을 구성하는 방법을 보여줍니다. 다음 사항에 주의하십시오. `deliveryMatchers` 스트리밍 대상에는 섹션이 필요하지 않습니다.

>[!BEGINSHADEBOX]

```json
{
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ]
}
```

>[!ENDSHADEBOX]

## 파일 기반 대상에 대한 대상 게재 설정 {#destination-delivery-file-based}

아래 예제는 파일 기반 대상에 대해 대상 게재 설정을 구성하는 방법을 보여 줍니다. 다음 사항에 주의하십시오. `deliveryMatchers` 파일 기반 대상에는 섹션이 필요합니다.

>[!BEGINSHADEBOX]

```json
{
   "destinationDelivery":[
      {
         "deliveryMatchers":[
            {
               "type":"SOURCE",
               "value":[
                  "batch"
               ]
            }
         ],
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ]
}
```

>[!ENDSHADEBOX]

## 다음 단계 {#next-steps}

이 문서를 읽은 후에는 스트리밍 및 파일 기반 대상 모두에 대해 대상에서 데이터를 내보낼 위치를 구성하는 방법을 더 잘 이해할 수 있어야 합니다.

다른 대상 구성 요소에 대한 자세한 내용은 다음 문서를 참조하십시오.

* [고객 인증](customer-authentication.md)
* [OAuth2 인증](oauth2-authorization.md)
* [UI 속성](ui-attributes.md)
* [고객 데이터 필드](customer-data-fields.md)
* [스키마 구성](schema-configuration.md)
* [ID 네임스페이스 구성](identity-namespace-configuration.md)
* [지원되는 매핑 구성](supported-mapping-configurations.md)
* [대상 메타데이터 구성](audience-metadata-configuration.md)
* [집계 정책](aggregation-policy.md)
* [일괄 처리 구성](batch-configuration.md)
* [과거 프로필 자격 요건](historical-profile-qualifications.md)
