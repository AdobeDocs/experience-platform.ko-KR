---
description: Destination SDK으로 빌드된 대상에 대한 대상 전달 설정을 구성하여 내보낸 데이터의 위치와 데이터가 도착하는 위치에서 사용되는 인증 규칙을 표시하는 방법을 알아봅니다.
title: 대상 게재
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 1%

---


# 대상 게재

대상으로 내보낸 데이터의 위치를 보다 세밀하게 제어하려면 Destination SDK에서 대상 전달 설정을 지정할 수 있습니다.

대상 게재 섹션은 내보낸 데이터가 이동하는 위치와 데이터가 도착하는 위치에서 사용되는 인증 규칙을 나타냅니다.

<!-- When configuring a destination, you must specify an authentication rule and one or more `destinationServerId` parameters, corresponding to the destination servers that define where the data will be delivered to. In most cases, the authentication rule that you should use is `CUSTOMER_AUTHENTICATION`.  -->

이 구성 요소가 Destination SDK과 함께 작성된 통합에 어떤 영향을 주는지 이해하려면 [구성 옵션](../configuration-options.md) 설명서나 다음 대상 구성 개요 페이지를 참조하십시오.

* [Destination SDK을 사용하여 스트리밍 대상 구성](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Destination SDK을 사용하여 파일 기반 대상 구성](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

를 통해 대상 게재 설정을 구성할 수 있습니다 `/authoring/destinations` 엔드포인트. 이 페이지에 표시된 구성 요소를 구성할 수 있는 자세한 API 호출 예는 다음 API 참조 페이지를 참조하십시오.

* [대상 구성 만들기](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [대상 구성 업데이트](../../authoring-api/destination-configuration/update-destination-configuration.md)

이 문서에서는 대상에 사용할 수 있는 지원되는 모든 대상 배달 옵션에 대해 설명합니다.

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

대상 게재 설정을 구성할 때 아래 표에 설명된 매개 변수를 사용하여 내보낸 데이터를 보낼 위치를 정의할 수 있습니다.

| 매개변수 | 유형 | 설명 |
|---------|----------|------|
| `authenticationRule` | 문자열 | 방법을 나타냅니다. [!DNL Platform] 대상에 연결해야 합니다. 지원되는 값:<ul><li>`CUSTOMER_AUTHENTICATION`: Platform 고객이 설명된 인증 방법을 통해 시스템에 로그인하는 경우 이 옵션을 사용합니다 [여기](customer-authentication.md).</li><li>`PLATFORM_AUTHENTICATION`: Adobe과 대상 및 대상 간에 글로벌 인증 시스템이 있는 경우 이 옵션을 사용합니다 [!DNL Platform] 고객은 대상에 연결하기 위해 인증 자격 증명을 제공할 필요가 없습니다. 이 경우 [자격 증명 API](../../credentials-api/create-credential-configuration.md) 구성. </li><li>`NONE`: 대상 플랫폼으로 데이터를 전송하는 데 인증이 필요하지 않으면 이 옵션을 사용합니다. </li></ul> |
| `destinationServerId` | 문자열 | 다음 `instanceId` 의 [대상 서버](../../authoring-api/destination-server/create-destination-server.md) 로 데이터를 내보낼 때 사용합니다. |
| `deliveryMatchers.type` | 문자열 | <ul><li>파일 기반 대상에 대한 대상 전달을 구성할 때는 항상 다음 설정을 `SOURCE`.</li><li>스트리밍 대상에 대한 대상 전달을 구성할 때 `deliveryMatchers` 섹션은 필요하지 않습니다.</li></ul> |
| `deliveryMatchers.value` | 문자열 | <ul><li>파일 기반 대상에 대한 대상 전달을 구성할 때는 항상 다음 설정을 `batch`.</li><li>스트리밍 대상에 대한 대상 전달을 구성할 때 `deliveryMatchers` 섹션은 필요하지 않습니다.</li></ul> |

{style="table-layout:auto"}

## 스트리밍 대상에 대한 대상 게재 설정 {#destination-delivery-streaming}

아래 예는 스트리밍 대상에 대해 대상 게재 설정을 구성하는 방법을 보여줍니다. 다음 사항에 유의하십시오. `deliveryMatchers` 스트리밍 대상에 대해서는 섹션이 필요하지 않습니다.

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

아래 예는 파일 기반 대상에 대해 대상 게재 설정을 구성하는 방법을 보여줍니다. 다음 사항에 유의하십시오. `deliveryMatchers` 파일 기반 대상에 대한 섹션이 필요합니다.

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

이 문서를 읽은 후에는 스트리밍 및 파일 기반 대상 모두에 대해 대상을 내보낼 위치를 구성하는 방법을 이해할 수 있어야 합니다.

다른 대상 구성 요소에 대해 자세히 알려면 다음 문서를 참조하십시오.

* [고객 인증](customer-authentication.md)
* [OAuth2 인증](oauth2-authentication.md)
* [UI 속성](ui-attributes.md)
* [고객 데이터 필드](customer-data-fields.md)
* [스키마 구성](schema-configuration.md)
* [ID 네임스페이스 구성](identity-namespace-configuration.md)
* [지원되는 매핑 구성](supported-mapping-configurations.md)
* [대상 메타데이터 구성](audience-metadata-configuration.md)
* [집계 정책](aggregation-policy.md)
* [배치 구성](batch-configuration.md)
* [내역 프로필 자격](historical-profile-qualifications.md)