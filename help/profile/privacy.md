---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 실시간 고객 프로필의 개인 정보 요청 처리
topic: overview
translation-type: tm+mt
source-git-commit: c8446f6040ac9ef1f4196d9057b531011e243258
workflow-type: tm+mt
source-wordcount: '603'
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

>[!NOTE]
>
>이 섹션에서는 데이터 저장소에 대한 개인 정보 요청을 만드는 방법을 [!DNL Profile] 설명합니다. 요청 페이로드에서 제출된 사용자 ID 데이터의 형식을 적절하게 지정하는 방법을 비롯하여 개인 정보 작업을 제출하는 방법에 대한 전체 단계를 보려면 [Privacy Service API](../privacy-service/api/getting-started.md) 또는 [Privacy Service UI](../privacy-service/ui/overview.md) 설명서를 검토해야 합니다.

다음 섹션에서는 API 또는 UI를 사용하여 개인 정보 [!DNL Real-time Customer Profile] 를 [!DNL Data Lake] 요청하는 방법에 대해 [!DNL Privacy Service] 설명합니다.

### API 사용

API에서 작업 요청 `userIDs` 을 만들 때 제공된 모든 작업 `namespace` 은 적용되는 데이터 저장소에 `type` 따라 특정 항목을 사용해야 합니다. 스토어의 [!DNL Profile] ID는 해당 `type` 값에 &quot;standard&quot; 또는 &quot;custom&quot; 중 하나를 사용하고 값 [에 대해 인식되는 유효한](#namespaces) ID 네임스페이스를 [!DNL Identity Service] 사용해야 `namespace` 합니다.


또한 요청 페이로드 `include` 배열에 요청이 수행되는 다른 데이터 저장소에 대한 제품 값이 포함되어야 합니다. 에 대한 요청을 할 때 배열 [!DNL Data Lake]에 &quot;ProfileService&quot; 값이 포함되어야 합니다.

다음 요청은 표준 &quot;이메일&quot; ID 네임스페이스를 [!DNL Real-time Customer Profile]사용하여 두 가지 모두에 대한 새 개인 정보 작업을 만듭니다. 스토리지 시스템 [!DNL Profile] 에 대한 제품 값도 `include` 포함합니다.

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
            "namespace": "Email",
            "value": "ajones@acme.com",
            "type": "standard"
          },
          {
            "namespace": "email_label",
            "value": "ajones@acme.com",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["ProfileService", "aepDataLake"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

### UI 사용

UI에서 작업 요청을 만들 때는 **[!UICONTROL 제품]** 아래의 **[!UICONTROL AEP 데이터 레이크]** 및/또는 _[!UICONTROL 프로필]_[!DNL Data Lake] 을 선택하여 [!DNL Real-time Customer Profile]데이터에 저장된 작업을각각 처리하거나 지연에 있는 AEP 데이터및 프로필을선택하십시오.

<img src="images/privacy/product-value.png" width="450"><br>

## 요청 처리 삭제

에서 [!DNL Experience Platform] 삭제 요청을 [!DNL Privacy Service]받으면 [!DNL Platform] 요청이 수신되고 영향을 받는 데이터가 삭제하도록 [!DNL Privacy Service] 표시되었다는 확인을 보냅니다. 그런 다음 7일 이내에 [!DNL Data Lake] 또는 [!DNL Profile] 스토어에서 레코드가 제거됩니다. 이 7일 기간 동안 데이터는 소프트 삭제되므로 어떤 [!DNL Platform] 서비스에서도 액세스할 수 없습니다.

향후 릴리스에서는 데이터가 물리적으로 삭제된 후 확인 [!DNL Platform] [!DNL Privacy Service] 을 보냅니다.

## 다음 단계

이 문서를 읽음으로써, 귀하는 [!DNL Experience Platform] ID 데이터를 관리하고 개인 정보 보호 작업을 만드는 방법에 대한 이해를 돕기 위해 이 안내서 전체에서 제공된 설명서를 계속 읽는 것이 좋습니다.

사용되지 않는 리소스에 대한 개인 정보 요청 처리 [!DNL Platform] 에 대한 자세한 내용은 [!DNL Profile]데이터 레이크에서 개인 정보 [보호 요청 처리에 관한 문서를 참조하십시오](../catalog/privacy.md).