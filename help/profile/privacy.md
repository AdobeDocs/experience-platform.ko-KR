---
keywords: Experience Platform;홈;인기 있는 주제
solution: Experience Platform
title: 실시간 고객 프로필에서 개인 정보 보호 요청 처리
type: Documentation
description: Adobe Experience Platform Privacy Service은 수많은 개인 정보 보호 규정에 명시된 대로 개인 데이터에 액세스하거나, 판매를 거부하거나, 삭제하기 위한 고객 요청을 처리합니다. 이 문서에서는 실시간 고객 프로필에 대한 개인 정보 보호 요청 처리와 관련된 필수 개념을 다룹니다.
exl-id: fba21a2e-aaf7-4aae-bb3c-5bd024472214
source-git-commit: 6eaa384feb1b84e6081f03cb4de9687ad26f437d
workflow-type: tm+mt
source-wordcount: '1757'
ht-degree: 1%

---

# [!DNL Real-Time Customer Profile]에서 개인 정보 보호 요청 처리 중

Adobe Experience Platform [!DNL Privacy Service]은(는) GDPR(일반 데이터 보호 규정) 및 CCPA([!DNL California Consumer Privacy Act])와 같은 개인 정보 보호 규정에 따라 기술된 대로 개인 데이터에 액세스하거나, 판매를 거부하거나, 삭제하도록 고객 요청을 처리합니다.

이 문서에서는 Adobe Experience Platform 내에서 [!DNL Real-Time Customer Profile]에 대한 개인 정보 보호 요청 처리와 관련된 필수 개념을 다룹니다.

>[!NOTE]
>
>이 안내서에서는 Experience Platform의 프로필 데이터 저장소에 대해 개인 정보 보호 요청을 하는 방법만 다룹니다. Experience Platform 데이터 레이크에 대한 개인 정보 보호 요청도 수행할 계획이라면 이 자습서 외에 [데이터 레이크의 개인 정보 보호 요청 처리](../catalog/privacy.md)에 대한 안내서를 참조하십시오.
>
>다른 Adobe Experience Cloud 애플리케이션에 대한 개인 정보 보호 요청을 하는 방법에 대한 단계는 [Privacy Service 설명서](../privacy-service/experience-cloud-apps.md)를 참조하십시오.

>[!IMPORTANT]
>
>이 안내서의 개인 정보 보호 요청은 B2B 비개인 엔터티를 지원하지 **않습니다**.

## 시작하기

이 안내서를 사용하려면 다음 [!DNL Experience Platform]개의 구성 요소를 제대로 이해하고 있어야 합니다.

* [[!DNL Privacy Service]](../privacy-service/home.md): Adobe Experience Cloud 애플리케이션에서 개인 데이터에 액세스하거나, 판매를 거부하거나, 삭제하기 위한 고객 요청을 관리합니다.
* [[!DNL Identity Service]](../identity-service/home.md): 장치 및 시스템 간에 ID를 연결하여 고객 경험 데이터의 단편화로 인해 발생하는 근본적인 문제를 해결합니다.
* [[!DNL Real-Time Customer Profile]](home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

## ID 네임스페이스 이해 {#namespaces}

Adobe Experience Platform [!DNL Identity Service]은(는) 시스템 및 장치 간에 고객 id 데이터를 브리지합니다. [!DNL Identity Service]은(는) **id 네임스페이스**&#x200B;를 사용하여 ID 값을 원본 시스템에 연결하여 컨텍스트를 제공합니다. 네임스페이스는 이메일 주소(&quot;이메일&quot;)와 같은 일반 개념을 나타내거나 Adobe Advertising Cloud ID(&quot;AdCloud&quot;) 또는 Adobe Target ID(&quot;TNTID&quot;)와 같은 특정 애플리케이션과 ID를 연결할 수 있습니다.

ID 서비스는 전역 정의(표준) 및 사용자 정의(사용자 정의) ID 네임스페이스 저장소를 유지 관리합니다. 표준 네임스페이스는 모든 조직에서 사용할 수 있으며(예: &quot;이메일&quot; 및 &quot;ECID&quot;), 조직에서는 특정 요구 사항에 맞게 사용자 정의 네임스페이스를 만들 수도 있습니다.

[!DNL Experience Platform]의 ID 네임스페이스에 대한 자세한 내용은 [ID 네임스페이스 개요](../identity-service/features/namespaces.md)를 참조하십시오.

## 요청 제출 {#submit}

아래 섹션에서는 [!DNL Privacy Service] API 또는 UI를 사용하여 [!DNL Real-Time Customer Profile]에 대한 개인 정보 보호 요청을 하는 방법에 대해 간략히 설명합니다. 이 섹션을 읽기 전에 [Privacy Service API](../privacy-service/api/getting-started.md) 또는 [Privacy Service UI](../privacy-service/ui/overview.md) 설명서를 검토하거나 알아 두어야 합니다. 이 문서에서는 요청 페이로드에서 제출된 사용자 ID 데이터의 형식을 제대로 지정하는 방법을 포함하여 개인 정보 보호 작업을 제출하는 방법에 대한 전체 단계를 제공합니다.

>[!IMPORTANT]
>
>Privacy Service에서는 ID 결합을 수행하지 않는 병합 정책을 사용해야만 [!DNL Profile] 데이터를 처리할 수 있습니다. 자세한 내용은 [병합 정책 제한](#merge-policy-limitations)의 섹션을 참조하십시오.
>
>개인 정보 보호 요청은 규정 요구 사항 내에서 비동기적으로 처리되며, 완료하는 데 걸리는 시간은 다를 수 있습니다. 요청이 계속 처리되는 동안 [!DNL Profile] 데이터가 변경되면 해당 수신 레코드도 해당 요청에서 처리되지 않을 수 있습니다. 개인 정보 보호 작업이 요청될 때 데이터 레이크 또는 프로필 저장소에 있는 프로필만 삭제됩니다. 삭제 작업 중에 삭제 요청 주체와 관련된 프로필 데이터를 수집하는 경우 모든 프로필 조각이 삭제되지는 않습니다.
>해당 데이터는 레코드 저장소에 삽입되므로 삭제 요청 시 Experience Platform 또는 Profile Service에서 들어오는 데이터를 아는 것은 사용자의 책임입니다. 삭제되었거나 삭제 중인 데이터 수집은 신중해야 합니다.

### API 사용

API에서 작업 요청을 만들 때 `userIDs` 내에 제공된 모든 ID는 특정 `namespace` 및 `type`을(를) 사용해야 합니다. [!DNL Identity Service]에서 인식하는 올바른 [ID 네임스페이스](#namespaces)을(를) `namespace` 값에 제공해야 하지만, `type`은(는) 각각 표준 및 사용자 지정 네임스페이스에 대해 `standard` 또는 `unregistered`이어야 합니다.

>[!NOTE]
>
>ID 그래프 및 프로필 조각이 Experience Platform 데이터 세트에서 배포되는 방식에 따라 각 고객에 대해 두 개 이상의 ID를 제공해야 할 수 있습니다. 자세한 내용은 다음 섹션 [프로필 조각](#fragments)을 참조하세요.

또한 요청 페이로드의 `include` 배열에는 요청을 수행하는 다른 데이터 저장소에 대한 제품 값이 포함되어야 합니다. ID와 연결된 프로필 데이터를 삭제하려면 배열에 값 `ProfileService`이(가) 포함되어야 합니다. 고객의 ID 그래프 연결을 삭제하려면 배열에 값 `identity`이(가) 포함되어야 합니다.

>[!NOTE]
>
>`include` 배열에서 `ProfileService` 및 `identity`을(를) 사용하는 영향에 대한 자세한 내용은 이 문서의 뒷부분에서 [프로필 요청 및 ID 요청](#profile-v-identity)에 대한 섹션을 참조하십시오.

다음 요청은 [!DNL Profile] 저장소에 있는 단일 고객 데이터에 대한 새 개인 정보 보호 작업을 만듭니다. `userIDs` 배열에서 고객에 대해 표준 `Email` ID 네임스페이스를 사용하는 ID 값과 사용자 지정 `Customer_ID` 네임스페이스를 사용하는 ID 값 두 개가 제공됩니다. `include` 배열의 [!DNL Profile]&#x200B;(`ProfileService`)에 대한 제품 값도 포함됩니다.

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
>Experience Platform은 조직에 속한 모든 [샌드박스](../sandboxes/home.md)에서 개인 정보 요청을 처리합니다. 따라서 요청에 포함된 모든 `x-sandbox-name` 헤더는 시스템에서 무시됩니다.

**제품 응답**

프로필 서비스의 경우 개인정보 보호 작업이 완료되면 요청된 사용자 ID에 대한 정보와 함께 JSON 형식으로 응답이 반환됩니다.

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

UI에서 작업 요청을 만들 때 데이터 레이크 또는 [!DNL Real-Time Customer Profile]에 저장된 데이터에 대한 작업을 처리하기 위해 **[!UICONTROL 제품]**&#x200B;에서 **[!UICONTROL AEP 데이터 레이크]** 및/또는 **[!UICONTROL 프로필]**&#x200B;을(를) 각각 선택하십시오.

![UI에서 액세스 작업 요청이 만들어지고 제품에서 프로필 옵션이 선택됨](./images/privacy/product-value.png)

## 개인 정보 보호 요청의 프로필 조각 {#fragments}

[!DNL Profile] 데이터 저장소에서 개별 고객의 개인 데이터는 종종 ID 그래프를 통해 사용자와 연결된 여러 프로필 조각으로 구성됩니다. [!DNL Profile] 스토어에 대한 개인 정보 보호 요청을 할 때는 전체 프로필이 아닌 프로필 조각 수준에서만 요청이 처리됩니다.

예를 들어 고객 속성 데이터를 세 개의 개별 데이터 세트에 저장하고, 서로 다른 식별자를 사용하여 해당 데이터를 개별 고객과 연결하는 상황을 생각해 보겠습니다.

| 데이터 세트 이름 | 기본 ID 필드 | 저장된 속성 |
| --- | --- | --- |
| 데이터 세트 1 | `customer_id` | `address` |
| 데이터 세트 2 | `email_id` | `firstName`, `lastName` |
| 데이터 세트 3 | `email_id` | `mlScore` |

데이터 세트 중 하나는 `customer_id`을(를) 기본 식별자로 사용하는 반면 다른 두 개의 데이터 세트는 `email_id`을(를) 사용합니다. `email_id`만 사용자 ID 값으로 사용하여 개인 정보 보호 요청(액세스 또는 삭제)을 전송하려는 경우 `firstName`, `lastName` 및 `mlScore` 특성만 처리되고 `address`은(는) 영향을 받지 않습니다.

개인 정보 보호 요청이 모든 관련 고객 속성을 처리하도록 하려면, 해당 속성이 저장될 수 있는 모든 적용 가능한 데이터 세트에 대한 기본 ID 값(고객당 최대 9개의 ID)을 제공해야 합니다. 일반적으로 ID로 표시되는 필드에 대한 자세한 내용은 스키마 컴포지션의 [기본 사항](../xdm/schema/composition.md#identity)에서 ID 필드에 대한 섹션을 참조하십시오.

## 삭제 요청 처리 {#delete}

[!DNL Experience Platform]이(가) [!DNL Privacy Service]에서 삭제 요청을 받으면 [!DNL Experience Platform]이(가) 요청이 수신되었고 영향을 받는 데이터가 삭제되도록 표시되었다는 확인을 [!DNL Privacy Service]에 보냅니다. 그런 다음 개인 정보 보호 작업이 완료되면 레코드가 제거됩니다.

>[!IMPORTANT]
>
>개인 정보 삭제 요청은 즉시 발생하지 않으며, 관련된 서비스 및 지리적 위치와 같은 기타 영향 요소에 따라 달라질 수 있습니다. 개인 정보 보호 작업 완료 기간은 15일에서 45일 사이일 수 있지만 보장되지는 않습니다.

프로필(`ProfileService`)에 대한 개인 정보 보호 요청에 ID 서비스(`identity`) 및 데이터 레이크(`aepDataLake`)도 제품으로 포함했는지 여부에 따라 프로필과 관련된 다른 데이터 집합이 잠재적으로 다른 시간에 시스템에서 제거됩니다.

| 포함된 제품 | 효과 |
| --- | --- |
| `ProfileService`만 | Privacy Service이 삭제 요청이 완료되었다는 확인을 전송하는 즉시 프로필이 삭제된 것으로 간주됩니다. 그러나 프로필의 ID 그래프는 여전히 남아 있으며 동일한 ID를 가진 새 데이터가 수집되면 프로필을 다시 구성할 수 있습니다. 프로필과 연결된 개인 식별되지 않는 데이터도 데이터 레이크에 남아 있습니다. |
| `ProfileService` 및 `identity` | Privacy Service에서 삭제 요청이 완료되었다는 확인을 전송하는 즉시 프로필 및 관련 ID 그래프가 즉시 삭제됩니다. 프로필과 연결된 개인 식별되지 않는 데이터도 데이터 레이크에 남아 있습니다. |
| `ProfileService` 및 `aepDataLake` | Privacy Service에서 삭제 요청이 완료되었다는 확인을 전송하는 즉시 프로필이 즉시 삭제됩니다. 그러나 프로필의 ID 그래프는 여전히 남아 있으며 동일한 ID를 가진 새 데이터가 수집되면 프로필을 다시 구성할 수 있습니다.<br><br>Data Lake 제품이 요청을 받았으며 현재 처리 중이라는 응답을 보내면 프로필과 연결된 데이터가 일시 삭제되므로 [!DNL Experience Platform] 서비스에서 액세스할 수 없습니다. 작업이 완료되면 데이터가 데이터 레이크에서 완전히 제거됩니다. |
| `ProfileService`, `identity` 및 `aepDataLake` | Privacy Service에서 삭제 요청이 완료되었다는 확인을 전송하는 즉시 프로필 및 관련 ID 그래프가 즉시 삭제됩니다.<br><br>Data Lake 제품이 요청을 받았으며 현재 처리 중이라는 응답을 보내면 프로필과 연결된 데이터가 일시 삭제되므로 [!DNL Experience Platform] 서비스에서 액세스할 수 없습니다. 작업이 완료되면 데이터가 데이터 레이크에서 완전히 제거됩니다. |

작업 상태 추적에 대한 자세한 내용은 [[!DNL Privacy Service] 설명서](../privacy-service/home.md#monitor)를 참조하세요.

### 프로필 요청 대 ID 요청 {#profile-v-identity}

프로필(`ProfileService`)에 대해 삭제 요청이 수행되었지만 ID 서비스(`identity`)가 아닌 경우 결과 작업은 고객(또는 고객 집합)에 대해 수집된 특성 데이터를 제거하지만 ID 그래프에 설정된 연결은 제거하지 않습니다.

예를 들어 고객의 `email_id` 및 `customer_id`을(를) 사용하는 삭제 요청은 해당 ID에 저장된 모든 특성 데이터를 제거합니다. 그러나 이후에 동일한 `customer_id`에서 수집된 데이터는 연결이 여전히 있으므로 해당 `email_id`과(와) 연결됩니다.

지정된 고객에 대한 프로필 및 모든 ID 연결을 제거하려면 삭제 요청에 Profile 및 Identity Service 를 대상 제품으로 포함해야 합니다.

### 병합 정책 제한 사항 {#merge-policy-limitations}

Privacy Service에서는 ID 결합을 수행하지 않는 병합 정책을 사용해야만 [!DNL Profile] 데이터를 처리할 수 있습니다. UI를 사용하여 개인 정보 보호 요청이 처리되고 있는지 확인하는 경우 **[!DNL None]**&#x200B;이(가) 포함된 정책을 [!UICONTROL ID 결합] 유형으로 사용하고 있는지 확인하십시오. 즉, [!UICONTROL ID 결합]이 [!UICONTROL 개인 그래프]&#x200B;(으)로 설정된 병합 정책을 사용할 수 없습니다.

>![병합 정책의 ID 결합이 없음으로 설정되어 있습니다](./images/privacy/no-id-stitch.png)

## 다음 단계

이 문서를 읽고 [!DNL Experience Platform]의 개인 정보 보호 요청 처리와 관련된 중요한 개념을 이해하게 되었습니다. ID 데이터를 관리하고 개인 정보 보호 작업을 만드는 방법을 깊이 이해하려면 이 안내서에 제공된 설명서를 계속 읽으십시오.

[!DNL Profile]에서 사용하지 않는 [!DNL Experience Platform] 리소스에 대한 개인 정보 보호 요청 처리에 대한 자세한 내용은 [데이터 레이크의 개인 정보 보호 요청 처리](../catalog/privacy.md)에 대한 문서를 참조하십시오.
