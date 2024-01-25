---
keywords: Experience Platform;홈;인기 항목;데이터 레이크 개인 정보;id 네임스페이스;개인 정보;데이터 레이크
solution: Experience Platform
title: 데이터 레이크에서 개인 정보 보호 요청 처리
description: Adobe Experience Platform Privacy Service은 법적 및 조직의 개인 정보 보호 규정에 명시된 대로 개인 데이터에 액세스하거나, 판매를 거부하거나, 삭제하기 위한 고객 요청을 처리합니다. 이 문서에서는 데이터 레이크에 저장된 고객 데이터에 대한 개인 정보 보호 요청 처리와 관련된 필수 개념을 다룹니다.
exl-id: c06b0a44-be1a-4938-9c3e-f5491a3dfc19
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1429'
ht-degree: 1%

---

# 데이터 레이크에서 개인 정보 보호 요청 처리

Adobe Experience Platform [!DNL Privacy Service] 는 법적 및 조직의 개인 정보 보호 규정에 명시된 대로 개인 데이터에 액세스하거나, 판매를 거부하거나, 삭제하도록 고객 요청을 처리합니다.

이 문서에서는 데이터 레이크에 저장된 고객 데이터에 대한 개인 정보 보호 요청 처리와 관련된 필수 개념을 다룹니다.

>[!NOTE]
>
>이 안내서에서는 Experience Platform의 데이터 레이크에 대해 개인 정보 보호 요청을 하는 방법만 다룹니다. Real-Time Customer Profile 데이터 저장소에 대한 개인 정보 보호 요청도 할 계획이라면 의 안내서를 참조하십시오. [프로필에 대한 개인 정보 보호 요청 처리](../profile/privacy.md) 이 튜토리얼 외에.
>
>다른 Adobe Experience Cloud 애플리케이션에 대한 개인 정보 보호 요청을 하는 방법에 대한 단계는 [Privacy Service 설명서](../privacy-service/experience-cloud-apps.md).

## 시작하기

다음 사항을 잘 알고 있는 것이 좋습니다 [!DNL Experience Platform] 이 안내서를 읽기 전의 서비스:

* [[!DNL Privacy Service]](../privacy-service/home.md): Adobe Experience Cloud 애플리케이션 전반에 걸친 개인 데이터 액세스, 판매 중지 또는 삭제에 대한 고객 요청을 관리합니다.
* [[!DNL Catalog Service]](home.md): 데이터 위치 및 내부 계보에 대한 레코드 시스템 [!DNL Experience Platform]. 데이터 세트 메타데이터를 업데이트하는 데 사용할 수 있는 API를 제공합니다.
* [[!DNL Experience Data Model (XDM) System]](../xdm/home.md): 표준화된 프레임워크 [!DNL Experience Platform] 고객 경험 데이터를 구성합니다.
* [[!DNL Identity Service]](../identity-service/home.md): 디바이스와 시스템 간에 ID를 연결하여 고객 경험 데이터의 단편화로 인해 발생하는 근본적인 문제를 해결합니다.

## ID 네임스페이스 이해 {#namespaces}

Adobe Experience Platform [!DNL Identity Service] 시스템 및 장치 간에 고객 id 데이터를 연결합니다. [!DNL Identity Service] 는 id 네임스페이스를 사용하여 id 값을 원래 시스템에 연결하여 컨텍스트를 id 값에 제공합니다. 네임스페이스는 이메일 주소(&quot;이메일&quot;)와 같은 일반적인 개념을 나타내거나 Adobe Advertising Cloud ID(&quot;AdCloud&quot;) 또는 Adobe Target ID(&quot;TNTID&quot;)와 같은 특정 애플리케이션과 ID를 연결할 수 있습니다.

[!DNL Identity Service] 는 전역 정의(표준) 및 사용자 정의(사용자 정의) id 네임스페이스 저장소를 유지 관리합니다. 표준 네임스페이스는 모든 조직에서 사용할 수 있으며(예: &quot;이메일&quot; 및 &quot;ECID&quot;), 조직에서는 특정 요구 사항에 맞게 사용자 정의 네임스페이스를 만들 수도 있습니다.

의 ID 네임스페이스에 대한 자세한 내용 [!DNL Experience Platform], 다음을 참조하십시오. [id 네임스페이스 개요](../identity-service/features/namespaces.md).

## 데이터 세트에 ID 데이터 추가

데이터 레이크에 대한 개인 정보 보호 요청을 만들 때 데이터를 찾고 적절하게 처리하려면 각 개별 고객에 대해 유효한 ID 값(및 관련 네임스페이스)이 제공되어야 합니다. 따라서 개인 정보 보호 요청의 대상이 되는 모든 데이터 세트에는 연관된 XDM 스키마에 ID 설명자가 포함되어야 합니다.

>[!NOTE]
>
>현재 ID 설명자 메타데이터를 지원하지 않는 스키마 기반의 모든 데이터 세트(예: 임시 데이터 세트)는 개인 정보 보호 요청에서 처리할 수 없습니다.

이 섹션에서는 기존 데이터 세트의 XDM 스키마에 ID 설명자를 추가하는 단계를 안내합니다. ID 설명자가 있는 데이터 세트가 이미 있는 경우 로 건너뛸 수 있습니다. [다음 섹션](#nested-maps).

>[!IMPORTANT]
>
>ID로 설정할 스키마 필드를 결정할 때는 다음 사항에 유의하십시오. [중첩된 맵 유형 필드 사용의 제한 사항](#nested-maps).

데이터 세트 스키마에 ID 설명자를 추가하는 방법에는 두 가지가 있습니다.

* [UI 사용](#identity-ui)
* [API 사용](#identity-api)

### UI 사용 {#identity-ui}

다음에서 [!DNL Experience Platform]사용자 인터페이스, **[!UICONTROL 스키마]** 작업 영역에서는 기존 XDM 스키마를 편집할 수 있습니다. 스키마에 ID 설명자를 추가하려면 목록에서 스키마를 선택하고 다음 단계를 수행합니다 [스키마 필드를 id 필드로 설정](../xdm/tutorials/create-schema-ui.md#identity-field) 다음에서 [!DNL Schema Editor] 튜토리얼.

스키마 내의 적절한 필드를 ID 필드로 설정한 다음에서 다음 섹션으로 진행할 수 있습니다. [개인 정보 보호 요청 제출](#submit).

### API 사용 {#identity-api}

>[!NOTE]
>
>이 섹션은 사용자가 데이터 세트 XDM 스키마의 고유 URI ID 값을 알고 있다고 가정합니다. 이 값을 모를 경우 [!DNL Catalog Service] API. 을(를) 읽은 후 [시작하기](./api/getting-started.md) 개발자 안내서 섹션에서 다음에 설명된 단계를 수행합니다. [목록 작성](./api/list-objects.md) 또는 [조회](./api/look-up-object.md) [!DNL Catalog] 개체를 사용하여 데이터 세트를 찾을 수 있습니다. 스키마 ID는에서 찾을 수 있습니다. `schemaRef.id`
>
>또한 이 섹션에서는 사용자가 스키마 레지스트리 API를 호출하는 방법을 알고 있다고 가정합니다. API 사용과 관련된 중요 정보(예: `{TENANT_ID}` 컨테이너의 개념은 [시작하기](../xdm/api/getting-started.md) 섹션에 자세히 설명되어 있습니다.

에 POST 요청을 하여 데이터 세트의 XDM 스키마에 ID 설명자를 추가할 수 있습니다. `/descriptors` 의 엔드포인트 [!DNL Schema Registry] API.

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
| `@type` | 생성 중인 설명자 유형. ID 설명자의 경우 값은 &quot;xdm:descriptorIdentity&quot;여야 합니다. |
| `xdm:sourceSchema` | 데이터 세트 XDM 스키마의 고유 URI ID. |
| `xdm:sourceVersion` | 에 지정된 XDM 스키마 버전 `xdm:sourceSchema`. |
| `xdm:sourceProperty` | 설명자가 적용되는 스키마 필드의 경로. |
| `xdm:namespace` | 다음 중 하나 [표준 id 네임스페이스](../privacy-service/api/appendix.md#standard-namespaces) 인식한 사람 [!DNL Privacy Service]또는 조직에서 정의한 사용자 정의 네임스페이스입니다. |
| `xdm:property` | 에서 사용 중인 네임스페이스에 따라 &quot;xdm:id&quot; 또는 &quot;xdm:code&quot; 중 하나 `xdm:namespace`. |
| `xdm:isPrimary` | 선택적 부울 값입니다. true이면 필드가 기본 ID임을 나타냅니다. 스키마에는 기본 ID가 하나만 포함될 수 있습니다. 포함되지 않은 경우 기본값은 false입니다. |

**응답**

성공적인 응답은 HTTP 상태 201(생성됨) 및 새로 생성된 설명자의 세부 정보를 반환합니다.

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
>이 섹션에서는 데이터 레이크에 대한 개인 정보 보호 요청을 포맷하는 방법을 다룹니다. 다음을 검토하는 것이 좋습니다. [[!DNL Privacy Service] UI](../privacy-service/ui/overview.md) 또는 [[!DNL Privacy Service] API](../privacy-service/api/getting-started.md) 요청 페이로드에서 제출된 사용자 id 데이터를 적절히 포맷하는 방법을 포함하여 개인 정보 보호 작업을 제출하는 방법에 대한 전체 단계에 대한 설명서입니다.

다음 섹션에서는 를 사용하여 데이터 레이크에 대한 개인 정보 보호 요청을 하는 방법에 대해 설명합니다. [!DNL Privacy Service] UI 또는 API.

>[!IMPORTANT]
>
>개인 정보 보호 요청이 완료되는 데 소요되는 시간은 보장되지 않습니다. 요청이 처리 중인 동안 데이터 레이크 내에서 변경 사항이 발생하는 경우 해당 레코드가 처리되는지 여부도 보장되지 않습니다.

### UI 사용

UI에서 작업 요청을 만들 때 다음을 선택해야 합니다. **[!UICONTROL AEP 데이터 레이크]** 아래에 **[!UICONTROL 제품]** 데이터 레이크에 저장된 데이터에 대한 작업을 처리합니다.

![개인 정보 보호 요청 만들기 대화 상자에서 선택한 데이터 레이크 제품을 보여 주는 이미지](./images/privacy/product-value.png)

### API 사용

API에서 작업 요청을 만들 때 `userIDs` 제공된 은 다음을 사용해야 합니다 `namespace` 및 `type` 데이터 저장소가 적용되는 데이터 저장소에 따라 다릅니다. 데이터 레이크의 ID는 `unregistered` 해당 사용자용 `type` 값 및 `namespace` 값과 일치하는 [개인 정보 보호 레이블](#privacy-labels) 해당 데이터 세트에 추가되었습니다.

또한 `include` 요청 페이로드의 배열에는 요청이 수행되는 다양한 데이터 저장소에 대한 제품 값이 포함되어야 합니다. 데이터 레이크에 요청할 때 배열에 값을 포함해야 합니다. `aepDataLake`.

다음 요청은 등록되지 않은 를 사용하여 데이터 레이크에 대한 새 개인 정보 보호 작업을 생성합니다 `email_label` 네임스페이스입니다. 또한 의 데이터 레이크에 대한 제품 값도 포함됩니다. `include` 배열:

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
>Platform은 모든 개인 정보 보호 요청을 처리합니다. [샌드박스](../sandboxes/home.md) 조직에 속해 있어야 합니다. 그 결과 `x-sandbox-name` 요청에 포함된 헤더는 시스템에서 무시됩니다.

## 삭제 요청 처리

날짜 [!DNL Experience Platform] 에서 삭제 요청을 수신합니다. [!DNL Privacy Service], [!DNL Platform] (으)로 확인 보내기 [!DNL Privacy Service] 요청을 수신하고 영향을 받는 데이터를 삭제하도록 표시했는지 여부. 그런 다음 7일 이내에 레코드가 데이터 레이크에서 제거됩니다. 7일 동안 데이터가 일시 삭제되므로 다른 사용자도 데이터에 액세스할 수 없습니다 [!DNL Platform] 서비스.

포함된 경우 `ProfileService` 또는 `identity` 개인 정보 보호 요청에서 관련 데이터는 별도로 처리됩니다. 의 섹션을 참조하십시오. [프로필에 대한 삭제 요청 처리](../profile/privacy.md#delete) 추가 정보.

## 다음 단계

이 문서를 읽으면 데이터 레이크에 대한 개인 정보 보호 요청 처리와 관련된 중요한 개념을 이해할 수 있습니다. ID 데이터를 관리하고 개인 정보 보호 작업을 만드는 방법에 대한 이해를 깊게 하기 위해 이 안내서 전반에 걸쳐 제공된 설명서를 계속 읽는 것이 좋습니다.

다음에 대한 문서 보기: [실시간 고객 프로필에 대한 개인 정보 보호 요청 처리](../profile/privacy.md) 에 대한 개인 정보 보호 요청을 처리하는 단계 [!DNL Profile] 저장.

## 부록

다음 섹션에는 데이터 레이크에서 개인 정보 보호 요청을 처리하는 데 필요한 추가 정보가 포함되어 있습니다.

### 중첩된 맵 유형 필드에 레이블 지정 {#nested-maps}

개인 정보 보호 레이블 지정을 지원하지 않는 중첩된 맵 유형 필드에는 두 가지 종류가 있습니다.

* 배열 유형 필드 내의 맵 유형 필드
* 다른 맵 유형 필드 내의 맵 유형 필드

위의 두 예 중 하나에 대한 개인 정보 보호 작업 처리는 결국 실패합니다. 이러한 이유로 중첩된 맵 유형 필드를 사용하여 개인 고객 데이터를 저장하지 않는 것이 좋습니다. 관련 소비자 ID는 내에 맵이 아닌 데이터 형식으로 저장해야 합니다. `identityMap` 레코드 기반 데이터 세트에 대한 필드(맵 유형 필드 자체) 또는 `endUserID` 시계열 기반 데이터 세트에 대한 필드입니다.
