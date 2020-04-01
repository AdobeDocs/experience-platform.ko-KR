---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 실시간 고객 프로필의 개인 정보 요청 처리
topic: overview
translation-type: tm+mt
source-git-commit: 5f0e0deb4a2fae636ac4d2313a6541c25309c294

---


# 실시간 고객 프로필의 개인 정보 요청 처리

Adobe Experience Platform Privacy Service는 GDPR(General Data Protection Regulation) 및 CCPA(California Consumer Privacy Act)와 같은 개인 정보 보호 규정에 따라 고객의 개인 정보에 대한 액세스, 거부 또는 삭제를 처리합니다.

이 문서에서는 실시간 고객 프로파일에 대한 개인정보 보호 요청 처리와 관련된 필수 개념을 다룹니다.

## 시작하기

이 안내서를 읽기 전에 다음 Experience Platform 서비스에 대한 충분한 지식이 있는 것이 좋습니다.

* [개인 정보 서비스](home.md):Adobe Experience Cloud 애플리케이션에서 개인 데이터를 액세스, 판매 거부 또는 삭제하기 위한 고객 요청을 관리합니다.
* [ID 서비스](../identity-service/home.md):다양한 디바이스와 시스템에 ID를 연결하여 고객 경험 데이터의 세분화로 인한 기본적인 문제를 해결합니다.
* [실시간 고객 프로필](../profile/home.md):다양한 소스의 데이터를 집계하여 통합된 실시간 고객 프로파일을 제공합니다.

## ID 네임스페이스 이해 {#namespaces}

Adobe Experience Platform Identity Service는 시스템 및 디바이스에서 고객 ID 데이터를 전달합니다. Identity Service는 **ID 네임스페이스를** 사용하여 ID 값을 원본 시스템에 연결하여 ID 값에 컨텍스트를 제공합니다. 네임스페이스는 이메일 주소(&quot;이메일&quot;)와 같은 일반적인 개념을 나타내거나 Adobe Advertising Cloud ID(&quot;AdCloud&quot;) 또는 Adobe Target ID(&quot;TNTID&quot;)와 같은 특정 애플리케이션과 ID를 연결할 수 있습니다.

ID 서비스는 전역적으로 정의된(표준) 및 사용자 정의(사용자 정의) ID 네임스페이스의 저장소를 유지 관리합니다. 표준 네임스페이스는 모든 조직(예: &quot;이메일&quot; 및 &quot;ECID&quot;)에서 사용할 수 있으며, 조직에서 특정 요구 사항에 맞게 사용자 정의 네임스페이스를 만들 수도 있습니다.

경험 플랫폼의 ID 네임스페이스에 대한 자세한 내용은 [ID 네임스페이스 개요를](../identity-service/namespaces.md)참조하십시오.

## 요청 제출 {#submit}

>[!NOTE] 이 섹션에서는 Data Lake에 대한 개인 정보 요청의 형식을 지정하는 방법에 대해 설명합니다. Adobe에서는 Privacy Service API [또는 Privacy Service](../privacy-service/api/getting-started.md) UI [문서를 검토하여 요청 페이로드에서 제출된 사용자 ID 데이터의 형식을 적절하게 지정하는 방법을 포함하여 개인 정보](../privacy-service/ui/overview.md) 보호 작업을 제출하는 방법에 대한 전체 단계를 수행하는 것이 좋습니다.

다음 섹션에서는 개인 정보 서비스 API 또는 UI를 사용하여 실시간 고객 프로필 및 Data Lake에 대한 개인 정보 요청을 수행하는 방법에 대해 설명합니다.

### API 사용

API에서 작업 요청을 만들 `userIDs` 때 제공된 모든 작업은 해당 작업이 적용되는 데이터 저장소에 `namespace` 따라 특정 `type` 및 를 사용해야 합니다. 프로필 스토어의 ID는 해당 `type` 값에 &quot;standard&quot; 또는 &quot;custom&quot;을 사용해야 하며, [값에 대해 Identity Service가 인식하는 유효한](#namespaces) ID 네임스페이스를 `namespace` 사용해야 합니다.


또한 요청 페이로드 `include` 배열에는 요청이 수행되는 여러 데이터 저장소에 대한 제품 값이 포함되어야 합니다. Data Lake에 대한 요청을 할 때 배열에 &quot;ProfileService&quot; 값이 포함되어야 합니다.

다음 요청은 표준 &quot;이메일&quot; ID 네임스페이스를 사용하여 실시간 고객 프로필에 대한 새 개인 정보 보호 작업을 만듭니다. 또한 `include` 배열에 있는 프로필의 제품 값도 포함합니다.

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

UI에서 작업 요청을 만들 때는 **DataLake** 및/또는 **Profiles에서** AEP Data _Lake 및/또는 Profile을 선택하여_ Data Lake 또는 실시간 고객 프로파일에 저장된 데이터에 대한 작업을 각각 처리해야 합니다.

<img src="images/privacy/product-value.png" width="450"><br>

## 요청 처리 삭제

Experience Platform이 개인 정보 보호 서비스에서 삭제 요청을 받으면, 플랫폼은 요청을 수신했으며 영향을 받는 데이터는 삭제하도록 표시되었음을 개인 정보 보호 서비스에 확인을 보냅니다. 그런 다음 7일 이내에 Data Lake 또는 프로필 저장소에서 레코드가 제거됩니다. 이 7일 기간 동안 데이터는 소프트 삭제되므로 플랫폼 서비스에서 액세스할 수 없습니다.

향후 릴리스에서는 데이터가 물리적으로 삭제된 후 Platform은 개인 정보 보호 서비스에 확인을 보냅니다.

## 다음 단계

이 문서를 읽음으로써 Experience Platform에서 개인 정보 요청 처리와 관련된 중요한 개념을 도입했습니다. ID 데이터 관리 및 개인 정보 보호 작업 생성 방법에 대한 이해를 높이려면 이 안내서 전체에서 제공된 설명서를 계속 읽는 것이 좋습니다.

프로필에 사용되지 않는 플랫폼 리소스에 대한 개인 정보 보호 요청을 처리하는 방법에 대한 자세한 내용은 Data Lake의 [개인 정보 보호 요청 처리에 대한 문서를 참조하십시오](../catalog/privacy.md).