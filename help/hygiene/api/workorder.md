---
title: 작업 주문 삭제 기록
description: 데이터 위생 API에서 /workorder 끝점을 사용하여 Adobe Experience Platform에서 레코드 삭제 작업 주문을 관리하는 방법을 알아봅니다. 이 안내서에서는 할당량, 처리 타임라인 및 API 사용을 다룹니다.
role: Developer
exl-id: f6d9c21e-ca8a-4777-9e5f-f4b2314305bf
source-git-commit: f1f37439bd4d77faf1015741e604eee7188c58d7
workflow-type: tm+mt
source-wordcount: '2440'
ht-degree: 1%

---

# 작업 주문 삭제 기록 {#work-order-endpoint}

데이터 위생 API의 `/workorder` 끝점을 사용하여 Adobe Experience Platform에서 레코드 삭제 작업 주문을 만들고, 보고, 관리합니다. 작업 주문을 통해 데이터 세트 간 데이터 제거를 제어, 모니터링 및 추적하여 데이터 품질을 유지하고 조직의 데이터 거버넌스 표준을 지원하는 데 도움이 됩니다.

>[!IMPORTANT]
>
>레코드 삭제 작업 주문은 데이터 정리, 익명 데이터 제거 또는 데이터 최소화를 위한 것입니다. **GDPR과 같은 개인 정보 보호 규정에 따른 데이터 주체 권한 요청에 대해 레코드 삭제 작업 지시를 사용하지 마십시오.** 준수 사용 사례의 경우 [Adobe Experience Platform Privacy Service](../../privacy-service/home.md)을(를) 사용하십시오.

## 시작

시작하기 전에 [개요](./overview.md)를 참조하여 필수 헤더, 샘플 API 호출 읽기 방법 및 관련 설명서를 찾을 위치에 대해 알아보십시오.

## 할당량 및 처리 타임라인 {#quotas}

기록 삭제 작업 지시는 조직의 라이선스 자격에 따라 결정되는 일별 및 월별 식별자 제출 제한을 따릅니다. 이러한 제한은 UI 및 API 기반 레코드 삭제 요청 모두에 적용됩니다.

>[!NOTE]
>
>하루에 최대 **1,000,000개의 식별자를 제출할 수 있습니다**. 단, 남은 월별 할당량이 허용하는 경우에만 제출합니다. 월별 상한이 100만 개 미만인 경우 일일 제출액은 해당 상한을 초과할 수 없습니다.

### 제품별 월별 제출 권한 {#quota-limits}

다음 표는 제품 및 자격 수준별 식별자 제출 제한을 보여 줍니다. 각 제품에 대해 월간 상한은 고정 식별자 천장이나 사용 허가된 데이터 볼륨에 연결된 백분율 기반 임계값의 두 값 중 적은 값입니다.

| 제품 | 권한 설명 | 월별 상한(둘 중 더 작은 값) |
|----------|-------------------------|---------------------------------|
| Real-Time CDP 또는 Adobe Journey Optimizer | Privacy and Security Shield 또는 Healthcare Shield 추가 기능 없음 | 식별자 2,000,000개 또는 대응 가능 대상의 5% |
| Real-Time CDP 또는 Adobe Journey Optimizer | Privacy and Security Shield 또는 Healthcare Shield 추가 기능 포함 | 식별자 15,000,000개 또는 대응 가능 대상의 10% |
| Customer Journey Analytics | Privacy and Security Shield 또는 Healthcare Shield 추가 기능 없음 | 2,000,000개의 식별자 또는 100개의 식별자/백만 CJA 권한 행당 |
| Customer Journey Analytics | Privacy and Security Shield 또는 Healthcare Shield 추가 기능 포함 | 15,000,000개의 식별자 또는 100만 개의 CJA 권한 행당 200개의 식별자 |

>[!NOTE]
>
>대부분의 조직에서는 실제 대응 가능 대상 또는 CJA 행 권한에 따라 월별 제한이 내려집니다.

>[!NOTE]
>
>할당량은 매월 1일에 재설정됩니다. 사용되지 않은 할당량은 **이월되지 않습니다**.

>[!NOTE]
>
>할당량 사용량은 **제출된 식별자**&#x200B;에 대한 조직의 라이선스가 부여된 월별 권한을 기준으로 합니다. 할당량은 시스템 가드레일에 의해 적용되지 않지만 모니터링 및 검토 될 수 있습니다.\
>레코드 삭제 작업 주문 용량은 **공유 서비스**&#x200B;입니다. 월간 캡은 Real-Time CDP, Adobe Journey Optimizer, Customer Journey Analytics 및 적용 가능한 모든 Shield 추가 기능에 걸쳐 가장 높은 권한을 반영합니다.

### 식별자 제출을 위한 처리 타임라인 {#sla-processing-timelines}

제출 후 레코드 삭제 작업 주문은 큐에 추가되며 사용자의 권한 수준에 따라 처리됩니다.

| 제품 및 자격 설명 | 대기열 기간 | 최대 처리 시간(SLA) |
|------------------------------------|---------------------|-------------------------------|
| Privacy and Security Shield 또는 Healthcare Shield 추가 기능 없음 | 최대 15일 | 30일 |
| Privacy and Security Shield 또는 Healthcare Shield 추가 기능 포함 | 일반적으로 24시간 | 15일 |

조직에서 더 높은 제한을 필요로 하는 경우 Adobe 담당자에게 권한 검토를 문의하십시오.

>[!TIP]
>
>현재 할당량 사용 또는 권한 계층을 확인하려면 [할당량 참조 안내서](../api/quota.md)를 참조하세요.

## 목록 레코드 삭제 작업 주문 {#list}

조직의 데이터 위생 작업에 대한 레코드 삭제 작업 주문의 페이지가 매겨진 목록을 검색합니다. 쿼리 매개 변수를 사용하여 결과를 필터링합니다. 각 작업 주문 레코드에는 작업 유형(예: `identity-delete`), 상태, 관련 데이터 세트 및 사용자 세부 정보, 감사 메타데이터가 포함됩니다.

**API 형식**

```http
GET /workorder
```

다음 테이블에서는 레코드 삭제 작업 지시를 나열하는 데 사용할 수 있는 쿼리 매개변수를 설명합니다.

| 쿼리 매개 변수 | 설명 |
| --------------- | ------------|
| `search` | author, displayName, description 또는 datasetName 필드에 대해 대소문자를 구분하지 않는 부분 일치(와일드카드 검색). 또한 정확한 만료 ID와 일치합니다. |
| `type` | 작업 주문 유형(예: `identity-delete`)별로 결과를 필터링합니다. |
| `status` | 작업 주문 상태를 쉼표로 구분한 목록. 상태 값은 대소문자를 구분합니다.<br>열거형: `received`, `validated`, `submitted`, `ingested`, `completed`, `failed` |
| `author` | 작업 순서를 가장 최근에 업데이트한 사람(또는 원래 작성자)을 찾습니다. 리터럴 또는 SQL 패턴을 허용합니다. |
| `displayName` | 작업 주문 표시 이름에 대해 대소문자를 구분하지 않습니다. |
| `description` | 작업 주문 설명에 대해 대/소문자를 구분하지 않는 일치 항목. |
| `workorderId` | 작업 주문 ID에 대한 정확한 일치. |
| `sandboxName` | 요청에 사용된 샌드박스 이름과 정확히 일치하거나 `*`을(를) 사용하여 모든 샌드박스를 포함하십시오. |
| `fromDate` | 이 날짜 또는 그 이후에 생성된 작업 주문으로 필터링합니다. `toDate`을(를) 설정해야 합니다. |
| `toDate` | 이 날짜 또는 이전에 생성된 작업 주문별로 필터링합니다. `fromDate`을(를) 설정해야 합니다. |
| `filterDate` | 이 날짜에 생성, 업데이트 또는 변경된 작업 주문만 반환합니다. |
| `page` | 반환할 페이지 색인(0에서 시작). |
| `limit` | 페이지당 최대 결과 수(1-100, 기본값: 25). |
| `orderBy` | 결과 정렬 순서. 오름차순/내림차순에는 `+` 또는 `-` 접두사를 사용하십시오. 예: `orderBy=-datasetName`. |
| `properties` | 결과당 포함할 추가 필드를 쉼표로 구분한 목록. 선택 사항입니다. |


**요청**

다음 요청은 완료된 모든 레코드 삭제 작업 지시를 페이지당 2개로 제한하여 검색합니다.

```shell
curl -X GET \
  "https://platform.adobe.io/data/core/hygiene/workorder?status=completed&limit=2" \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공적인 응답은 기록 삭제 작업 주문의 페이지가 매겨진 목록을 반환합니다.

```json
{
  "results": [
    {
      "workorderId": "DI-1729d091-b08b-47f4-923f-6a4af52c93ac",
      "orgId": "9C1F2AC143214567890ABCDE@AcmeOrg",
      "bundleId": "BN-4cfabf02-c22a-45ef-b21f-bd8c3d631f41",
      "action": "identity-delete",
      "createdAt": "2034-03-15T11:02:10.935Z",
      "updatedAt": "2034-03-15T11:10:10.938Z",
      "operationCount": 3,
      "targetServices": [
        "profile",
        "datalake",
        "identity"
      ],
      "status": "received",
      "createdBy": "a.stark@acme.com <a.stark@acme.com> BD8C3D631F41@acme.com",
      "datasetId": "a7b7c8f3a1b8457eaa5321ab",
      "datasetName": "Acme_Customer_Exports",
      "displayName": "Customer Identity Delete Request",
      "description": "Scheduled identity deletion for compliance"
    }
  ],
  "total": 1,
  "count": 1,
  "_links": {
    "next": {
      "href": "https://platform.adobe.io/workorder?page=1&limit=2",
      "templated": false
    },
    "page": {
      "href": "https://platform.adobe.io/workorder?limit={limit}&page={page}",
      "templated": true
    }
  }
}
```

다음 표에서는 응답의 속성에 대해 설명합니다.

| 속성 | 설명 |
| --- | --- |
| `results` | 레코드 삭제 작업 주문 개체의 배열입니다. 각 개체에는 아래 필드가 포함되어 있습니다. |
| `workorderId` | 작업 주문 삭제 레코드에 대한 고유 식별자입니다. |
| `orgId` | 고유한 조직 식별자. |
| `bundleId` | 해당 레코드가 포함된 번들의 작업 주문 삭제 고유 식별자입니다. 번들링을 사용하면 여러 삭제 주문을 그룹화하고 다운스트림 서비스에서 함께 처리할 수 있습니다. |
| `action` | 작업 주문에서 요청한 작업 유형입니다. |
| `createdAt` | 작업 순서가 생성된 타임스탬프. |
| `updatedAt` | 작업 주문이 마지막으로 업데이트된 타임스탬프입니다. |
| `operationCount` | 작업 주문에 포함된 작업 수입니다. |
| `targetServices` | 작업 주문에 대한 대상 서비스 목록입니다. |
| `status` | 작업 주문의 현재 상태입니다. 가능한 값은 `received`,`validated`, `submitted`, `ingested`, `completed` 및 `failed`입니다. |
| `createdBy` | 작업 주문을 만든 사용자의 이메일 및 식별자입니다. |
| `datasetId` | 작업 주문과 연계된 데이터 세트에 대한 고유 식별자. 요청이 모든 데이터 세트에 적용되는 경우 이 필드는 ALL로 설정됩니다. |
| `datasetName` | 작업 주문과 연계된 데이터 세트 이름. |
| `displayName` | 사람이 인식할 수 있는 작업 순서 레이블. |
| `description` | 작업 주문 목적에 대한 설명. |
| `total` | 쿼리와 일치하는 총 레코드 삭제 작업 주문 수 |
| `count` | 현재 페이지의 레코드 삭제 작업 주문 수 |
| `_links` | 페이지 매김 및 탐색 링크. |
| `next` | 다음 페이지의 `href`(문자열)과 `templated`(부울)이(가) 있는 개체입니다. |
| `page` | 페이지 탐색을 위한 `href`(문자열) 및 `templated`(부울)이(가) 있는 개체입니다. |

{style="table-layout:auto"}

## 레코드 만들기 삭제 작업 주문 {#create}

단일 데이터 세트 또는 모든 데이터 세트에서 하나 이상의 ID와 연결된 레코드를 삭제하려면 `/workorder` 끝점에 대한 POST 요청을 만듭니다.

작업 주문은 비동기적으로 처리되며 제출 후 작업 주문 목록에 나타납니다.

>[!TIP]
>
>API를 통해 제출된 각 레코드 삭제 작업 주문에는 최대 **100,000개의 ID**&#x200B;가 포함될 수 있습니다. 효율성을 극대화하기 위해 요청당 가능한 한 많은 ID를 제출합니다. 단일 ID 작업 주문과 같은 낮은 볼륨 제출을 방지합니다.

**API 형식**

```http
POST /workorder
```

>[!NOTE]
>
>연관된 XDM 스키마가 기본 ID 또는 ID 맵을 정의하는 데이터 세트에서만 레코드를 삭제할 수 있습니다.

>[!NOTE]
>
>이미 활성 만료가 있는 데이터 세트에 대해 레코드 삭제 작업 주문을 만들려고 하면 요청이 HTTP 400(잘못된 요청)을 반환합니다. 활성 만료는 아직 완료되지 않은 예약된 삭제입니다.

**요청**

다음 요청은 특정 데이터 세트에서 지정된 이메일 주소와 연관된 모든 레코드를 삭제합니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/hygiene/workorder \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "displayName": "Acme Loyalty - Customer Data Deletion",
        "description": "Delete all records associated with the specified email addresses from the Acme_Loyalty_2023 dataset.",
        "action": "delete_identity",
        "datasetId": "7eab61f3e5c34810a49a1ab3",
        "namespacesIdentities": [
          {
            "namespace": {
              "code": "email"
            },
            "IDs": [
              "alice.smith@acmecorp.com",
              "bob.jones@acmecorp.com",
              "charlie.brown@acmecorp.com"
            ]
          }
        ]
      }'
```

다음 표에서는 레코드 삭제 작업 순서를 만들기 위한 속성에 대해 설명합니다.

| 속성 | 설명 |
| --- | --- |
| `displayName` | 사람이 인식할 수 있는 이 레코드의 레이블은 작업 순서를 삭제합니다. |
| `description` | 작업 주문 삭제 레코드에 대한 설명. |
| `action` | 작업 주문 삭제 레코드에 대해 요청한 작업입니다. 특정 ID와 연결된 레코드를 삭제하려면 `delete_identity`을(를) 사용합니다. |
| `datasetId` | 데이터 세트에 대한 고유 식별자입니다. 특정 데이터 세트의 데이터 세트 ID를 사용하거나 `ALL`을(를) 사용하여 모든 데이터 세트를 대상으로 합니다. 데이터 세트에는 기본 ID 또는 ID 맵이 있어야 합니다. ID 맵이 있으면 `identityMap`(이)라는 최상위 수준의 필드로 표시됩니다.<br>데이터 집합 행의 ID 맵에는 여러 ID가 있을 수 있지만, 한 ID만 기본으로 표시할 수 있습니다. `"primary": true`이(가) 기본 ID와 일치하도록 하려면 `id`을(를) 포함해야 합니다. |
| `namespacesIdentities` | 각각 <br>을(를) 포함하는 개체 배열<ul><li> `namespace`: ID 네임스페이스를 지정하는 `code` 속성이 있는 개체(예: &quot;email&quot;).</li><li> `IDs`: 이 네임스페이스에 대해 삭제할 ID 값의 배열입니다.</li></ul>ID 네임스페이스는 ID 데이터에 컨텍스트를 제공합니다. Experience Platform에서 제공하는 표준 네임스페이스를 사용하거나 고유한 네임스페이스를 만들 수 있습니다. 자세한 내용은 [ID 네임스페이스 설명서](../../identity-service/features/namespaces.md) 및 [ID 서비스 API 사양](https://developer.adobe.com/experience-platform-apis/references/identity-service/#operation/getIdNamespaces)을 참조하세요. |

**응답**

성공적인 응답은 새 레코드 삭제 작업 주문의 세부 정보를 반환합니다.

```json
{
  "workorderId": "DI-95c40d52-6229-44e8-881b-fc7f072de63d",
  "orgId": "8B1F2AC143214567890ABCDE@AcmeOrg",
  "bundleId": "BN-c61bec61-5ce8-498f-a538-fb84b094adc6",
  "action": "identity-delete",
  "createdAt": "2035-06-02T09:21:00.000Z",
  "updatedAt": "2035-06-02T09:21:05.000Z",
  "operationCount": 1,
  "targetServices": [
    "profile",
    "datalake",
    "identity"
  ],
  "status": "received",
  "createdBy": "c.lannister@acme.com <c.lannister@acme.com> 7EAB61F3E5C34810A49A1AB3@acme.com",
  "datasetId": "7eab61f3e5c34810a49a1ab3",
  "datasetName": "Acme_Loyalty_2023",
  "displayName": "Loyalty Identity Delete Request",
  "description": "Schedule deletion for Acme loyalty program dataset"
}
```

다음 표에서는 응답의 속성에 대해 설명합니다.

| 속성 | 설명 |
| --- | --- |
| `workorderId` | 작업 주문 삭제 레코드에 대한 고유 식별자입니다. 이 값을 사용하여 삭제 상태 또는 세부 정보를 조회합니다. |
| `orgId` | 고유한 조직 식별자. |
| `bundleId` | 해당 레코드가 포함된 번들의 작업 주문 삭제 고유 식별자입니다. 번들링을 사용하면 여러 삭제 주문을 그룹화하고 다운스트림 서비스에서 함께 처리할 수 있습니다. |
| `action` | 작업 주문 삭제 레코드에 요청된 작업 유형입니다. |
| `createdAt` | 작업 순서가 생성된 타임스탬프. |
| `updatedAt` | 작업 주문이 마지막으로 업데이트된 타임스탬프입니다. |
| `operationCount` | 작업 주문에 포함된 작업 수입니다. |
| `targetServices` | 레코드 삭제 작업 주문에 대한 대상 서비스 목록입니다. |
| `status` | 작업 주문 삭제 레코드의 현재 상태. |
| `createdBy` | 레코드 삭제 작업 주문을 만든 사용자의 이메일 및 식별자입니다. |
| `datasetId` | 데이터 세트에 대한 고유 식별자입니다. 모든 데이터 세트에 대한 요청인 경우 값이 `ALL`(으)로 설정됩니다. |
| `datasetName` | 이 레코드의 작업 주문 삭제 데이터 세트 이름. |
| `displayName` | 사람이 인식할 수 있는 레코드 삭제 작업 순서 레이블. |
| `description` | 작업 주문 삭제 레코드에 대한 설명. |

{style="table-layout:auto"}

>[!NOTE]
>
>레코드 삭제 작업 주문에 대한 작업 속성은 현재 API 응답에서 `identity-delete`입니다. API가 다른 값(예: `delete_identity`)을 사용하도록 변경되면 이 설명서도 그에 따라 업데이트됩니다.

## 레코드 삭제 요청을 위해 ID 목록을 JSON으로 변환

식별자가 포함된 CSV, TSV 또는 TXT 파일에서 레코드 삭제 작업 순서를 만들려면 전환 스크립트를 사용하여 `/workorder` 끝점에 필요한 JSON 페이로드를 생성할 수 있습니다. 이 방법은 기존 데이터 파일로 작업할 때 특히 유용합니다. 즉시 사용할 수 있는 스크립트 및 포괄적인 지침을 보려면 [csv에서 데이터로 위생 GitHub 저장소](https://github.com/perlmonger42/csv-to-data-hygiene)를 방문하십시오.

### JSON 페이로드 생성

다음 bash 스크립트 예는 Python 또는 Ruby에서 변환 스크립트를 실행하는 방법을 보여줍니다.

>[!BEGINTABS]

>[!TAB Python 스크립트를 실행하는 예제]

```bash
#!/usr/bin/env bash

rm -rf ./output && mkdir output
for NAME in UTF8 CSV TSV TXT XYZ big; do
  ./csv-to-DI-payload.py sample/sample-$NAME.* \
      --verbose \
      --column 2 \
      --namespace email \
      --dataset-id 66f4161cc19b0f2aef3edf10 \
      --description 'a simple sample' \
      --output-dir output
  echo Checking output/sample-$NAME-*.json against expect/sample-$NAME-*.json
  diff <(cat output/sample-$NAME-*.json) <(cat expect/sample-$NAME-*.json) || echo Unexpected output in sample-$NAME-*.*
done
```

>[!TAB Ruby 스크립트를 실행하는 예제]

```bash
#!/usr/bin/env bash

rm -rf ./output && mkdir output
for NAME in UTF8 CSV TSV TXT XYZ big; do
  ./csv-to-DI-payload.rb sample/sample-$NAME.* \
      --verbose \
      --column 2 \
      --namespace email \
      --dataset-id 66f4161cc19b0f2aef3edf10 \
      --description 'a simple sample' \
      --output-dir output
  echo Checking output/sample-$NAME-*.json against expect/sample-$NAME-*.json
  diff <(cat output/sample-$NAME-*.json) <(cat expect/sample-$NAME-*.json) || echo Unexpected output in sample-$NAME-*.*
done
```

>[!ENDTABS]

아래 표에서는 기본 스크립트의 매개 변수에 대해 설명합니다.

| 매개변수 | 설명 |
| ---           | ---     |
| `verbose` | 자세한 정보 출력을 활성화합니다. |
| `column` | 삭제할 ID 값이 포함된 열의 인덱스(1 기반) 또는 헤더 이름입니다. 지정하지 않은 경우 기본값은 첫 번째 열로 설정됩니다. |
| `namespace` | ID 네임스페이스를 지정하는 `code` 속성이 있는 개체(예: &quot;email&quot;). |
| `dataset-id` | 작업 주문과 연계된 데이터 세트에 대한 고유 식별자. 요청이 모든 데이터 세트에 적용되는 경우 이 필드는 `ALL`(으)로 설정됩니다. |
| `description` | 작업 주문 삭제 레코드에 대한 설명. |
| `output-dir` | 출력 JSON 페이로드를 쓸 디렉터리입니다. |

{style="table-layout:auto"}

아래 예제는 CSV, TSV 또는 TXT 파일에서 변환된 성공적인 JSON 페이로드를 보여 줍니다. 지정된 네임스페이스와 연결된 레코드가 포함되어 있으며 전자 메일 주소로 식별된 레코드를 삭제하는 데 사용됩니다.

```json
{
  "action": "delete_identity",
  "datasetId": "66f4161cc19b0f2aef3edf10",
  "displayName": "output/sample-big-001.json",
  "description": "a simple sample",
  "identities": [
    {
      "namespace": {
        "code": "email"
      },
      "id": "1"
    },
    {
      "namespace": {
        "code": "email"
      },
      "id": "2"
    }
  ]
}
```

다음 표에서는 JSON 페이로드의 속성에 대해 설명합니다.

| 속성 | 설명 |
| ---          | ---     |
| `action` | 작업 주문 삭제 레코드에 대해 요청한 작업입니다. 변환 스크립트에 의해 자동으로 `delete_identity`(으)로 설정됩니다. |
| `datasetId` | 데이터 세트에 대한 고유 식별자입니다. |
| `displayName` | 사람이 인식할 수 있는 이 레코드의 레이블은 작업 순서를 삭제합니다. |
| `description` | 작업 주문 삭제 레코드에 대한 설명. |
| `identities` | 각각 <br>을(를) 포함하는 개체 배열<ul><li> `namespace`: ID 네임스페이스를 지정하는 `code` 속성이 있는 개체(예: &quot;email&quot;).</li><li> `id`: 이 네임스페이스에 대해 삭제할 ID 값입니다.</li></ul> |

{style="table-layout:auto"}

### 생성된 JSON 데이터를 `/workorder` 끝점에 제출

요청을 제출하려면 [레코드 삭제 작업 주문 만들기](#create) 섹션의 지침을 따르십시오. `-d` POST 요청을 `curl` API 끝점으로 보낼 때 변환된 JSON 페이로드를 요청 본문(`/workorder`)으로 사용해야 합니다.

## 특정 레코드 삭제 작업 주문에 대한 세부 정보 검색 {#lookup}

`/workorder/{WORKORDER_ID}`에 GET을 요청하여 특정 레코드 삭제 작업 주문에 대한 정보를 검색합니다. 응답에는 작업 유형, 상태, 관련 데이터 세트 및 사용자 정보, 감사 메타데이터가 포함됩니다.

**API 형식**

```http
GET /workorder/{WORKORDER_ID}
```

| 매개변수 | 설명 |
| --- | --- |
| `{WORK_ORDER_ID}` | 조회하고 있는 레코드 삭제 작업 주문에 대한 고유 식별자입니다. |

{style="table-layout:auto"}

**요청**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/hygiene/workorder/DI-6fa98d52-7bd2-42a5-bf61-fb5c22ec9427 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

성공한 응답은 지정된 레코드 삭제 작업 주문의 세부 정보를 반환합니다.

```json
{
  "workorderId": "DI-6fa98d52-7bd2-42a5-bf61-fb5c22ec9427",
  "orgId": "3C7F2AC143214567890ABCDE@AcmeOrg",
  "bundleId": "BN-dbe3ffad-cb0b-401f-91ae-01c189f8e7b2",
  "action": "identity-delete",
  "createdAt": "2037-01-21T08:25:45.119Z",
  "updatedAt": "2037-01-21T08:30:45.233Z",
  "operationCount": 3,
  "targetServices": [
    "ajo",
    "profile",
    "datalake",
    "identity"
  ],
  "status": "received",
  "createdBy": "g.baratheon@acme.com <g.baratheon@acme.com> C189F8E7B2@acme.com",
  "datasetId": "d2f1c8a4b8f747d0ba3521e2",
  "datasetName": "Acme_Marketing_Events",
  "displayName": "Marketing Identity Delete Request",
  "description": "Scheduled identity deletion for marketing compliance"
}
```

다음 표에서는 응답의 속성에 대해 설명합니다.

| 속성 | 설명 |
| --- | --- |
| `workorderId` | 작업 주문 삭제 레코드에 대한 고유 식별자입니다. |
| `orgId` | 조직의 고유 식별자입니다. |
| `bundleId` | 해당 레코드가 포함된 번들의 작업 주문 삭제 고유 식별자입니다. 번들링을 사용하면 여러 삭제 주문을 그룹화하고 다운스트림 서비스에서 함께 처리할 수 있습니다. |
| `action` | 작업 주문 삭제 레코드에 요청된 작업 유형입니다. |
| `createdAt` | 작업 순서가 생성된 타임스탬프. |
| `updatedAt` | 작업 주문이 마지막으로 업데이트된 타임스탬프입니다. |
| `operationCount` | 작업 주문에 포함된 작업 수입니다. |
| `targetServices` | 이 레코드의 영향을 받은 대상 서비스 목록 삭제 작업 순서. |
| `status` | 작업 주문 삭제 레코드의 현재 상태. |
| `createdBy` | 레코드 삭제 작업 주문을 만든 사용자의 이메일 및 식별자입니다. |
| `datasetId` | 작업 주문과 연계된 데이터 세트에 대한 고유 식별자. |
| `datasetName` | 작업 주문과 연계된 데이터 세트 이름. |
| `displayName` | 사람이 인식할 수 있는 레코드 삭제 작업 순서 레이블. |
| `description` | 작업 주문 삭제 레코드에 대한 설명. |

## 레코드 삭제 작업 주문 업데이트

`name` 끝점에 대한 PUT 요청을 수행하여 레코드 삭제 작업 순서에 대한 `description` 및 `/workorder/{WORKORDER_ID}`을(를) 업데이트합니다.

**API 형식**

```http
PUT /workorder/{WORKORDER_ID}
```

다음 표에서는 이 요청의 매개 변수에 대해 설명합니다.

| 매개변수 | 설명 |
| --- | --- |
| `{WORK_ORDER_ID}` | 업데이트할 레코드 삭제 작업 주문의 고유 식별자입니다. |

{style="table-layout:auto"}

**요청**

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/hygiene/workorder/DI-893a6b1d-47c2-41e1-b3f1-2d7c2956aabb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Updated Marketing Identity Delete Request",
        "description": "Updated deletion request for marketing data"
      }'
```

다음 표에서는 업데이트할 수 있는 속성에 대해 설명합니다.

| 속성 | 설명 |
| --- | --- |
| `name` | 사람이 인식할 수 있는 업데이트된 레코드 삭제 작업 순서 레이블. |
| `description` | 작업 주문 삭제 레코드에 대한 업데이트된 설명. |

{style="table-layout:auto"}

**응답**

성공적인 응답이 업데이트된 작업 주문 요청을 반환합니다.

```json
{
  "workorderId": "DI-893a6b1d-47c2-41e1-b3f1-2d7c2956aabb",
  "orgId": "7D4E2AC143214567890ABCDE@AcmeOrg",
  "bundleId": "BN-12abcf45-32ea-45bc-9d1c-8e7b321cabc8",
  "action": "identity-delete",
  "createdAt": "2038-04-15T12:14:29.210Z",
  "updatedAt": "2038-04-15T12:30:29.442Z",
  "operationCount": 2,
  "targetServices": [
    "profile",
    "datalake"
  ],
  "status": "received",
  "createdBy": "b.tarth@acme.com <b.tarth@acme.com> 8E7B321CABC8@acme.com",
  "datasetId": "1a2b3c4d5e6f7890abcdef12",
  "datasetName": "Acme_Marketing_2024",
  "displayName": "Updated Marketing Identity Delete Request",
  "description": "Updated deletion request for marketing data",
  "productStatusDetails": [
        {
            "productName": "Data Management",
            "productStatus": "waiting",
            "createdAt": "2024-06-12T20:11:18.447747Z"
        },
        {
            "productName": "Identity Service",
            "productStatus": "success",
            "createdAt": "2024-06-12T20:36:09.020832Z"
        },
        {
            "productName": "Profile Service",
            "productStatus": "waiting",
            "createdAt": "2024-06-12T20:11:18.447747Z"
        },
        {
            "productName": "Journey Orchestrator",
            "productStatus": "success",
            "createdAt": "2024-06-12T20:12:19.843199Z"
        }
    ]
}
```

| 속성 | 설명 |
| ---------------- | ----------------------------------------------------------------------------------------- |
| `workorderId` | 작업 주문 삭제 레코드에 대한 고유 식별자입니다. |
| `orgId` | 조직의 고유 식별자입니다. |
| `bundleId` | 해당 레코드가 포함된 번들의 작업 주문 삭제 고유 식별자입니다. 번들링을 사용하면 여러 삭제 주문을 그룹화하고 다운스트림 서비스에서 함께 처리할 수 있습니다. |
| `action` | 작업 주문 삭제 레코드에 요청된 작업 유형입니다. |
| `createdAt` | 작업 순서가 생성된 타임스탬프. |
| `updatedAt` | 작업 주문이 마지막으로 업데이트된 타임스탬프입니다. |
| `operationCount` | 작업 주문에 포함된 작업 수입니다. |
| `targetServices` | 이 레코드의 영향을 받은 대상 서비스 목록 삭제 작업 순서. |
| `status` | 작업 주문 삭제 레코드의 현재 상태. 가능한 값은 `received`,`validated`, `submitted`, `ingested`, `completed` 및 `failed`입니다. |
| `createdBy` | 레코드 삭제 작업 주문을 만든 사용자의 이메일 및 식별자입니다. |
| `datasetId` | 레코드 삭제 작업 주문에 연결된 데이터 세트에 대한 고유 식별자입니다. |
| `datasetName` | 레코드 삭제 작업 주문과 연결된 데이터 세트의 이름입니다. |
| `displayName` | 사람이 인식할 수 있는 레코드 삭제 작업 순서 레이블. |
| `description` | 작업 주문 삭제 레코드에 대한 설명. |
| `productStatusDetails` | 요청에 대한 다운스트림 프로세스의 현재 상태를 나열하는 배열입니다. 각 객체에는 다음이 포함됩니다.<ul><li>`productName`: 다운스트림 서비스의 이름입니다.</li><li>`productStatus`: 다운스트림 서비스의 현재 처리 상태입니다.</li><li>`createdAt`: 서비스에서 가장 최근 상태를 게시한 타임스탬프입니다.</li></ul>이 속성은 처리를 시작하기 위해 작업 주문이 다운스트림 서비스에 제출된 후에 사용할 수 있습니다. |

{style="table-layout:auto"}
