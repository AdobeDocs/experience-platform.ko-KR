---
keywords: Experience Platform;홈;인기 있는 주제
solution: Experience Platform
title: 실시간 고객 프로필의 개인 정보 보호 요청 처리
type: Documentation
description: Adobe Experience Platform Privacy Service은 다양한 개인 정보 보호 규정에 따라 지정된 대로 고객 개인 데이터에 대한 액세스, 판매 거부 또는 삭제 요청을 처리합니다. 이 문서에서는 실시간 고객 프로필의 개인 정보 보호 요청 처리와 관련된 필수 개념을 다룹니다.
exl-id: fba21a2e-aaf7-4aae-bb3c-5bd024472214
source-git-commit: d41606e4df297d11b4e0e755363d362e075e862c
workflow-type: tm+mt
source-wordcount: '1573'
ht-degree: 0%

---

# 의 개인 정보 보호 요청 처리 [!DNL Real-Time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] 는 GDPR(General Data Protection Regulation) 및 와 같은 개인 정보 보호 규정에 따라 지정된 대로 고객 개인 데이터에 대한 액세스, 판매 거부 또는 삭제 요청을 처리합니다 [!DNL California Consumer Privacy Act] (CCPA).

이 문서에서는 [!DNL Real-Time Customer Profile] Adobe Experience Platform 내에서 사용할 수 있습니다.

>[!NOTE]
>
>이 안내서에서는 Experience Platform의 프로필 데이터 저장소에 대해 개인 정보 보호 요청을 하는 방법만 다룹니다. 플랫폼 데이터 레이크에 대한 개인 정보 보호 요청을 수행하려는 경우 [data lake의 개인 정보 보호 요청 처리](../catalog/privacy.md) 추가 정보.
>
>다른 Adobe Experience Cloud 애플리케이션에 대해 개인 정보 보호 요청을 수행하는 방법에 대한 단계는 [Privacy Service 설명서](../privacy-service/experience-cloud-apps.md).

## 시작하기

이 안내서에서는 다음을 이해하기 위해 작업해야 합니다 [!DNL Platform] 구성 요소:

* [[!DNL Privacy Service]](../privacy-service/home.md): Adobe Experience Cloud 애플리케이션에서 개인 데이터를 액세스, 판매 거부 또는 삭제하기 위한 고객 요청을 관리합니다.
* [[!DNL Identity Service]](../identity-service/home.md): 여러 장치 및 시스템에서 ID를 브리징하여 고객 경험 데이터의 분화로 인한 근본적인 문제를 해결합니다.
* [[!DNL Real-Time Customer Profile]](home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

## ID 네임스페이스 이해 {#namespaces}

Adobe Experience Platform [!DNL Identity Service] 는 시스템 및 장치에서 고객 ID 데이터를 전달합니다. [!DNL Identity Service] 사용 **id 네임스페이스** ID 값에 컨텍스트를 제공하는 데 사용할 수 있습니다. 네임스페이스는 이메일 주소(&quot;이메일&quot;)와 같은 일반적인 개념을 나타내거나 ID를 Adobe Advertising Cloud ID(&quot;AdCloud&quot;) 또는 Adobe Target ID(&quot;TNTID&quot;)와 같은 특정 애플리케이션과 연결할 수 있습니다.

ID 서비스는 전역적으로 정의된(표준) 및 사용자 정의(사용자 정의) ID 네임스페이스의 저장소를 유지 관리합니다. 표준 네임스페이스는 모든 조직(예: &quot;이메일&quot; 및 &quot;ECID&quot;)에서 사용할 수 있지만 조직은 특정 요구 사항에 맞게 사용자 지정 네임스페이스를 만들 수도 있습니다.

의 ID 네임스페이스에 대한 자세한 내용은 [!DNL Experience Platform]를 참조하고 [id 네임스페이스 개요](../identity-service/namespaces.md).

## 요청 제출 {#submit}

아래 섹션에서는 개인 정보 보호 요청을 수행하는 방법에 대해 간략하게 설명합니다 [!DNL Real-Time Customer Profile] 사용 [!DNL Privacy Service] API 또는 UI. 이러한 섹션을 읽기 전에 [Privacy Service API](../privacy-service/api/getting-started.md) 또는 [Privacy Service UI](../privacy-service/ui/overview.md) 문서 를 참조하십시오.

>[!IMPORTANT]
>
>Privacy Service은 처리할 수만 있습니다 [!DNL Profile] ID 결합을 수행하지 않는 병합 정책을 사용하는 데이터. 의 섹션을 참조하십시오. [정책 제한 사항 병합](#merge-policy-limitations) 추가 정보.
>
>개인 정보 보호 요청을 완료하는 데 걸리는 시간에 유의하십시오 **사용할 수 없음** 보증됩니다. 에서 변경 사항이 발생하는 경우 [!DNL Profile] 요청이 여전히 처리 중인 동안 해당 레코드가 처리되는지 여부도 보장할 수 없습니다.

### API 사용

API에서 작업 요청을 만들 때 내에 제공된 모든 ID입니다 `userIDs` 특정 `namespace` 및 `type`. 유효한 [id 네임스페이스](#namespaces) 인식자 [!DNL Identity Service] 는 `namespace` 값, `type` 다음 중 하나여야 합니다. `standard` 또는 `unregistered` (표준 및 사용자 지정 네임스페이스의 경우 각각).

>[!NOTE]
>
>ID 그래프와 프로필 조각이 Platform 데이터 세트에 배포되는 방법에 따라 각 고객에 대해 두 개 이상의 ID를 제공해야 할 수 있습니다. 다음 섹션을 참조하십시오 [프로필 조각](#fragments) 추가 정보.

또한 `include` 요청 페이로드 배열에는 요청이 수행되고 있는 다양한 데이터 저장소의 제품 값이 포함되어야 합니다. ID와 연결된 프로필 데이터를 삭제하려면 배열에 값이 포함되어야 합니다 `ProfileService`. 고객의 ID 그래프 연결을 삭제하려면 배열에 값이 포함되어야 합니다 `identity`.

>[!NOTE]
>
>의 섹션을 참조하십시오. [프로필 요청 및 ID 요청](#profile-v-identity) 의 사용에 대한 효과에 대한 자세한 내용은 이 문서의 뒷부분에서 참조하십시오 `ProfileService` 및 `identity` 내 `include` 배열입니다.

다음 요청은 의 단일 고객 데이터에 대한 새 개인 정보 작업을 만듭니다 [!DNL Profile] 저장. 에서는 고객에 대해 두 개의 ID 값이 제공됩니다 `userIDs` 배열; 표준 `Email` id 네임스페이스 및 사용자 지정 `Customer_ID` 네임스페이스. 여기에는 다음에 대한 제품 값도 포함됩니다 [!DNL Profile] (`ProfileService`)을 클릭하여 제품에서 사용할 수 있습니다. `include` 배열:

**요청**

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
            "namespace": "Email",
            "value": "ajones@acme.com",
            "type": "standard"
          },
          {
            "namespace": "Customer_ID",
            "value": "12345678",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["ProfileService","identity"],
    "expandIds": false,
    "priority": "normal",
    "regulation": "ccpa"
}'
```

>[!IMPORTANT]
>
>플랫폼은 모든 위치에서 개인 정보 요청을 처리합니다 [샌드박스](../sandboxes/home.md) 조직에 속해 있어야 합니다. 따라서, 모든 `x-sandbox-name` 요청에 포함된 헤더는 시스템에서 무시됩니다.

**제품 응답**

프로필 서비스의 경우 개인 정보 작업이 완료되면 요청된 사용자 ID에 대한 정보가 포함된 응답이 JSON 형식으로 반환됩니다.

```json
{
    "privacyResponse": {
        "jobId": "7467850f-9698-11ed-8635-355435552164",
        "response": [
            {
                "sandbox": "prod",
                "mergePolicyId": "none",
                "result": {
                    "person": {
                        "gender": "female"           
                    },
                    "personalEmail": {
                        "address": "ajones@acme.com",
                    },
                    "identityMap": {
                        "crmid": [
                            {
                                "id": "5b7db37a-bc7a-46a2-a63e-2cfe7e1cc068"
                            }
                        ]
                    }
                }
            },
            {
                "sandbox": "prod",
                "mergePolicyId": "none",
                "result": {
                    "person": {
                        "gender": "male"
                    },
                    "id": 12345678,
                    "identityMap": {
                        "crmid": [
                            {
                                "id": "e9d439f2-f5e4-4790-ad67-b13dbd89d52e"
                            }
                        ]
                    }
                }
            }
        ]
    }
}
```

### UI 사용

UI에서 작업 요청을 만들 때는 반드시 선택해야 합니다 **[!UICONTROL AEP Data Lake]** 및/또는 **[!UICONTROL 프로필]** 아래에 **[!UICONTROL 제품]** data lake 또는 [!DNL Real-Time Customer Profile]각각 입니다.

![제품 아래에 프로필 옵션이 선택된 상태로 UI에서 생성 중인 액세스 작업 요청](./images/privacy/product-value.png)

## 개인 정보 요청의 프로필 조각 {#fragments}

에서 [!DNL Profile] 데이터 저장소 개별 고객에 대한 개인 데이터는 ID 그래프를 통해 사용자와 연결된 여러 프로필 조각으로 구성되는 경우가 많습니다. 에 개인 정보를 요청할 때 [!DNL Profile] 저장 시, 요청은 전체 프로필이 아닌 프로필 조각 수준에서만 처리됩니다.

예를 들어, 서로 다른 식별자를 사용하여 해당 데이터를 개별 고객과 연결하는 세 개의 개별 데이터 세트에 고객 특성 데이터를 저장하는 상황을 생각해 보십시오.

| 데이터 세트 이름 | 기본 ID 필드 | 저장된 속성 |
| --- | --- | --- |
| 데이터 세트 1 | `customer_id` | `address` |
| 데이터 세트 2 | `email_id` | `firstName`, `lastName` |
| 데이터 세트 3 | `email_id` | `mlScore` |

데이터 세트 중 하나는 를 사용합니다 `customer_id` 는 기본 식별자로 사용되지만 다른 두 식별자는 `email_id`. 개인 정보 보호 요청(액세스 또는 삭제)을 `email_id` 를 사용자 ID 값으로 채우면 됩니다. `firstName`, `lastName`, 및 `mlScore` 속성이 처리되는 반면 `address` 영향을 받지 않습니다.

개인 정보 보호 요청이 모든 관련 고객 속성을 처리하도록 하려면 해당 속성을 저장할 수 있는 모든 적용 가능한 데이터 세트에 대한 기본 ID 값을 제공해야 합니다(고객당 최대 9개의 ID). 의 ID 필드에 대한 섹션을 참조하십시오. [스키마 구성 기본 사항](../xdm/schema/composition.md#identity) id로 일반적으로 표시된 필드에 대한 자세한 내용은 다음을 참조하십시오.

## 요청 처리 삭제 {#delete}

When [!DNL Experience Platform] 에서 삭제 요청을 받습니다. [!DNL Privacy Service], [!DNL Platform] 에 확인 보내기 [!DNL Privacy Service] 요청이 수신되고 영향을 받는 데이터가 삭제로 표시되었음을 나타냅니다. 그런 다음 개인 정보 작업이 완료되면 레코드가 제거됩니다.

ID 서비스(`identity`) 및 data lake(`aepDataLake`)을 제품(`ProfileService`). 프로필과 관련된 서로 다른 데이터 세트가 잠재적으로 다른 시점에 시스템에서 제거됩니다.

| 포함된 제품 | 효과 |
| --- | --- |
| `ProfileService` 전용 | Platform이 삭제 요청을 수신했다는 확인을 전송하는 즉시 프로필이 삭제됩니다. 하지만 프로필의 ID 그래프는 여전히 남아 있으며 동일한 ID를 사용하는 새 데이터를 수집할 수 있습니다. 프로필과 연결된 데이터도 데이터 레이크에 유지됩니다. |
| `ProfileService` 및 `identity` | Platform이 삭제 요청을 수신했다는 확인을 전송하는 즉시 프로필 및 관련 ID 그래프가 삭제됩니다. 프로필과 연관된 데이터는 데이터 레이크에 유지됩니다. |
| `ProfileService` 및 `aepDataLake` | Platform이 삭제 요청을 수신했다는 확인을 전송하는 즉시 프로필이 삭제됩니다. 하지만 프로필의 ID 그래프는 여전히 남아 있으며 동일한 ID를 사용하는 새 데이터를 수집할 수 있습니다.<br><br>Data Lake 제품이 요청을 받고 현재 처리 중임을 응답하면 프로필과 연결된 데이터가 소프트 삭제되므로 다른 제품도 액세스할 수 없습니다 [!DNL Platform] 서비스. 작업이 완료되면 데이터가 데이터 레이크에서 완전히 제거됩니다. |
| `ProfileService`, `identity`, 및 `aepDataLake` | Platform이 삭제 요청을 수신했다는 확인을 전송하는 즉시 프로필 및 관련 ID 그래프가 삭제됩니다.<br><br>Data Lake 제품이 요청을 받고 현재 처리 중임을 응답하면 프로필과 연결된 데이터가 소프트 삭제되므로 다른 제품도 액세스할 수 없습니다 [!DNL Platform] 서비스. 작업이 완료되면 데이터가 데이터 레이크에서 완전히 제거됩니다. |

자세한 내용은 [[!DNL Privacy Service] 설명서](../privacy-service/home.md#monitor) 작업 상태 추적에 대한 자세한 내용을 참조하십시오.

### 프로필 요청 및 ID 요청 {#profile-v-identity}

프로필에 대해 삭제 요청이 수행된 경우(`ProfileService`)이지만 ID 서비스(`identity`). 결과 작업은 고객(또는 고객 세트)에 대해 수집된 속성 데이터를 제거하지만 identity 그래프에 설정된 연관은 제거하지 않습니다.

예를 들어 고객의 `email_id` 및 `customer_id` 는 해당 ID에 저장된 모든 속성 데이터를 제거합니다. 그러나 이후에 수집된 모든 데이터는 동일한 위치에서 수집됩니다 `customer_id` 은 여전히 적절한 `email_id`: 연결이 아직 있으므로

지정된 고객에 대한 프로필 및 모든 ID 연결을 제거하려면 삭제 요청에 프로필 및 ID 서비스를 모두 대상 제품으로 포함해야 합니다.

### 병합 정책 제한 사항 {#merge-policy-limitations}

Privacy Service은 처리할 수만 있습니다 [!DNL Profile] ID 결합을 수행하지 않는 병합 정책을 사용하는 데이터. UI를 사용하여 개인 정보 보호 요청이 처리되는지 확인하는 경우 **[!DNL None]** 로서의 [!UICONTROL ID 결합] 유형. 즉, [!UICONTROL ID 결합] 가 로 설정되어 있습니다. [!UICONTROL 비공개 그래프].
>![병합 정책의 ID 결합이 없음으로 설정되어 있습니다](./images/privacy/no-id-stitch.png)
>
## 다음 단계

이 문서를 읽은 후에는 의 개인 정보 보호 요청 처리와 관련된 중요한 개념을 도입했습니다 [!DNL Experience Platform]. ID 데이터를 관리하고 개인 정보 보호 작업을 만드는 방법에 대한 이해를 높이려면 이 안내서 전체에서 제공된 설명서를 계속 읽으십시오.

에 대한 개인 정보 보호 요청 처리에 대한 자세한 내용은 [!DNL Platform] 에서 사용하지 않는 리소스 [!DNL Profile]에서 문서를 참조하십시오. [data lake의 개인 정보 보호 요청 처리](../catalog/privacy.md).
