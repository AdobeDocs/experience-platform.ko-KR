---
keywords: Experience Platform;홈;인기 항목
solution: Experience Platform
title: 실시간 고객 프로필의 개인 정보 요청 처리
topic-legacy: overview
type: Documentation
description: Adobe Experience Platform Privacy Service은 다양한 개인 정보 보호 규정에 따라 고객의 개인 데이터 액세스, 판매 거부 또는 삭제를 처리합니다. 이 문서에서는 실시간 고객 프로파일에 대한 개인정보 보호 요청 처리와 관련된 중요한 개념을 설명합니다.
exl-id: fba21a2e-aaf7-4aae-bb3c-5bd024472214
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1091'
ht-degree: 0%

---

# [!DNL Real-time Customer Profile]의 개인 정보 요청 처리

Adobe Experience Platform [!DNL Privacy Service]은(는) GDPR(General Data Protection Regulation) 및 [!DNL California Consumer Privacy Act](CCPA)와 같은 개인 정보 보호 규정에 따라 고객의 개인 정보에 액세스하거나, 판매를 거부하거나, 삭제하도록 요청을 처리합니다.

이 문서에서는 [!DNL Real-time Customer Profile]에 대한 개인 정보 요청 처리와 관련된 중요한 개념을 다룹니다.

## 시작하기

이 안내서를 읽기 전에 다음 [!DNL Experience Platform] 서비스에 대한 작업 이해를 구하는 것이 좋습니다.

* [[!DNL Privacy Service]](home.md):Adobe Experience Cloud 애플리케이션에서 개인 데이터를 액세스, 판매 거부 또는 삭제하기 위한 고객 요청을 관리합니다.
* [[!DNL Identity Service]](../identity-service/home.md):디바이스 및 시스템 간의 ID를 결합함으로써 고객 경험 데이터의 세분화로 인해 발생하는 기본적인 문제를 해결합니다.
* [[!DNL Real-time Customer Profile]](../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

## ID 네임스페이스 {#namespaces} 이해

Adobe Experience Platform [!DNL Identity Service]은(는) 시스템 및 장치 간에 고객 ID 데이터를 연결해줍니다. [!DNL Identity Service] id  **namespacesttesto를** 사용하여 해당 ID를 원래 시스템에 연결하여 ID 값에 컨텍스트를 제공합니다. 네임스페이스는 이메일 주소(&quot;이메일&quot;)와 같은 일반적인 개념을 나타내거나 ID를 Adobe Advertising Cloud ID(&quot;AdCloud&quot;) 또는 Adobe Target ID(&quot;TNTID&quot;)와 같은 특정 응용 프로그램과 연결할 수 있습니다.

Identity Service는 전역적으로 정의된(표준) ID 네임스페이스와 사용자 정의(사용자 정의) ID 네임스페이스의 저장소를 유지 관리합니다. 표준 네임스페이스는 모든 조직(예: &quot;이메일&quot; 및 &quot;ECID&quot;)에서 사용할 수 있지만 조직에서 특정 요구에 맞는 사용자 정의 네임스페이스를 만들 수도 있습니다.

[!DNL Experience Platform]의 ID 네임스페이스에 대한 자세한 내용은 [ID 네임스페이스 개요](../identity-service/namespaces.md)를 참조하십시오.

## 요청 제출 중 {#submit}

아래 섹션에서는 [!DNL Privacy Service] API 또는 UI를 사용하여 [!DNL Real-time Customer Profile]에 대한 개인 정보 요청을 수행하는 방법에 대해 간략하게 설명합니다. 이 섹션을 읽기 전에 요청 페이로드에서 제출된 사용자 ID 데이터의 형식을 적절하게 지정하는 방법을 포함하여 개인 정보 작업을 제출하는 방법에 대한 전체 단계를 보려면 [Privacy Service API](../privacy-service/api/getting-started.md) 또는 [Privacy Service UI](../privacy-service/ui/overview.md) 설명서를 검토해야 합니다.

>[!IMPORTANT]
>
>Privacy Service은 ID 연결을 수행하지 않는 병합 정책을 사용하여 [!DNL Profile] 데이터만 처리할 수 있습니다. UI를 사용하여 개인 정보 요청의 처리 여부를 확인하는 경우 &quot;[!DNL None]&quot;이(가) 있는 정책을 [!UICONTROL ID stitching] 유형으로 사용하고 있는지 확인하십시오. 즉, [!UICONTROL ID stitching]이(가) &quot;[!UICONTROL Private graph]&quot;로 설정된 병합 정책을 사용할 수 없습니다.
>
>![](./images/privacy/no-id-stitch.png)
>
>개인정보 보호 요청을 완료하는 데 소요되는 시간은 보장되지 않습니다. 요청이 계속 처리되는 동안 [!DNL Profile] 데이터에 변경 사항이 발생하는 경우 해당 레코드가 처리되는지 여부도 보장할 수 없습니다.

### API 사용

API에서 작업 요청을 만들 때 `userIDs` 내에 제공된 모든 ID는 특정 `namespace` 및 `type`를 사용해야 합니다. `namespace` 값에 대해 [!DNL Identity Service]에서 인식하는 유효한 [id 네임스페이스](#namespaces)를 제공해야 하며, `type`는 각각 `standard` 또는 `unregistered`(표준 및 사용자 정의 네임스페이스의 경우)이어야 합니다.

>[!NOTE]
>
>ID 그래프와 프로필 단편이 플랫폼 데이터 세트에서 어떻게 배포되는지에 따라 각 고객에 대해 두 개 이상의 ID를 제공해야 할 수 있습니다. 자세한 내용은 다음 섹션 [프로필 조각](#fragments)을 참조하십시오.

또한 요청 페이로드의 `include` 배열에는 요청이 수행되는 다른 데이터 저장소에 대한 제품 값이 포함되어야 합니다. [!DNL Data Lake]에 대한 요청을 할 때 배열에 &quot;ProfileService&quot; 값이 포함되어야 합니다.

다음 요청은 [!DNL Profile] 스토어에 있는 단일 고객의 데이터에 대한 새 개인 정보 보호 작업을 만듭니다. `userIDs` 배열에서 고객에 대해 두 개의 ID 값이 제공됩니다.하나는 표준 `Email` id 네임스페이스를 사용하고 다른 하나는 사용자 지정 `Customer_ID` 네임스페이스를 사용합니다. 또한 `include` 배열에 [!DNL Profile](`ProfileService`)에 대한 제품 값이 포함되어 있습니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
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
    "include": ["ProfileService"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

### UI 사용

UI에서 작업 요청을 만들 때는 [!DNL Data Lake] 또는 [!DNL Real-time Customer Profile]에 저장된 데이터의 작업을 각각 처리하려면 **[!UICONTROL AEP Data Lake]** 및/또는 **[!UICONTROL Profile]** 아래에서 **[!UICONTROL Products]**&#x200B;을 선택해야 합니다.

<img src="images/privacy/product-value.png" width="450"><br>

## 개인 정보 요청의 프로필 조각 {#fragments}

[!DNL Profile] 데이터 저장소에서 개별 고객에 대한 개인 데이터는 종종 ID 그래프를 통해 사람과 연결되는 여러 프로필 조각으로 구성됩니다. [!DNL Profile] 스토어에 개인 정보를 요청할 때는 요청이 전체 프로필이 아니라 프로필 조각 수준에서만 처리된다는 점을 주목해야 합니다.

예를 들어 서로 다른 식별자를 사용하여 해당 데이터를 개별 고객과 연결하는 별도의 데이터 세트 3개에 고객 속성 데이터를 저장하는 상황을 가정해 보십시오.

| 데이터 세트 이름 | 기본 ID 필드 | 저장된 속성 |
| --- | --- | --- |
| 데이터 세트 1 | `customer_id` | `address` |
| 데이터 세트 2 | `email_id` | `firstName`, `lastName` |
| 데이터 세트 3 | `email_id` | `mlScore` |

데이터 세트 중 하나는 `customer_id`을(를) 기본 식별자로 사용하는 반면 다른 두 데이터 집합은 `email_id`을 사용합니다. 사용자 ID 값으로 `email_id`만 사용하여 개인 정보 요청을 전송(액세스 또는 삭제)하려는 경우 `firstName`, `lastName` 및 `mlScore` 속성만 처리되고 `address`는 영향을 받지 않습니다.

개인 정보 요청이 모든 관련 고객 속성을 처리하도록 하려면 해당 속성이 저장될 수 있는 모든 해당 데이터 세트에 대한 기본 ID 값을 제공해야 합니다(고객당 최대 9개의 ID). ID로 일반적으로 표시된 필드에 대한 자세한 내용은 스키마 컴포지션](../xdm/schema/composition.md#identity)의 [기본 사항의 ID 필드에 대한 섹션을 참조하십시오.

>[!NOTE]
>
>다른 [샌드박스](../sandboxes/home.md)를 사용하여 [!DNL Profile] 데이터를 저장하는 경우 `x-sandbox-name` 헤더에서 적절한 샌드박스 이름을 나타내는 각 샌드박스에 대해 별도의 개인 정보 요청을 해야 합니다.

## 요청 처리 삭제

[!DNL Experience Platform]이(가) [!DNL Privacy Service]의 삭제 요청을 받으면 [!DNL Platform]은(는) 요청을 받았고 영향을 받는 데이터가 삭제하도록 표시되었다는 확인을 [!DNL Privacy Service]에 보냅니다. 그러면 개인 정보 작업이 완료되면 [!DNL Data Lake] 또는 [!DNL Profile] 스토어에서 레코드가 제거됩니다. 삭제 작업이 계속 처리되는 동안 데이터는 소프트 삭제되므로 [!DNL Platform] 서비스에서 액세스할 수 없습니다. 작업 상태 추적에 대한 자세한 내용은 [[!DNL Privacy Service] 설명서](../privacy-service/home.md#monitor)를 참조하십시오.

>[!IMPORTANT]
>
>삭제 요청이 성공하면 고객(또는 고객 집합)에 대해 수집된 속성 데이터가 제거되지만 ID 그래프에 설정된 연결은 요청이 제거되지 않습니다.
>
>예를 들어 고객의 `email_id` 및 `customer_id`을 사용하는 삭제 요청은 해당 ID 아래에 저장된 모든 특성 데이터를 제거합니다. 하지만, 같은 `customer_id`에서 인제스트된 데이터는 여전히 연관성이 있으므로 해당 `email_id`과(와) 계속 연결됩니다.

데이터가 물리적으로 삭제된 후 [!DNL Platform]이(가) [!DNL Privacy Service]에 확인을 보냅니다.

## 다음 단계

이 문서를 읽음으로써 [!DNL Experience Platform]의 개인 정보 요청 처리와 관련된 중요한 개념을 도입했습니다. ID 데이터 관리 및 개인 정보 보호 작업 생성 방법에 대한 이해를 심도있게 하기 위해 이 안내서 전체에서 제공된 설명서를 계속 읽는 것이 좋습니다.

[!DNL Profile]에서 사용하지 않는 [!DNL Platform] 리소스에 대한 개인정보 보호 요청을 처리하는 방법에 대한 자세한 내용은 데이터 레이크](../catalog/privacy.md)의 [개인 정보 요청 처리에 대한 문서를 참조하십시오.
