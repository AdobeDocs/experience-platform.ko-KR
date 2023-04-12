---
keywords: Experience Platform;홈;인기 있는 주제
title: Identity 서비스에서 개인 정보 보호 요청 처리
description: Adobe Experience Platform Privacy Service은 다양한 개인 정보 보호 규정에 따라 지정된 대로 고객 개인 데이터에 대한 액세스, 판매 거부 또는 삭제 요청을 처리합니다. 이 문서에서는 Identity 서비스의 개인 정보 보호 요청 처리와 관련된 필수 개념을 다룹니다.
exl-id: ab84450b-1a4b-4fdd-b77d-508c86bbb073
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1037'
ht-degree: 0%

---

# 의 개인 정보 보호 요청 처리 [!DNL Identity Service]

Adobe Experience Platform [!DNL Privacy Service] 는 GDPR(General Data Protection Regulation) 및 와 같은 개인 정보 보호 규정에 따라 지정된 대로 고객 개인 데이터에 대한 액세스, 판매 거부 또는 삭제 요청을 처리합니다 [!DNL California Consumer Privacy Act] (CCPA).

이 문서에서는 [!DNL Identity Service] Adobe Experience Platform 내에서 사용할 수 있습니다.

>[!NOTE]
>
>이 안내서에서는 Experience Platform의 ID 데이터 저장소에 대해 개인 정보 보호 요청을 하는 방법만 다룹니다. 플랫폼 데이터 레이크에 대해 개인 정보 보호 요청을 하려는 경우 또는 [!DNL Real-Time Customer Profile]에서 참조할 수 있는 [data lake의 개인 정보 보호 요청 처리](../catalog/privacy.md) 및 [프로필에 대한 개인 정보 보호 요청 처리](../profile/privacy.md) 추가 정보.
>
>다른 Adobe Experience Cloud 애플리케이션에 대해 개인 정보 보호 요청을 수행하는 방법에 대한 단계는 [Privacy Service 설명서](../privacy-service/experience-cloud-apps.md).

## 시작하기

다음 사항에 대한 작업 이해를 하는 것이 좋습니다 [!DNL Experience Platform] 이 안내서를 읽기 전 서비스

* [[!DNL Privacy Service]](../privacy-service/home.md): Adobe Experience Cloud 애플리케이션에서 개인 데이터를 액세스, 판매 거부 또는 삭제하기 위한 고객 요청을 관리합니다.
* [[!DNL Identity Service]](../identity-service/home.md): 여러 장치 및 시스템에서 ID를 브리징하여 고객 경험 데이터의 분화로 인한 근본적인 문제를 해결합니다.
* [[!DNL Real-Time Customer Profile]](home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

## ID 네임스페이스 이해 {#namespaces}

Adobe Experience Platform [!DNL Identity Service] 는 시스템 및 장치에서 고객 ID 데이터를 전달합니다. [!DNL Identity Service] 사용 **id 네임스페이스** ID 값에 컨텍스트를 제공하는 데 사용할 수 있습니다. 네임스페이스는 이메일 주소(&quot;이메일&quot;)와 같은 일반적인 개념을 나타내거나 ID를 Adobe Advertising Cloud ID(&quot;AdCloud&quot;) 또는 Adobe Target ID(&quot;TNTID&quot;)와 같은 특정 애플리케이션과 연결할 수 있습니다.

ID 서비스는 전역적으로 정의된(표준) 및 사용자 정의(사용자 정의) ID 네임스페이스의 저장소를 유지 관리합니다. 표준 네임스페이스는 모든 조직(예: &quot;이메일&quot; 및 &quot;ECID&quot;)에서 사용할 수 있지만 조직은 특정 요구 사항에 맞게 사용자 지정 네임스페이스를 만들 수도 있습니다.

의 ID 네임스페이스에 대한 자세한 내용은 [!DNL Experience Platform]를 참조하고 [id 네임스페이스 개요](../identity-service/namespaces.md).

## 요청 제출 {#submit}

아래 섹션에서는 개인 정보 보호 요청을 수행하는 방법에 대해 간략하게 설명합니다 [!DNL Identity Service] 사용 [!DNL Privacy Service] API 또는 UI. 이러한 섹션을 읽기 전에 [Privacy Service API](../privacy-service/api/getting-started.md) 또는 [Privacy Service UI](../privacy-service/ui/overview.md) 문서 를 참조하십시오.

### API 사용

API에서 작업 요청을 만들 때 내에 제공된 모든 ID입니다 `userIDs` 특정 `namespace` 및 `type`. 유효한 [id 네임스페이스](#namespaces) 인식자 [!DNL Identity Service] 는 `namespace` 값, `type` 다음 중 하나여야 합니다. `standard` 또는 `unregistered` (표준 및 사용자 지정 네임스페이스의 경우 각각).

또한 `include` 요청 페이로드 배열에는 요청이 수행되고 있는 다양한 데이터 저장소의 제품 값이 포함되어야 합니다. 에 요청할 때 [!DNL Identity]이면 배열에 값이 포함되어야 합니다 `Identity`.

다음 요청은 의 단일 고객 데이터에 대한 GDPR 아래에 새 개인 정보 작업을 만듭니다 [!DNL Identity] 저장. 에서는 고객에 대해 두 개의 ID 값이 제공됩니다 `userIDs` 배열; 표준 `Email` id 네임스페이스 및 `ECID` 네임스페이스에 대한 제품 값도 포함됩니다 [!DNL Identity] (`Identity`)을 클릭하여 제품에서 사용할 수 있습니다. `include` 배열:

>[!TIP]
>
>API를 사용하여 사용자 지정 네임스페이스를 삭제할 때는 표시 이름 대신 ID 기호를 네임스페이스로 지정해야 합니다.

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer <key>' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: acp_privacy_ui_gdpr' \
  -H 'x-gw-ims-org-id: sample@AdobeOrg' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "sample@AdobeOrg"
      }
    ],
    "users": [
      {
        "key": "bob",
        "action": ["delete"],
        "userIDs": [
          {
            "namespace": "email",
            "value": "bob@adobe.com",
            "type": "standard"
          },
          {
            "namespace": "ECID",
            "type": "standard",
            "value":  "123451234512345123451234512345",
            "isDeletedClientSide": false
          }
        ]
      }
    ],
    "include": ["Identity"],
    "regulation": "gdpr"
}'
```

### UI 사용

>[!TIP]
>
>UI를 사용하여 사용자 지정 네임스페이스를 삭제할 때는 표시 이름 대신 ID 기호를 네임스페이스로 지정해야 합니다. 또한 비프로덕션 샌드박스의 UI에서 사용자 지정 네임스페이스를 삭제할 수 없습니다.

UI에서 작업 요청을 만들 때는 반드시 선택해야 합니다 **[!UICONTROL ID]** 아래에 **[!UICONTROL 제품]** 에 저장된 데이터의 작업을 처리하려면 [!DNL Identity Service].

![id-gdpr](./images/identity-gdpr.png)

## 요청 처리 삭제

When [!DNL Experience Platform] 에서 삭제 요청을 받습니다. [!DNL Privacy Service], [!DNL Platform] 에 확인 보내기 [!DNL Privacy Service] 요청이 수신되고 영향을 받는 데이터가 삭제로 표시되었음을 나타냅니다. 개별 ID의 삭제는 제공된 네임스페이스 및/또는 ID 값을 기반으로 합니다. 또한 해당 조직과 연관된 모든 샌드박스에 대해서도 삭제를 수행합니다.

실시간 고객 프로필(`ProfileService`) 및 data lake(`aepDataLake`)을 ID 서비스에 대한 개인 정보 보호 요청의 제품으로 사용(`identity`). ID와 관련된 다른 데이터 세트는 잠재적으로 다른 시간에 시스템에서 제거됩니다.

| 포함된 제품 | 효과 |
| --- | --- |
| `identity` 전용 | 제공된 ID와 연결된 ID 그래프는 Platform이 삭제 요청을 수신했다는 확인을 전송하는 즉시 삭제됩니다. 해당 ID 그래프에서 생성된 프로필은 여전히 남아 있지만 ID 연결이 제거되므로 새 데이터를 수집할 때 업데이트되지 않습니다. 프로필과 연결된 데이터도 데이터 레이크에 유지됩니다. |
| `identity` 및 `ProfileService` | Platform이 삭제 요청을 수신했다는 확인을 전송하는 즉시 ID 그래프 및 관련 프로필이 삭제됩니다. 프로필과 연관된 데이터는 데이터 레이크에 유지됩니다. |
| `identity` 및 `aepDataLake` | 제공된 ID와 연결된 ID 그래프는 Platform이 삭제 요청을 수신했다는 확인을 전송하는 즉시 삭제됩니다. 해당 ID 그래프에서 생성된 프로필은 여전히 남아 있지만 ID 연결이 제거되므로 새 데이터를 수집할 때 업데이트되지 않습니다.<br><br>Data Lake 제품이 요청을 받고 현재 처리 중임을 응답하면 프로필과 연결된 데이터가 소프트 삭제되므로 다른 제품도 액세스할 수 없습니다 [!DNL Platform] 서비스. 작업이 완료되면 데이터가 데이터 레이크에서 완전히 제거됩니다. |
| `identity`, `ProfileService`, 및 `aepDataLake` | Platform이 삭제 요청을 수신했다는 확인을 전송하는 즉시 ID 그래프 및 관련 프로필이 삭제됩니다.<br><br>Data Lake 제품이 요청을 받고 현재 처리 중임을 응답하면 프로필과 연결된 데이터가 소프트 삭제되므로 다른 제품도 액세스할 수 없습니다 [!DNL Platform] 서비스. 작업이 완료되면 데이터가 데이터 레이크에서 완전히 제거됩니다. |

자세한 내용은 [[!DNL Privacy Service] 설명서](../privacy-service/home.md#monitor) 작업 상태 추적에 대한 자세한 내용을 참조하십시오.

## 다음 단계

이 문서를 읽은 후에는 의 개인 정보 보호 요청 처리와 관련된 중요한 개념을 도입했습니다 [!DNL Identity Service]. 기타 사용자에 대한 개인 정보 보호 요청 처리에 대한 정보 [!DNL Experience Cloud] 응용 프로그램, 문서 보기 [[!DNL Privacy Service] and [!DNL Experience Cloud] 애플리케이션](../privacy-service/experience-cloud-apps.md).
