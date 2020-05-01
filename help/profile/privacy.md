---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 실시간 고객 프로필의 개인 정보 요청 처리
topic: overview
translation-type: tm+mt
source-git-commit: cc296670db91640e75fd7a47b874a46eaf57ecde

---


# 실시간 고객 프로필의 개인 정보 요청 처리

Adobe Experience Platform 개인 정보 보호 서비스는 GDPR(General Data Protection Regulation) 및 CCPA(California Consumer Privacy Act)와 같은 개인 정보 보호 규정에 따라 고객의 개인 정보에 액세스하거나, 판매를 거부하거나, 삭제하도록 요청합니다.

이 문서에서는 실시간 고객 프로파일에 대한 개인정보 보호 요청 처리와 관련된 중요한 개념을 다룹니다.

## 시작하기

이 안내서를 읽기 전에 다음 경험 플랫폼 서비스에 대한 충분한 지식이 있는 것이 좋습니다.

* [개인정보 보호 서비스](home.md): Adobe Experience Cloud 애플리케이션에서 개인 데이터를 액세스, 판매 거부 또는 삭제하기 위한 고객 요청을 관리합니다.
* [ID 서비스](../identity-service/home.md): 다양한 디바이스와 시스템에 ID를 연결하여 고객 경험 데이터의 세분화로 인한 기본적인 문제를 해결합니다.
* [실시간 고객 프로필](../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

## ID 네임스페이스 이해 {#namespaces}

Adobe Experience Platform Identity Service는 시스템 및 디바이스에서 고객 ID 데이터를 연결해 줍니다. Identity Service는 **ID 네임스페이스를** 사용하여 ID 값에 대한 컨텍스트를 ID 시스템에 연결함으로써 제공합니다. 네임스페이스는 이메일 주소(&quot;이메일&quot;)와 같은 일반 개념을 나타내거나 Adobe Advertising Cloud ID(&quot;AdCloud&quot;) 또는 Adobe Target ID(&quot;TNTID&quot;)와 같은 특정 애플리케이션과 ID를 연결할 수 있습니다.

ID 서비스는 전역적으로 정의된(표준) 및 사용자 정의(사용자 정의) ID 네임스페이스의 저장소를 유지 관리합니다. 표준 네임스페이스는 모든 조직(예: &quot;이메일&quot; 및 &quot;ECID&quot;)에서 사용할 수 있지만 조직에서 특정 요구에 맞는 사용자 정의 네임스페이스를 만들 수도 있습니다.

경험 플랫폼의 ID 네임스페이스에 대한 자세한 내용은 [ID 네임스페이스 개요를 참조하십시오](../identity-service/namespaces.md).

## 요청 제출 {#submit}

>[!NOTE] 이 섹션에서는 프로필 데이터 저장소에 대한 개인 정보 요청을 만드는 방법에 대해 설명합니다. 요청 페이로드에서 제출된 사용자 ID 데이터의 형식을 적절하게 지정하는 방법을 비롯하여 개인 정보 보호 [서비스 API](../privacy-service/api/getting-started.md) 또는 [개인 정보 서비스 UI](../privacy-service/ui/overview.md) 설명서를 검토할 것을 권장합니다.

다음 섹션에서는 개인정보 보호 서비스 API 또는 UI를 사용하여 실시간 고객 프로필 및 Data Lake에 대한 개인정보 보호 요청을 수행하는 방법에 대해 설명합니다.

### API 사용

API에서 작업 요청 `userIDs` 을 만들 때 제공된 모든 작업 `namespace` 은 적용되는 데이터 저장소에 `type` 따라 특정 항목을 사용해야 합니다. 프로필 스토어의 ID는 해당 값에 &quot;standard&quot; 또는 &quot;custom&quot; 중 하나를 사용하고 해당 `type` 값에 대해 ID 서비스에서 인식하는 유효한 [ID 네임스페이스를](#namespaces) `namespace` 사용해야 합니다.


또한 요청 페이로드 `include` 배열에 요청이 수행되는 다른 데이터 저장소에 대한 제품 값이 포함되어야 합니다. Data Lake에 요청을 할 때 배열에 &quot;ProfileService&quot; 값이 포함되어야 합니다.

다음 요청은 표준 &quot;이메일&quot; ID 네임스페이스를 사용하여 실시간 고객 프로필 모두에 대한 새 개인 정보 작업을 만듭니다. 배열에 있는 프로필에 대한 제품 값도 `include` 포함합니다.

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

UI에서 작업 요청을 만들 때는 **제품** 에서 **AEP 데이터 레이크** 및/또는 _프로필_ 을 선택하여 데이터 레이크 또는 실시간 고객 프로필에 저장된 데이터의 작업을 각각 처리해야 합니다.

<img src="images/privacy/product-value.png" width="450"><br>

## 요청 처리 삭제

Experience Platform(경험 플랫폼)이 개인정보 보호 서비스로부터 삭제 요청을 받으면, 개인정보 보호 서비스에 요청이 접수되었고 영향을 받는 데이터가 삭제하도록 표시되었음을 알리는 확인 메시지를 보냅니다. 그러면 7일 이내에 Data Lake 또는 Profile 스토어에서 레코드가 제거됩니다. 이 7일 기간 동안 데이터는 소프트 삭제되므로 플랫폼 서비스에서 액세스할 수 없습니다.

향후 릴리스에서는 데이터가 물리적으로 삭제된 후 Platform(플랫폼)은 개인 정보 보호 서비스에 확인을 보냅니다.

## 다음 단계

이 문서를 읽음으로써 Experience Platform에서 개인 정보 요청 처리와 관련된 중요한 개념을 도입했습니다. ID 데이터를 관리하고 개인 정보 보호 작업을 만드는 방법에 대한 이해를 돕기 위해 이 안내서 전체에서 제공된 설명서를 계속 읽는 것이 좋습니다.

프로필에 사용되지 않는 플랫폼 리소스에 대한 개인 정보 보호 요청 처리에 대한 자세한 내용은 데이터 레이크에서 [개인 정보 보호 요청 처리에 관한 문서를 참조하십시오](../catalog/privacy.md).