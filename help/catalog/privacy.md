---
keywords: Experience Platform;홈;인기 항목;데이터 레이크 개인 정보;ID 네임스페이스;개인 정보;데이터 레이크
solution: Experience Platform
title: Data Lake의 개인 정보 보호 요청 처리
topic-legacy: overview
description: Adobe Experience Platform Privacy Service은 법률 및 조직 개인 정보 보호 규정에 따라 지정된 대로 고객 개인 데이터에 대한 액세스, 판매 거부 또는 삭제 요청을 처리합니다. 이 문서에서는 Data Lake에 저장된 고객 데이터의 개인 정보 보호 요청 처리와 관련된 중요한 개념을 다룹니다.
exl-id: c06b0a44-be1a-4938-9c3e-f5491a3dfc19
source-git-commit: a713245f3228ed36f262fa3c2933d046ec8ee036
workflow-type: tm+mt
source-wordcount: '1388'
ht-degree: 1%

---

# 의 개인 정보 보호 요청 처리 [!DNL Data Lake]

Adobe Experience Platform [!DNL Privacy Service] 법적 및 조직 개인 정보 보호 규정에 따라 지정된 대로 고객 개인 데이터에 대한 액세스, 판매 거부 또는 삭제 요청을 처리합니다.

이 문서에서는 [!DNL Data Lake].

>[!NOTE]
>
>이 안내서에서는 Experience Platform의 데이터 레이크에 대해 개인 정보 보호 요청을 수행하는 방법만 다룹니다. 실시간 고객 프로필 데이터 저장소에 대한 개인 정보 보호 요청도 수행하려는 경우 가이드를 참조하십시오 [프로필에 대한 개인 정보 보호 요청 처리](../profile/privacy.md) 추가 정보.
>
>다른 Adobe Experience Cloud 애플리케이션에 대해 개인 정보 보호 요청을 수행하는 방법에 대한 단계는 [Privacy Service 설명서](../privacy-service/experience-cloud-apps.md).

## 시작하기

다음 사항에 대한 작업 이해를 하는 것이 좋습니다 [!DNL Experience Platform] 이 안내서를 읽기 전 서비스

* [[!DNL Privacy Service]](../privacy-service/home.md): Adobe Experience Cloud 애플리케이션에서 개인 데이터를 액세스, 판매 거부 또는 삭제하기 위한 고객 요청을 관리합니다.
* [[!DNL Catalog Service]](home.md): 데이터 위치 및 내부 계보 기록 시스템 [!DNL Experience Platform]. 데이터 집합 메타데이터를 업데이트하는 데 사용할 수 있는 API를 제공합니다.
* [[!DNL Experience Data Model (XDM) System]](../xdm/home.md): 표준화된 프레임워크 [!DNL Experience Platform] 고객 경험 데이터를 구성합니다.
* [[!DNL Identity Service]](../identity-service/home.md): 여러 장치 및 시스템에서 ID를 브리징하여 고객 경험 데이터의 분화로 인한 근본적인 문제를 해결합니다.

## ID 네임스페이스 이해 {#namespaces}

Adobe Experience Platform [!DNL Identity Service] 는 시스템 및 장치에서 고객 ID 데이터를 전달합니다. [!DNL Identity Service] id 네임스페이스를 사용하여 ID 값과 원본 시스템을 관련시켜 ID 값의 컨텍스트를 제공합니다. 네임스페이스는 이메일 주소(&quot;이메일&quot;)와 같은 일반적인 개념을 나타내거나 ID를 Adobe Advertising Cloud ID(&quot;AdCloud&quot;) 또는 Adobe Target ID(&quot;TNTID&quot;)와 같은 특정 애플리케이션과 연결할 수 있습니다.

[!DNL Identity Service] 전역적으로 정의된(표준) 및 사용자 정의(사용자 정의) id 네임스페이스의 저장소를 유지 관리합니다. 표준 네임스페이스는 모든 조직(예: &quot;이메일&quot; 및 &quot;ECID&quot;)에서 사용할 수 있지만 조직은 특정 요구 사항에 맞게 사용자 지정 네임스페이스를 만들 수도 있습니다.

의 ID 네임스페이스에 대한 자세한 내용은 [!DNL Experience Platform]를 참조하고 [id 네임스페이스 개요](../identity-service/namespaces.md).

## 데이터 세트에 ID 데이터 추가

에 대한 개인 정보 보호 요청을 만들 때 [!DNL Data Lake], 데이터를 찾고 그에 따라 처리하기 위해서는 각 개별 고객에 대해 유효한 ID 값(및 관련 네임스페이스)을 제공해야 합니다. 따라서 개인 정보 보호 요청의 대상이 되는 모든 데이터 세트에는 연결된 XDM 스키마에 ID 설명자가 포함되어야 합니다.

>[!NOTE]
>
>ID 설명자 메타데이터(예: 애드혹 데이터 세트)를 지원하지 않는 스키마를 기반으로 하는 데이터 세트는 현재 개인 정보 보호 요청에서 처리할 수 없습니다.

이 섹션에서는 기존 데이터 세트의 XDM 스키마에 ID 설명자를 추가하는 단계를 설명합니다. ID 설명자가 있는 데이터 세트가 이미 있는 경우 [다음 섹션](#nested-maps).

>[!IMPORTANT]
>
>ID로 설정할 스키마 필드를 결정할 때에는 다음 사항에 유의하십시오. [중첩 맵 유형 필드 사용 제한 사항](#nested-maps).

데이터 세트 스키마에 ID 설명자를 추가하는 방법에는 두 가지가 있습니다.

* [UI 사용](#identity-ui)
* [API 사용](#identity-api)

### UI 사용 {#identity-ui}

에서 [!DNL Experience Platform ]사용자 인터페이스, **[!UICONTROL 스키마]** workspace를 사용하면 기존 XDM 스키마를 편집할 수 있습니다. 스키마에 ID 설명자를 추가하려면 목록에서 스키마를 선택하고 다음 단계를 수행합니다 [스키마 필드를 ID 필드로 설정](../xdm/tutorials/create-schema-ui.md#identity-field) 에서 [!DNL Schema Editor] 자습서입니다.

스키마 내에 ID 필드로 적절한 필드를 설정하면 다음 섹션으로 진행할 수 있습니다 [개인 정보 요청 제출](#submit).

### API 사용 {#identity-api}

>[!NOTE]
>
>이 섹션에서는 데이터 세트 XDM 스키마의 고유한 URI ID 값을 알고 있다고 가정합니다. 이 값을 모를 경우 [!DNL Catalog Service] API. 를 읽은 후 [시작하기](./api/getting-started.md) 개발자 가이드의 섹션에서 [목록](./api/list-objects.md) 또는 [보기](./api/look-up-object.md) [!DNL Catalog] 데이터 집합을 찾을 개체. 스키마 ID는 `schemaRef.id`
>
>이 섹션에서는 스키마 레지스트리 API를 호출하는 방법을 알고 있다고 가정합니다. API 사용과 관련된 중요한 정보(예: `{TENANT_ID}` 컨테이너의 개념은 [시작하기](../xdm/api/getting-started.md) api 안내서의 섹션을 참조하십시오.

에 POST 요청을 수행하여 데이터 집합의 XDM 스키마에 ID 설명자를 추가할 수 있습니다 `/descriptors` 의 엔드포인트 [!DNL Schema Registry] API.

**API 형식**

```http
POST /descriptors
```

**요청**

다음 요청은 샘플 스키마의 &quot;email address&quot; 필드에 ID 설명자를 정의합니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
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
| `@type` | 생성 중인 설명자 유형입니다. ID 설명자의 경우 값은 &quot;xdm:descriptorIdentity&quot;여야 합니다. |
| `xdm:sourceSchema` | 데이터 집합 XDM 스키마의 고유 URI ID입니다. |
| `xdm:sourceVersion` | 에 지정된 XDM 스키마 버전입니다. `xdm:sourceSchema`. |
| `xdm:sourceProperty` | 설명자가 적용되는 스키마 필드의 경로입니다. |
| `xdm:namespace` | 다음 중 하나 [표준 id 네임스페이스](../privacy-service/api/appendix.md#standard-namespaces) 인식자 [!DNL Privacy Service]또는 조직에서 정의한 사용자 정의 네임스페이스입니다. |
| `xdm:property` | 아래에 사용되는 네임스페이스에 따라 &quot;xdm:id&quot; 또는 &quot;xdm:code&quot; 중 하나를 선택합니다 `xdm:namespace`. |
| `xdm:isPrimary` | 선택적 부울 값입니다. true면 필드가 기본 ID임을 나타냅니다. 스키마에는 기본 ID가 하나만 포함될 수 있습니다. 포함되지 않은 경우 기본값은 false 입니다. |

**응답**

성공한 응답은 HTTP 상태 201(생성됨) 및 새로 만든 설명자의 세부 정보를 반환합니다.

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

>[!NOTE]
>
>이 섹션에서는 다음에 대한 개인 정보 보호 요청의 형식을 지정하는 방법을 다룹니다 [!DNL Data Lake]. 를 검토하는 것이 좋습니다 [[!DNL Privacy Service] UI](../privacy-service/ui/overview.md) 또는 [[!DNL Privacy Service] API](../privacy-service/api/getting-started.md) 문서 를 참조하십시오.

다음 섹션에서는 [!DNL Data Lake] 사용 [!DNL Privacy Service] UI 또는 API.

>[!IMPORTANT]
>
>개인 정보 보호 요청을 완료하는 데 걸리는 시간은 보장할 수 없습니다. 요청이 여전히 처리 중인 동안 Data Lake 내에서 변경 사항이 발생하는 경우 해당 레코드가 처리되는지 여부도 보장할 수 없습니다.

### UI 사용

UI에서 작업 요청을 만들 때는 반드시 선택해야 합니다 **[!UICONTROL AEP Data Lake]** 아래에 **[!UICONTROL 제품]** 에 저장된 데이터의 작업을 처리하려면 [!DNL Data Lake].

![개인 정보 보호 요청 만들기 대화 상자에서 선택한 Data Lake 제품을 보여주는 이미지](./images/privacy/product-value.png)

### API 사용

API에서 작업 요청을 만들 때 `userIDs` 제공된 경우 특정 `namespace` 및 `type` 적용되는 데이터 저장소에 따라 다릅니다. 의 ID [!DNL Data Lake] 를 사용해야 합니다. `unregistered` 그들의 `type` 값, 및 `namespace` 와 일치하는 값 [개인 정보 레이블](#privacy-labels) 해당 데이터 세트에 추가되었습니다.

또한 `include` 요청 페이로드 배열에는 요청이 수행되고 있는 다양한 데이터 저장소의 제품 값이 포함되어야 합니다. 에 요청할 때 [!DNL Data Lake]이면 배열에 값이 포함되어야 합니다 `aepDataLake`.

다음 요청은 [!DNL Data Lake], 등록 취소를 사용하여 `email_label` 네임스페이스. 여기에는 다음에 대한 제품 값도 포함됩니다 [!DNL Data Lake] 에서 `include` 배열:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{ORG_ID}"
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

>[!IMPORTANT]
>
>플랫폼은 모든 위치에서 개인 정보 요청을 처리합니다 [샌드박스](../sandboxes/home.md) 조직에 속해 있어야 합니다. 따라서, 모든 `x-sandbox-name` 요청에 포함된 헤더는 시스템에서 무시됩니다.

## 요청 처리 삭제

When [!DNL Experience Platform] 에서 삭제 요청을 받습니다. [!DNL Privacy Service], [!DNL Platform] 에 확인 보내기 [!DNL Privacy Service] 요청이 수신되고 영향을 받는 데이터가 삭제로 표시되었음을 나타냅니다. 그러면 레코드가 [!DNL Data Lake] 7일 안에 이 7일 기간 동안 데이터는 소프트 삭제되므로 다른 사용자가 액세스할 수 없습니다 [!DNL Platform] 서비스.

향후 릴리스에서 [!DNL Platform] 은(는) 확인을 [!DNL Privacy Service] 데이터가 물리적으로 삭제된 후

## 다음 단계

이 문서를 읽은 후에는 의 개인 정보 보호 요청 처리와 관련된 중요한 개념을 도입했습니다 [!DNL Data Lake]. ID 데이터를 관리하고 개인 정보 보호 작업을 만드는 방법을 더 깊이 이해하기 위해 이 안내서 전체에서 제공된 설명서를 계속 읽는 것이 좋습니다.

다음 문서를 참조하십시오. [실시간 고객 프로필에 대한 개인 정보 보호 요청 처리](../profile/privacy.md) 에 대한 개인 정보 보호 요청 처리 단계에 대해 설명합니다. [!DNL Profile] 저장.

## 부록

다음 섹션에서는 [!DNL Data Lake].

### 중첩 맵 유형 필드에 레이블 지정 {#nested-maps}

개인 정보 레이블 지정을 지원하지 않는 중첩 맵 유형 필드에는 두 종류가 있습니다.

* 배열 유형 필드 내의 맵 유형 필드
* 다른 맵 유형 필드 내의 맵 유형 필드

위의 두 예 중 하나에 대한 개인 정보 보호 작업 처리가 결국 실패합니다. 따라서 개인 고객 데이터를 저장하기 위해 중첩된 맵 유형 필드를 사용하지 않는 것이 좋습니다. 관련 소비자 ID는 `identityMap` 레코드 기반 데이터 세트에 대한 필드(자체 맵 유형 필드) 또는 `endUserID` 시계열 기반 데이터 세트에 대한 필드입니다.
