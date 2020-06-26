---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Data Lake의 개인 정보 요청 처리
topic: overview
translation-type: tm+mt
source-git-commit: 327be13cbaaa40e4d0409cbb49a051b7067759bf
workflow-type: tm+mt
source-wordcount: '1275'
ht-degree: 0%

---


# Data Lake의 개인 정보 요청 처리

Adobe Experience Platform Privacy Service은 법적 및 조직의 개인 정보 보호 규정에 따라 고객의 개인 데이터 액세스, 판매 거부 또는 삭제를 요청합니다.

이 문서에서는 Data Lake에 저장된 고객 데이터의 개인 정보 요청 처리와 관련된 필수 개념을 다룹니다.

## 시작하기

이 안내서를 읽기 전에 다음 Experience Platform 서비스에 대해 잘 알고 있는 것이 좋습니다.

* [Privacy Service](../privacy-service/home.md): Adobe Experience Cloud 애플리케이션에서 개인 데이터를 액세스, 판매 거부 또는 삭제하기 위한 고객 요청을 관리합니다.
* [카탈로그 서비스](home.md): Experience Platform 내의 데이터 위치 및 계열에 대한 기록 시스템. 데이터 세트 메타데이터를 업데이트하는 데 사용할 수 있는 API를 제공합니다.
* [XDM(Experience Data Model) 시스템](../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
* [ID 서비스](../identity-service/home.md): 다양한 디바이스와 시스템에 ID를 연결하여 고객 경험 데이터의 세분화로 인한 기본적인 문제를 해결합니다.

## ID 네임스페이스 이해 {#namespaces}

Adobe Experience Platform ID 서비스는 시스템 및 디바이스에서 고객 ID 데이터를 연결해줍니다. Identity Service는 **ID 네임스페이스를** 사용하여 ID 값에 대한 컨텍스트를 ID 시스템에 연결함으로써 제공합니다. 네임스페이스는 이메일 주소(&quot;이메일&quot;)와 같은 일반 개념을 나타내거나 Adobe Advertising Cloud ID(&quot;AdCloud&quot;) 또는 Adobe Target ID(&quot;TNTID&quot;)와 같은 특정 응용 프로그램과 ID를 연결할 수 있습니다.

ID 서비스는 전역적으로 정의된(표준) 및 사용자 정의(사용자 정의) ID 네임스페이스의 저장소를 유지 관리합니다. 표준 네임스페이스는 모든 조직(예: &quot;이메일&quot; 및 &quot;ECID&quot;)에서 사용할 수 있지만 조직에서 특정 요구에 맞는 사용자 정의 네임스페이스를 만들 수도 있습니다.

Experience Platform의 ID 네임스페이스에 대한 자세한 내용은 [ID 네임스페이스 개요를 참조하십시오](../identity-service/namespaces.md).

## 데이터 세트에 ID 데이터 추가

Data Lake에 대한 개인 정보 보호 요청을 만들 때, 데이터를 찾고 그에 따라 처리하기 위해 각 개별 고객에 대해 유효한 ID 값(및 관련 네임스페이스)을 제공해야 합니다. 따라서 개인 정보 요청의 대상이 되는 모든 데이터 집합은 관련 XDM 스키마에 **ID 설명자를** 포함해야 합니다.

>[!NOTE] ID 설명자 메타데이터(예: 임시 데이터 집합)를 지원하지 않는 스키마를 기반으로 한 데이터 집합은 현재 개인 정보 요청에서 처리할 수 없습니다.

이 섹션에서는 기존 데이터 세트의 XDM 스키마에 ID 설명자를 추가하는 단계를 안내합니다. ID 설명자가 있는 데이터 세트가 이미 있는 경우 [다음 섹션으로 건너뛸 수 있습니다](#nested-maps).

>[!IMPORTANT]
>
>ID로 설정할 스키마 필드를 결정할 때는 중첩 맵 유형 필드 [를 사용하는 제한 사항을 염두에 두십시오](#nested-maps).

데이터 세트 스키마에 ID 설명자를 추가하는 방법에는 두 가지가 있습니다.

* [UI 사용](#identity-ui)
* [API 사용](#identity-api)

### UI 사용 {#identity-ui}

Experience Platform 사용자 인터페이스에서 스키마 _[!UICONTROL 작업]_공간을 사용하여 기존 XDM 스키마를 편집할 수 있습니다. 스키마에 ID 설명자를 추가하려면 목록에서 스키마를 선택하고 스키마 필드를 ID 필드로[설정하는 단계를](../xdm/tutorials/create-schema-ui.md#identity-field)따릅니다.

스키마 내의 적절한 필드를 ID 필드로 설정하면 개인 정보 요청 [제출 시 다음 섹션으로 진행할 수 있습니다](#submit).

### API 사용 {#identity-api}

>[!NOTE] 이 섹션에서는 데이터 세트 XDM 스키마의 고유한 URI ID 값을 알고 있다고 가정합니다. 이 값을 모르는 경우 카탈로그 서비스 API를 사용하여 검색할 수 있습니다. 개발자 안내서의 [시작](./api/getting-started.md) 섹션을 읽은 후 [는 카탈로그 개체를](./api/list-objects.md) 목록 [으로 표시하거나](./api/look-up-object.md) 조회하여데이터 세트를 찾습니다. 스키마 ID는 `schemaRef.id`
>
> 이 섹션에는 스키마 레지스트리 API에 대한 호출이 포함되어 있습니다. 컨테이너 개념 `{TENANT_ID}` 과 귀하 [의 이해를 포함하여 API 사용과 관련된 중요한 정보는 개발자 안내서의 시작](../xdm/api/getting-started.md) 섹션을 참조하십시오.

스키마 레지스트리 API의 끝점에 POST 요청을 만들어 데이터 집합의 XDM 스키마에 ID 설명자를 추가할 수 `/descriptors` 있습니다.

**API 형식**

```http
POST /descriptors
```

**요청**

다음 요청은 샘플 스키마의 &quot;이메일 주소&quot; 필드에 ID 설명자를 정의합니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
      {
        "@type": "xdm:descriptorIdentity",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/personalEmail/address",
        "xdm:namespace": "Email",
        "xdm:property": "xdm:code",
        "xdm:isPrimary": false
      }'
```

| 속성 | 설명 |
| --- | --- |
| `@type` | 생성할 설명자 유형입니다. ID 설명자의 경우 값은 &quot;xdm:descriptorIdentity&quot;여야 합니다. |
| `xdm:sourceSchema` | 데이터 세트 XDM 스키마의 고유한 URI ID. |
| `xdm:sourceVersion` | 에 지정된 XDM 스키마 버전입니다 `xdm:sourceSchema`. |
| `xdm:sourceProperty` | 설명자가 적용되는 스키마 필드의 경로입니다. |
| `xdm:namespace` | Privacy Service에서 인식하는 [표준 ID 네임스페이스](../privacy-service/api/appendix.md#standard-namespaces) 또는 조직에서 정의한 사용자 지정 네임스페이스 중 하나입니다. |
| `xdm:property` | 사용 중인 네임스페이스에 따라 &quot;xdm:id&quot; 또는 &quot;xdm:code&quot; 중 하나를 선택합니다 `xdm:namespace`. |
| `xdm:isPrimary` | 선택적 부울 값입니다. true이면 필드가 기본 ID임을 나타냅니다. 스키마에는 하나의 기본 ID만 포함될 수 있습니다. 포함되지 않은 경우 기본값은 false입니다. |

**응답**

성공적인 응답은 HTTP 상태 201(작성됨)과 새로 만든 설명자의 세부 정보를 반환합니다.

```json
{
  "@type": "xdm:descriptorIdentity",
  "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
  "xdm:sourceVersion": 1,
  "xdm:sourceProperty": "/personalEmail/address",
  "xdm:namespace": "Email",
  "xdm:property": "xdm:code",
  "xdm:isPrimary": false,
  "meta:containerId": "tenant",
  "@id": "f3a1dfa38a4871cf4442a33074c1f9406a593407"
}
```

## 요청 제출 {#submit}

>[!NOTE] 이 섹션에서는 Data Lake에 대한 개인 정보 요청의 형식을 지정하는 방법에 대해 설명합니다. 요청 페이로드에서 제출된 사용자 ID 데이터의 형식을 적절하게 지정하는 방법을 비롯하여 개인 정보 작업을 제출하는 방법에 대한 전체 단계를 보려면 [Privacy Service UI](../privacy-service/ui/overview.md) 또는 [Privacy Service API](../privacy-service/api/getting-started.md) 설명서를 검토해야 합니다.

다음 섹션에서는 Privacy Service UI 또는 API를 사용하여 Data Lake에 대한 개인 정보 요청을 만드는 방법에 대해 설명합니다.

### UI 사용

UI에서 작업 요청을 만들 때는 **제품** 에서 **AEP 데이터 레이크** 및/또는 _프로필_ 을 선택하여 데이터 레이크 또는 실시간 고객 프로필에 저장된 데이터의 작업을 각각 처리해야 합니다.

<img src="images/privacy/product-value.png" width="450"><br>

### API 사용

API에서 작업 요청 `userIDs` 을 만들 때 제공된 모든 작업 `namespace` 은 적용되는 데이터 저장소에 `type` 따라 특정 항목을 사용해야 합니다. 데이터 레이크의 ID는 해당 값에 &quot;등록되지 않은&quot; 값을 사용해야 하며, 이 `type` 값은 적용 가능한 데이터 세트에 추가된 `namespace` 개인 정보 레이블 [중 하나와 일치하는](#privacy-labels) 값입니다.

또한 요청 페이로드 `include` 배열에 요청이 수행되는 다른 데이터 저장소에 대한 제품 값이 포함되어야 합니다. Data Lake에 대한 요청을 할 때 배열에 &quot;aepDataLake&quot; 값이 포함되어야 합니다.

다음 요청은 등록되지 않은 &quot;email_label&quot; 네임스페이스를 사용하여 Data Lake에 대한 새 개인 정보 작업을 만듭니다. 또한 배열에 있는 데이터 레이크의 제품 값도 `include` 포함합니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
      }
    ],
    "users": [
      {
        "key": "user12345",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "email_label",
            "value": "ajones@acme.com",
            "type": "unregistered"
          },
          {
            "namespace": "email_label",
            "value": "jdoe@example.com",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["aepDataLake"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "ccpa"
}'
```

## 요청 처리 삭제

Experience Platform이 Privacy Service에서 삭제 요청을 받으면 Platform은 요청이 수신되고 영향을 받는 데이터가 삭제하도록 표시되었다는 확인을 Privacy Service에 보냅니다. 그러면 7일 이내에 Data Lake에서 레코드가 제거됩니다. 이 7일 기간 동안 데이터는 소프트 삭제되므로 Platform 서비스에서 액세스할 수 없습니다.

향후 릴리스에서 Platform은 데이터가 물리적으로 삭제된 후 Privacy Service에 확인을 보냅니다.

## 다음 단계

이 문서를 읽음으로써 Data Lake의 개인 정보 요청 처리와 관련된 중요한 개념을 도입했습니다. ID 데이터를 관리하고 개인 정보 보호 작업을 만드는 방법에 대한 이해를 돕기 위해 이 안내서 전체에서 제공된 설명서를 계속 읽는 것이 좋습니다.

프로필 스토어에 대한 개인정보 보호 요청을 처리하는 단계는 [실시간 고객 프로필을](../profile/privacy.md) 위한 개인정보 보호 요청 처리에 관한 문서를 참조하십시오.

## 부록

다음 섹션에는 Data Lake의 개인 정보 요청을 처리하기 위한 추가 정보가 포함되어 있습니다.

### 중첩된 맵 유형 필드 레이블 지정 {#nested-maps}

개인 정보 표시를 지원하지 않는 중첩 맵 유형 필드에는 두 가지 종류가 있습니다.

* 배열 유형 필드 내의 맵 유형 필드
* 다른 맵 유형 필드 내의 맵 유형 필드

위의 두 예 중 하나에 대한 개인 정보 작업 처리가 결국 실패합니다. 따라서 비공개 고객 데이터를 저장하기 위해 중첩된 맵 유형 필드를 사용하지 않는 것이 좋습니다. 관련 소비자 ID는 레코드 기반 데이터 집합에 대해 `identityMap` 필드(자체 맵 유형 필드) 내에 매핑되지 않은 데이터 유형이나 시간 시리즈 기반 데이터 세트에 대한 `endUserID` 필드로 저장해야 합니다.