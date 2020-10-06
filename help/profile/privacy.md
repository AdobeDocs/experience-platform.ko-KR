---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 실시간 고객 프로필의 개인 정보 요청 처리
topic: overview
translation-type: tm+mt
source-git-commit: f7abccb677294e1595fb35c27e03c30eb968082a
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 0%

---


# 개인 정보 요청 처리 [!DNL Real-time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] 는 GDPR(General Data Protection Regulation) 및 [!DNL California Consumer Privacy Act] (CPPA)와 같은 개인 정보 보호 규정에 따라 고객의 개인 정보에 액세스하거나, 판매를 거부하거나, 삭제하도록 요청을 처리합니다.

이 문서에서는 개인정보 보호 요청 처리와 관련된 필수 개념을 다룹니다 [!DNL Real-time Customer Profile].

## 시작하기

이 안내서를 읽기 전에 다음 [!DNL Experience Platform] 서비스에 대해 잘 알고 있는 것이 좋습니다.

* [[!DNL Privacy Service]](home.md):Adobe Experience Cloud 애플리케이션에서 개인 데이터를 액세스, 판매 거부 또는 삭제하기 위한 고객 요청을 관리합니다.
* [[!DNL Identity Service]](../identity-service/home.md):다양한 디바이스와 시스템에 ID를 연결하여 고객 경험 데이터의 세분화로 인한 기본적인 문제를 해결합니다.
* [[!DNL 실시간 고객 프로필]](../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

## ID 네임스페이스 이해 {#namespaces}

Adobe Experience Platform [!DNL Identity Service] 는 시스템과 디바이스에서 고객 ID 데이터를 연결해줍니다. [!DNL Identity Service] id 네임스페이스를 **** 사용하여 ID 값을 원본 시스템과 연결함으로써 ID 값에 컨텍스트를 제공합니다. 네임스페이스는 이메일 주소(&quot;이메일&quot;)와 같은 일반 개념을 나타내거나 ID를 Adobe Advertising Cloud ID(&quot;AdCloud&quot;) 또는 Adobe Target ID(&quot;TNTID&quot;)와 같은 특정 응용 프로그램과 연결할 수 있습니다.

ID 서비스는 전역적으로 정의된(표준) 및 사용자 정의(사용자 정의) ID 네임스페이스의 저장소를 유지 관리합니다. 표준 네임스페이스는 모든 조직(예: &quot;이메일&quot; 및 &quot;ECID&quot;)에서 사용할 수 있지만 조직에서 특정 요구에 맞는 사용자 정의 네임스페이스를 만들 수도 있습니다.

의 ID 네임스페이스에 대한 자세한 내용 [!DNL Experience Platform]은 [ID 네임스페이스 개요를 참조하십시오](../identity-service/namespaces.md).

## 요청 제출 {#submit}

아래 섹션에서는 API 또는 UI를 사용하기 위해 개인 정보 [!DNL Real-time Customer Profile] 를 요청하는 방법을 간략하게 [!DNL Privacy Service] 설명합니다. 이러한 섹션을 읽기 전에, 요청 페이로드에서 제출된 사용자 ID 데이터의 형식을 적절하게 지정하는 방법을 포함하여 개인 정보 보호 작업을 제출하는 방법에 대한 전체 단계를 위해 [Privacy Service API](../privacy-service/api/getting-started.md) 또는 [Privacy Service UI](../privacy-service/ui/overview.md) 설명서를 검토할 것을 권장합니다.

>[!IMPORTANT]
>
>Privacy Service은 ID 연결을 수행하지 않는 병합 정책을 사용하여 [!DNL Profile] 데이터만 처리할 수 있습니다. UI를 사용하여 개인 정보 요청 처리 여부를 확인하는 경우, &quot;[!DNL None]&quot;가 있는 정책을 [!UICONTROL ID 연결] 유형으로 사용하고 있는지 확인하십시오. 즉, ID 스티칭이 &quot; [!UICONTROL 비공개 그래프] &quot;로 설정된 병합 정책은 사용할 수[!UICONTROL 없습니다].
>
>![](./images/privacy/no-id-stitch.png)

### API 사용

API에서 작업 요청을 만들 때 ID에 제공된 모든 ID는 특정 및 `userIDs` 을 사용해야 `namespace` 합니다 `type`. 값 [에 대해](#namespaces) 인식되는 유효한 [!DNL Identity Service] ID 네임스페이스 `namespace``type` 를 제공해야 `standard` 하지만 `unregistered` ID는 표준 및 사용자 정의 네임스페이스에 각각또는여야 합니다.

>[!NOTE]
>
>ID 그래프와 프로필 단편이 플랫폼 데이터 세트에서 배포되는 방식에 따라 각 고객에 대해 두 개 이상의 ID를 제공해야 할 수 있습니다. 자세한 내용은 다음 섹션 [프로필 조각을](#fragments) 참조하십시오.

또한 요청 페이로드 `include` 배열에 요청이 수행되는 다른 데이터 저장소에 대한 제품 값이 포함되어야 합니다. 에 대한 요청을 할 때 배열 [!DNL Data Lake]에 &quot;ProfileService&quot; 값이 포함되어야 합니다.

다음 요청은 [!DNL Profile] 스토어에 있는 단일 고객의 데이터에 대한 새 개인 정보 보호 작업을 만듭니다. 스토리지 시스템의 고객에 대해 두 개의 ID 값이 `userIDs` 제공됩니다.표준 `Email` ID 네임스페이스를 사용하는 경우와 사용자 지정 `Customer_ID` 네임스페이스를 사용하는 경우에 사용됩니다. 또한 배열에 [!DNL Profile] (`ProfileService`)의 제품 값도 `include` 포함합니다.

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

UI에서 작업 요청을 만들 때는 **[!UICONTROL 제품]** 아래의 **[!UICONTROL AEP 데이터 레이크]** 및/또는 **[!UICONTROL 프로필]**[!DNL Data Lake] 을 선택하여 [!DNL Real-time Customer Profile]데이터에 저장된 작업을각각 처리하거나 지연에 있는 AEP 데이터및 프로필을선택하십시오.

<img src="images/privacy/product-value.png" width="450"><br>

## 개인 정보 요청의 프로필 조각 {#fragments}

데이터 [!DNL Profile] 저장소에서 개별 고객의 개인 데이터는 여러 프로필 조각으로 구성되며, 이것은 ID 그래프를 통해 사람과 연결됩니다. 저장소에 개인 정보 요청을 할 때 [!DNL Profile] 요청은 전체 프로필이 아니라 프로필 조각 수준에서만 처리됩니다.

예를 들어, 고객 속성 데이터를 서로 다른 식별자를 사용하여 개별 고객과 데이터를 연결하는 세 개의 개별 데이터 세트에 저장하는 경우를 생각해 보십시오.

| 데이터 세트 이름 | 기본 ID 필드 | 저장된 속성 |
| --- | --- | --- |
| 데이터 세트 1 | `customer_id` | `address` |
| 데이터 세트 2 | `email_id` | `firstName`, `lastName` |
| 데이터 세트 3 | `email_id` | `mlScore` |

데이터 집합 중 하나는 기본 식별자로 사용하는 반면 다른 두 데이터 집합은 사용합니다 `customer_id` `email_id`. 사용자 ID 값만 사용하여 개인 정보 요청(액세스 또는 삭제) `email_id` 을 전송하려는 경우 `firstName`, `lastName`및 `mlScore` 속성만 처리되지만 영향을 받지 `address` 않습니다.

개인 정보 요청이 모든 관련 고객 속성을 처리하도록 하려면 해당 속성이 저장될 수 있는 모든 해당 데이터 세트에 대한 기본 ID 값을 제공해야 합니다(고객당 최대 9개의 ID). ID로 일반적으로 표시된 필드에 대한 자세한 내용은 스키마 작성 [](../xdm/schema/composition.md#identity) 기본 사항의 ID 필드에 대한 섹션을 참조하십시오.

>[!NOTE]
>
>다른 [샌드박스를](../sandboxes/home.md) 사용하여 [!DNL Profile] 데이터를 저장하는 경우 각 샌드박스에 대해 별도의 개인 정보 보호 요청을 해야 하며, 이는 `x-sandbox-name` 헤더에 해당 샌드박스 이름을 나타내야 합니다.

## 요청 처리 삭제

에서 [!DNL Experience Platform] 삭제 요청을 [!DNL Privacy Service]받으면 [!DNL Platform] 요청이 수신되고 영향을 받는 데이터가 삭제하도록 [!DNL Privacy Service] 표시되었다는 확인을 보냅니다. 그러면 개인 정보 보호 작업이 완료되면 [!DNL Data Lake] 또는 [!DNL Profile] 저장소에서 레코드가 제거됩니다. 삭제 작업이 계속 처리되는 동안 데이터는 소프트 삭제되므로 어떤 [!DNL Platform] 서비스에서도 액세스할 수 없습니다. 작업 상태 추적에 대한 자세한 내용은 [[!DNL Privacy Service] 설명서를](../privacy-service/home.md#monitor) 참조하십시오.

>[!IMPORTANT]
>
>삭제 요청이 성공하면 고객(또는 고객 집합)에 대해 수집된 속성 데이터가 제거되지만 ID 그래프에 설정된 연결은 요청이 제거되지 않습니다.
>
>예를 들어 고객의 이름을 사용하고 해당 ID `email_id` 에 저장된 모든 속성 데이터를 `customer_id` 제거하는 삭제 요청입니다. 하지만, 같은 방식으로 수집되는 데이터는 연계가 여전히 존재하므로 해당 데이터 `customer_id` `email_id`와 계속 연관됩니다.

향후 릴리스에서는 데이터가 물리적으로 삭제된 후 확인 [!DNL Platform] [!DNL Privacy Service] 을 보냅니다.

## 다음 단계

이 문서를 읽음으로써, 귀하는 [!DNL Experience Platform] ID 데이터를 관리하고 개인 정보 보호 작업을 만드는 방법에 대한 이해를 돕기 위해 이 안내서 전체에서 제공된 설명서를 계속 읽는 것이 좋습니다.

사용되지 않는 리소스에 대한 개인 정보 요청 처리 [!DNL Platform] 에 대한 자세한 내용은 [!DNL Profile]데이터 레이크에서 개인 정보 [보호 요청 처리에 관한 문서를 참조하십시오](../catalog/privacy.md).