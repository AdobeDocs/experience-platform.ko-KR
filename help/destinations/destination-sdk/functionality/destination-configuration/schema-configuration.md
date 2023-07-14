---
description: Destination SDK으로 빌드된 대상에 대해 파트너 스키마를 구성하는 방법을 알아봅니다.
title: 파트너 스키마 구성
source-git-commit: 20dc7b31f75e88badac17faa542e046598632690
workflow-type: tm+mt
source-wordcount: '1892'
ht-degree: 4%

---


# 파트너 스키마 구성

Experience Platform은 스키마를 사용하여 데이터의 구조를 일관되고 재사용 가능한 방식으로 설명합니다. 데이터가 Platform에 수집되면 XDM 스키마에 따라 구조화됩니다. 디자인 원칙 및 모범 사례를 포함하여 스키마 구성 모델에 대한 자세한 내용은 [스키마 컴포지션 기본 사항](../../../../xdm/schema/composition.md).

Destination SDK을 사용하여 대상을 작성할 때 대상 플랫폼에서 사용할 고유한 파트너 스키마를 정의할 수 있습니다. 이를 통해 사용자는 Platform의 프로필 속성을 대상 플랫폼이 인식하는 특정 필드에 모두 Platform UI 내에서 매핑할 수 있습니다.

대상에 대한 파트너 스키마를 구성할 때 다음과 같이 대상 플랫폼에서 지원하는 필드 매핑을 미세 조정할 수 있습니다.

* 사용자가 를 매핑하도록 허용 `phoneNumber` 에 대한 XDM 속성 `phone` 대상 플랫폼에서 지원하는 속성.
* Experience Platform이 대상 내에서 지원되는 모든 속성 목록을 검색하기 위해 동적으로 호출할 수 있는 동적 파트너 스키마를 만듭니다.
* 대상 플랫폼에 필요한 필수 필드 매핑을 정의합니다.

이 구성 요소가 Destination SDK으로 만든 통합에 어디에 맞는지 이해하려면 의 다이어그램을 참조하십시오. [구성 옵션](../configuration-options.md) 설명서 또는 방법에 대한 안내서 참조 [Destination SDK을 사용하여 파일 기반 대상 구성](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

다음을 통해 스키마 설정을 구성할 수 있습니다. `/authoring/destinations` 엔드포인트. 이 페이지에 표시된 구성 요소를 구성할 수 있는 자세한 API 호출 예는 다음 API 참조 페이지를 참조하십시오.

* [대상 구성 만들기](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [대상 구성 업데이트](../../authoring-api/destination-configuration/update-destination-configuration.md)

이 문서에서는 대상에 사용할 수 있는 지원되는 모든 스키마 구성 옵션에 대해 설명하고 고객이 Platform UI에서 보게 되는 내용을 보여 줍니다.

>[!IMPORTANT]
>
>Destination SDK에서 지원하는 모든 매개변수 이름 및 값은 다음과 같습니다. **대소문자 구분**. 대소문자 구분 오류를 방지하려면 설명서에 표시된 대로 매개 변수 이름과 값을 정확히 사용하십시오.

## 지원되는 통합 유형 {#supported-integration-types}

이 페이지에 설명된 기능을 지원하는 통합 유형에 대한 자세한 내용은 아래 표를 참조하십시오.

| 통합 유형 | 기능 지원 |
|---|---|
| 실시간(스트리밍) 통합 | 예 |
| 파일 기반 (일괄 처리) 통합 | 예 |

## 지원되는 스키마 구성 {#supported-schema-types}

Destination SDK은 여러 스키마 구성을 지원합니다.

* 정적 스키마는 `profileFields` 배열에서 `schemaConfig` 섹션. 정적 스키마에서는 의 Experience Platform UI에 표시되어야 하는 모든 대상 속성을 정의합니다 `profileFields` 배열입니다. 스키마를 업데이트해야 하는 경우 [대상 구성 업데이트](../../authoring-api/destination-configuration/update-destination-configuration.md).
* 동적 스키마는 라는 추가 대상 서버 유형을 사용합니다. [동적 스키마 서버](../../authoring-api/destination-server/create-destination-server.md)를 사용하여 고유한 API를 기반으로 스키마를 동적으로 생성할 수 있습니다. 동적 스키마는 `profileFields` 배열입니다. 스키마를 업데이트해야 하는 경우 업데이트할 필요가 없습니다 [대상 구성 업데이트](../../authoring-api/destination-configuration/update-destination-configuration.md). 대신 동적 스키마 서버는 API에서 업데이트된 스키마를 검색합니다.
* 스키마 구성 내에는 필수(또는 사전 정의된) 매핑을 추가할 수 있는 옵션이 있습니다. 이는 사용자가 Platform UI에서 볼 수 있는 매핑이지만 대상에 대한 연결을 설정할 때 수정할 수 없습니다. 예를 들어 이메일 주소 필드를 항상 대상으로 전송하도록 적용할 수 있습니다.

다음 `schemaConfig` 섹션은 아래 섹션에 표시된 대로 필요한 스키마 유형에 따라 여러 구성 매개 변수를 사용합니다.

## 정적 스키마 만들기 {#attributes-schema}

프로필 속성을 사용하여 정적 스키마를 생성하려면 다음에서 대상 속성을 정의합니다. `profileFields` 아래 표시된 대로 배열합니다.

```json
"schemaConfig":{
      "profileFields":[
           {
              "name":"phoneNo",
              "title":"phoneNo",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the mobilePhone.number value in Experience Platform could be phoneNo on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           },
                      {
              "name":"firstName",
              "title":"firstName",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the person.name.firstName value in Experience Platform could be firstName on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           },
                      {
              "name":"lastName",
              "title":"lastName",
              "description":"This is a fixed attribute on your destination side that customers can map profile attributes to. For example, the person.name.lastName value in Experience Platform could be phoneNo on your side.",
              "type":"string",
              "isRequired":false,
              "readOnly":false,
              "hidden":false
           }
        ],
      "useCustomerSchemaForAttributeMapping":false,
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true,
      "segmentNamespaceAllowList": ["someNamespace"],
      "segmentNamespaceDenyList": ["someOtherNamespace"]

}
```

| 매개변수 | 유형 | 필수/선택적 | 설명 |
|---------|----------|------|---|
| `profileFields` | 배열 | 선택 사항입니다 | 대상 플랫폼에서 허용하는 타겟 속성의 배열을 정의하여 고객이 해당 프로필 속성을 매핑할 수 있도록 합니다. 사용 시 `profileFields` 배열에서 `useCustomerSchemaForAttributeMapping` 매개 변수를 완전히 채우는 방법을 설명합니다. |
| `useCustomerSchemaForAttributeMapping` | 부울 | 선택 사항입니다 | 고객 스키마의 속성을에서 정의한 특성으로 매핑하거나 비활성화합니다. `profileFields` 배열입니다. <ul><li>로 설정된 경우 `true`, 사용자는 매핑 필드에 소스 열만 볼 수 있습니다. `profileFields` 이 경우에는 적용되지 않습니다.</li><li>로 설정된 경우 `false`, 사용자는 스키마의 소스 속성을 에서 정의한 속성에 매핑할 수 있습니다. `profileFields` 배열입니다.</li></ul> 기본값은 `false`입니다. |
| `profileRequired` | 부울 | 선택 사항입니다 | 사용 `true` 사용자가 프로필의 Experience Platform 속성을 대상 플랫폼의 사용자 지정 속성에 매핑할 수 있어야 하는 경우입니다. |
| `segmentRequired` | 부울 | 필수 여부 | 이 매개 변수는 Destination SDK에 필요하며 항상 로 설정해야 합니다. `true`. |
| `identityRequired` | 부울 | 필수 여부 | 다음으로 설정 `true` 사용자가 매핑할 수 있어야 하는 경우 [id 유형](identity-namespace-configuration.md) Experience Platform에서 정의한 특성으로 `profileFields` 배열 . |
| `segmentNamespaceAllowList` | 배열 | 선택 사항입니다 | 사용자가 대상을 대상에 매핑할 수 있는 특정 대상 네임스페이스를 정의합니다. 이 매개 변수를 사용하여 Platform 사용자가 배열에서 정의한 대상 네임스페이스에서만 대상을 내보내도록 제한합니다. 이 매개 변수는 함께 사용할 수 없습니다. `segmentNamespaceDenyList`.<br> <br> 예: `"segmentNamespaceAllowList": ["AudienceManager"]` 는 사용자가 의 대상자만 매핑할 수 있도록 허용합니다. `AudienceManager` 네임스페이스를 이 대상에 추가합니다. <br> <br> 사용자가 대상을 대상으로 내보낼 수 있도록 이 매개 변수를 무시할 수 있습니다. <br> <br> 둘 다인 경우 `segmentNamespaceAllowList` 및 `segmentNamespaceDenyList` 구성에서 이(가) 누락되면 사용자는 의 대상자만 내보낼 수 있습니다. [세분화 서비스](../../../../segmentation/home.md). |
| `segmentNamespaceDenyList` | 배열 | 선택 사항입니다 | 사용자가 배열에 정의된 대상 네임스페이스에서 대상을 대상에 매핑하지 못하도록 제한합니다. 과 함께 사용할 수 없음 `segmentNamespaceAllowed`. <br> <br> 예: `"segmentNamespaceDenyList": ["AudienceManager"]` 은(는) 의 대상자 매핑에서 사용자를 차단합니다. `AudienceManager` 네임스페이스를 이 대상에 추가합니다. <br> <br> 사용자가 대상을 대상으로 내보낼 수 있도록 이 매개 변수를 무시할 수 있습니다. <br> <br> 둘 다인 경우 `segmentNamespaceAllowed` 및 `segmentNamespaceDenyList` 구성에서 이(가) 누락되면 사용자는 의 대상자만 내보낼 수 있습니다. [세분화 서비스](../../../../segmentation/home.md). <br> <br> 원본에 관계없이 모든 대상을 내보내도록 허용하려면 을 설정합니다. `"segmentNamespaceDenyList":[]`. |

{style="table-layout:auto"}

결과 UI 경험이 아래 이미지에 표시됩니다.

사용자가 대상 매핑을 선택하면 `profileFields` 배열입니다.

![타겟 특성 화면을 표시하는 UI 이미지입니다.](../../assets/functionality/destination-configuration/select-attributes.png)

속성을 선택하면 타겟 필드 열에서 속성을 볼 수 있습니다.

![속성이 있는 정적 대상 스키마를 보여 주는 UI 이미지](../../assets/functionality/destination-configuration/static-schema-attributes.png)

## 동적 스키마 만들기 {#dynamic-schema-configuration}

Destination SDK은 동적 파트너 스키마 생성을 지원합니다. 정적 스키마와 달리 동적 스키마는 `profileFields` 배열입니다. 대신 동적 스키마는 스키마 구성을 검색하는 위치에서 자체 API에 연결되는 동적 스키마 서버를 사용합니다.

>[!IMPORTANT]
>
>동적 스키마를 생성하기 전에 다음을 수행해야 합니다 [동적 스키마 서버 만들기](../../authoring-api/destination-server/create-destination-server.md).

동적 스키마 구성에서 `profileFields` 배열이 로 대체됨 `dynamicSchemaConfig` 섹션에 있는 마지막 항목이 될 필요가 없습니다.

```json
"schemaConfig":{
   "dynamicSchemaConfig":{
      "dynamicEnum": {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"DYNAMIC_SCHEMA_SERVER_ID",
         "value": "Schema Name",
         "responseFormat": "SCHEMA"
      }
   },
   "profileRequired":true,
   "segmentRequired":true,
   "identityRequired":true
}
```

| 매개변수 | 유형 | 필수/선택적 | 설명 |
|---------|----------|------|---|
| `dynamicEnum.authenticationRule` | 문자열 | 필수 여부 | 방법을 나타냅니다. [!DNL Platform] 고객이 대상에 연결합니다. 허용되는 값은 다음과 같습니다 `CUSTOMER_AUTHENTICATION`, `PLATFORM_AUTHENTICATION`, `NONE`. <br> <ul><li>사용 `CUSTOMER_AUTHENTICATION` 플랫폼 고객이 설명된 인증 방법을 통해 시스템에 로그인하는 경우 [여기](customer-authentication.md). </li><li> 사용 `PLATFORM_AUTHENTICATION` Adobe과 대상 및 간에 글로벌 인증 시스템이 있는 경우 [!DNL Platform] 고객은 대상에 연결하기 위해 인증 자격 증명을 제공할 필요가 없습니다. 이 경우 다음을 수행해야 합니다 [자격 증명 개체 만들기](../../credentials-api/create-credential-configuration.md) 자격 증명 API 사용. </li><li>사용 `NONE` 대상 플랫폼으로 데이터를 전송하는 데 인증이 필요하지 않은 경우 </li></ul> |
| `dynamicEnum.destinationServerId` | 문자열 | 필수 여부 | 다음 `instanceId` 동적 스키마 서버. 이 대상 서버에는 Experience Platform이 동적 스키마를 검색하기 위해 호출할 API 끝점이 포함됩니다. |
| `dynamicEnum.value` | 문자열 | 필수 여부 | 동적 스키마 서버 구성에 정의된 동적 스키마의 이름입니다. |
| `dynamicEnum.responseFormat` | 문자열 | 필수 여부 | 항상 로 설정 `SCHEMA` 동적 스키마를 정의할 때. |
| `profileRequired` | 부울 | 선택 사항입니다 | 사용 `true` 사용자가 프로필의 Experience Platform 속성을 대상 플랫폼의 사용자 지정 속성에 매핑할 수 있어야 하는 경우입니다. |
| `segmentRequired` | 부울 | 필수 여부 | 이 매개 변수는 Destination SDK에 필요하며 항상 로 설정해야 합니다. `true`. |
| `identityRequired` | 부울 | 필수 여부 | 다음으로 설정 `true` 사용자가 매핑할 수 있어야 하는 경우 [id 유형](identity-namespace-configuration.md) Experience Platform에서 정의한 특성으로 `profileFields` 배열 . |

{style="table-layout:auto"}

## 필수 매핑 {#required-mappings}

스키마 구성 내에서는 정적 또는 동적 스키마 외에 필수(또는 사전 정의된) 매핑을 추가할 수 있습니다. 이는 사용자가 Platform UI에서 볼 수 있는 매핑이지만 대상에 대한 연결을 설정할 때 수정할 수 없습니다.

예를 들어 이메일 주소 필드를 항상 대상으로 전송하도록 적용할 수 있습니다.

>[!NOTE]
>
>현재 지원되는 필수 매핑 조합은 다음과 같습니다.
>* 필수 소스 필드와 필수 대상 필드를 구성할 수 있습니다. 이 경우 사용자는 두 필드 중 하나를 편집하거나 선택할 수 없으며 선택 사항만 볼 수 있습니다.
>* 필수 대상 필드만 구성할 수 있습니다. 이 경우 사용자는 대상에 매핑할 소스 필드를 선택할 수 있습니다.
>
> 필수 소스 필드만 현재 구성하는 중 *아님* 지원됨.

필요한 매핑이 포함된 스키마 구성의 두 가지 예제와 의 매핑 단계에서 표시되는 내용을 참조하십시오. [데이터를 배치 대상으로 활성화 워크플로](../../../ui/activate-batch-profile-destinations.md).


>[!BEGINTABS]

>[!TAB 필수 소스 및 대상 매핑]

아래 예는 필수 소스 및 대상 매핑을 모두 보여 줍니다. 소스 필드와 대상 필드가 모두 필수 매핑으로 지정된 경우 사용자는 두 필드 중 하나를 선택하거나 편집할 수 없으며 사전 정의된 선택 사항만 볼 수 있습니다.

```json
"schemaConfig": {
    "requiredMappingsOnly": true,
    "requiredMappings": [
      {
        "sourceType": "text/x.schema-path",
        "source": "personalEmail.address",
        "destination": "personalEmail.address"
      }
    ] 
}
```

| 매개변수 | 유형 | 필수/선택적 | 설명 |
|---|---|---|---|
| `requiredMappingsOnly` | 부울 | 선택 사항입니다 | true로 설정되면,에서 정의하는 필수 매핑과는 별도로 사용자는 활성화 플로우에서 다른 속성 및 ID를 매핑할 수 없습니다. `requiredMappings` 배열입니다. |
| `requiredMappings.sourceType` | 문자열 | 필수 여부 | 의 유형을 나타냅니다 `source` 필드. 지원되는 값: <ul><li>`text/x.schema-path`: 다음 경우에 이 값 사용: `source` 필드는 XDM 스키마의 프로필 속성입니다.</li><li>`text/x.aep-xl`: 다음 경우에 이 값 사용: `source` 필드는 정규 표현식으로 정의됩니다. 예: `iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`</li><li>`text/plain`: 다음 경우에 이 값 사용: `source` 필드는 매크로 템플릿으로 정의됩니다. 현재 지원되는 유일한 매크로 템플릿은 `metadata.segment.alias`.</li></ul> |
| `requiredMappings.source` | 문자열 | 필수 여부 | 소스 필드의 값을 나타냅니다. 지원되는 값 유형: <ul><li>XDM 프로필 속성. 예: `personalEmail.address`. 소스 속성이 XDM 프로필 속성인 경우 `sourceType` 매개 변수 `text/x.schema-path`.</li><li>정규 표현식. 예: `iif(segmentMembership.ups.aep_seg_id.status==\"exited\", \"1\", \"0\")`. 소스 속성이 정규 표현식인 경우 `sourceType` 매개 변수 `text/x.aep-xl`.</li><li>매크로 템플릿. 예:`metadata.segment.alias`. 소스 속성이 매크로 템플릿인 경우 `sourceType` 매개 변수 `text/plain`. 현재 지원되는 유일한 매크로 템플릿은 `metadata.segment.alias`.</li></ul> |
| `requiredMappings.destination` | 문자열 | 필수 여부 | 대상 필드의 값을 나타냅니다. 소스 필드와 대상 필드가 모두 필수 매핑으로 지정된 경우 사용자는 두 필드 중 하나를 선택하거나 편집할 수 없으며 선택 사항만 볼 수 있습니다. |

{style="table-layout:auto"}

따라서 두 가지 모두 **[!UICONTROL 소스 필드]** 및 **[!UICONTROL Target 필드]** Platform UI의 섹션이 회색으로 표시됩니다.

![UI 활성화 플로우에서 필요한 매핑의 이미지입니다.](../../assets/functionality/destination-configuration/required-mappings-2.png)

>[!TAB 필수 대상 매핑]

아래 예는 필수 대상 매핑을 보여 줍니다. 대상 필드만 필요에 따라 지정하는 경우 사용자는 매핑할 소스 필드를 선택할 수 있습니다.

```json
"schemaConfig": {
    "requiredMappingsOnly": true,
    "requiredMappings": [
      {
        "destination": "identityMap.ExamplePartner_ID",
        "mandatoryRequired": true,
        "primaryKeyRequired": true
      }
    ] 
}
```

| 매개변수 | 유형 | 필수/선택적 | 설명 |
|---|---|---|---|
| `requiredMappingsOnly` | 부울 | 선택 사항입니다 | true로 설정되면,에서 정의하는 필수 매핑과는 별도로 사용자는 활성화 플로우에서 다른 속성 및 ID를 매핑할 수 없습니다. `requiredMappings` 배열입니다. |
| `requiredMappings.destination` | 문자열 | 필수 여부 | 대상 필드의 값을 나타냅니다. 대상 필드만 지정된 경우 사용자는 대상에 매핑할 소스 필드를 선택할 수 있습니다. |
| `mandatoryRequired` | 부울 | 선택 사항입니다 | 매핑을 다음으로 표시할지 여부를 나타냅니다. [필수 속성](../../../ui/activate-batch-profile-destinations.md#mandatory-attributes). |
| `primaryKeyRequired` | 부울 | 선택 사항입니다 | 매핑을 다음으로 표시할지 여부를 나타냅니다. [중복 제거 키](../../../ui/activate-batch-profile-destinations.md#deduplication-keys). |

{style="table-layout:auto"}

그 결과 **[!UICONTROL Target 필드]** Platform UI의 섹션은 회색으로 표시되고 **[!UICONTROL 소스 필드]** 섹션이 활성 상태이므로 사용자가 이 섹션과 상호 작용할 수 있습니다. 다음 **[!UICONTROL 필수 키]** 및 **[!UICONTROL 중복 제거 키]** 옵션이 활성 상태이므로 사용자가 변경할 수 없습니다.

![UI 활성화 플로우에서 필요한 매핑의 이미지입니다.](../../assets/functionality/destination-configuration/required-mappings-1.png)

>[!ENDTABS]

## 다음 단계 {#next-steps}

이 문서를 읽은 후에는 Destination SDK에서 지원하는 스키마 유형과 스키마를 구성하는 방법을 보다 잘 이해할 수 있어야 합니다.

다른 대상 구성 요소에 대한 자세한 내용은 다음 문서를 참조하십시오.

* [고객 인증](customer-authentication.md)
* [OAuth2 인증](oauth2-authentication.md)
* [UI 속성](ui-attributes.md)
* [고객 데이터 필드](customer-data-fields.md)
* [ID 네임스페이스 구성](identity-namespace-configuration.md)
* [지원되는 매핑 구성](supported-mapping-configurations.md)
* [대상 게재](destination-delivery.md)
* [대상 메타데이터 구성](audience-metadata-configuration.md)
* [집계 정책](aggregation-policy.md)
* [일괄 처리 구성](batch-configuration.md)
* [과거 프로필 자격 요건](historical-profile-qualifications.md)