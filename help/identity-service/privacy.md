---
keywords: Experience Platform;홈;인기 있는 주제
title: Identity 서비스에서 개인 정보 보호 요청 처리
description: Adobe Experience Platform Privacy Service은 수많은 개인 정보 보호 규정에 명시된 대로 개인 데이터에 액세스하거나, 판매를 거부하거나, 삭제하기 위한 고객 요청을 처리합니다. 이 문서에서는 Identity 서비스에 대한 개인 정보 보호 요청 처리와 관련된 필수 개념을 다룹니다.
exl-id: ab84450b-1a4b-4fdd-b77d-508c86bbb073
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1005'
ht-degree: 1%

---

# [!DNL Identity Service]에서 개인 정보 보호 요청 처리 중

Adobe Experience Platform [!DNL Privacy Service]은(는) GDPR(일반 데이터 보호 규정) 및 CCPA([!DNL California Consumer Privacy Act])와 같은 개인 정보 보호 규정에 따라 기술된 대로 개인 데이터에 액세스하거나, 판매를 거부하거나, 삭제하도록 고객 요청을 처리합니다.

이 문서에서는 Adobe Experience Platform 내에서 [!DNL Identity Service]에 대한 개인 정보 보호 요청 처리와 관련된 필수 개념을 다룹니다.

>[!NOTE]
>
>이 안내서에서는 Experience Platform의 ID 데이터 저장소에 대해 개인 정보를 요청하는 방법만 다룹니다. Experience Platform 데이터 레이크 또는 [!DNL Real-Time Customer Profile]에 대한 개인 정보 보호 요청도 수행할 계획이라면 이 자습서 외에 [데이터 레이크의 개인 정보 보호 요청 처리 가이드](../catalog/privacy.md) 및 [프로필에 대한 개인 정보 보호 요청 처리 가이드](../profile/privacy.md)를 참조하십시오.
>
>다른 Adobe Experience Cloud 애플리케이션에 대한 개인 정보 보호 요청을 하는 방법에 대한 단계는 [Privacy Service 설명서](../privacy-service/experience-cloud-apps.md)를 참조하십시오.

## 시작하기

이 안내서를 읽기 전에 다음 [!DNL Experience Platform] 서비스를 이해하는 것이 좋습니다.

* [[!DNL Privacy Service]](../privacy-service/home.md): Adobe Experience Cloud 애플리케이션에서 개인 데이터에 액세스하거나, 판매를 거부하거나, 삭제하기 위한 고객 요청을 관리합니다.
* [[!DNL Identity Service]](../identity-service/home.md): 장치 및 시스템 간에 ID를 연결하여 고객 경험 데이터의 단편화로 인해 발생하는 근본적인 문제를 해결합니다.
* [[!DNL Real-Time Customer Profile]](home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

## ID 네임스페이스 이해 {#namespaces}

Adobe Experience Platform [!DNL Identity Service]은(는) 시스템 및 장치 간에 고객 id 데이터를 브리지합니다. [!DNL Identity Service]은(는) **id 네임스페이스**&#x200B;를 사용하여 ID 값을 원본 시스템에 연결하여 컨텍스트를 제공합니다. 네임스페이스는 이메일 주소(&quot;이메일&quot;)와 같은 일반 개념을 나타내거나 Adobe Advertising Cloud ID(&quot;AdCloud&quot;) 또는 Adobe Target ID(&quot;TNTID&quot;)와 같은 특정 애플리케이션과 ID를 연결할 수 있습니다.

ID 서비스는 전역 정의(표준) 및 사용자 정의(사용자 정의) ID 네임스페이스 저장소를 유지 관리합니다. 표준 네임스페이스는 모든 조직에서 사용할 수 있으며(예: &quot;이메일&quot; 및 &quot;ECID&quot;), 조직에서는 특정 요구 사항에 맞게 사용자 정의 네임스페이스를 만들 수도 있습니다.

[!DNL Experience Platform]의 ID 네임스페이스에 대한 자세한 내용은 [ID 네임스페이스 개요](../identity-service/features/namespaces.md)를 참조하십시오.

## 요청 제출 {#submit}

아래 섹션에서는 [!DNL Privacy Service] API 또는 UI를 사용하여 [!DNL Identity Service]에 대한 개인 정보 보호 요청을 하는 방법에 대해 간략히 설명합니다. 이 섹션을 읽기 전에 [Privacy Service API](../privacy-service/api/getting-started.md) 또는 [Privacy Service UI](../privacy-service/ui/overview.md) 설명서를 검토하여 요청 페이로드에서 사용자 데이터를 올바르게 포맷하는 방법을 포함하여 개인 정보 보호 작업을 제출하는 방법에 대한 전체 단계를 확인하는 것이 좋습니다.

### API 사용

API에서 작업 요청을 만들 때 `userIDs` 내에 제공된 모든 ID는 특정 `namespace` 및 `type`을(를) 사용해야 합니다. [!DNL Identity Service]에서 인식하는 올바른 [ID 네임스페이스](#namespaces)을(를) `namespace` 값에 제공해야 하지만, `type`은(는) 각각 표준 및 사용자 지정 네임스페이스에 대해 `standard` 또는 `unregistered`이어야 합니다.

또한 요청 페이로드의 `include` 배열에는 요청을 수행하는 다른 데이터 저장소에 대한 제품 값이 포함되어야 합니다. [!DNL Identity]에 요청할 때 배열에 값 `Identity`이(가) 포함되어야 합니다.

다음 요청은 GDPR에 [!DNL Identity] 저장소의 단일 고객 데이터에 대한 새 개인 정보 보호 작업을 만듭니다. `userIDs` 배열에서 고객에 대해 두 개의 ID 값이 제공됩니다. 하나는 표준 `Email` ID 네임스페이스를 사용하고 다른 하나는 `ECID` 네임스페이스를 사용하며, 여기에는 `include` 배열의 [!DNL Identity]&#x200B;(`Identity`)에 대한 제품 값도 포함됩니다.

>[!TIP]
>
>GDPR 삭제를 사용하여 ID를 삭제할 때 표시 이름 대신 ID 기호를 네임스페이스로 지정해야 합니다.

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
>GDPR 삭제를 사용하여 ID를 삭제할 때 표시 이름 대신 ID 기호를 네임스페이스로 지정해야 합니다.

UI에서 작업 요청을 만들 때 [!DNL Identity Service]에 저장된 데이터에 대한 작업을 처리하려면 **[!UICONTROL 제품]**&#x200B;에서 **[!UICONTROL ID]**&#x200B;을(를) 선택하십시오.

![identity-gdpr](./images/identity-gdpr.png)

## 삭제 요청 처리

[!DNL Experience Platform]이(가) [!DNL Privacy Service]에서 삭제 요청을 받으면 [!DNL Experience Platform]이(가) 요청이 수신되었고 영향을 받는 데이터가 삭제되도록 표시되었다는 확인을 [!DNL Privacy Service]에 보냅니다. 개별 ID의 삭제는 제공된 네임스페이스 및/또는 ID 값을 기반으로 합니다. 또한 해당 조직과 연관된 모든 샌드박스에 대해 삭제가 수행됩니다.

ID 서비스(`identity`)에 대한 개인 정보 보호 요청에 제품으로 실시간 고객 프로필(`ProfileService`) 및 데이터 레이크(`aepDataLake`)를 포함했는지 여부에 따라 ID와 관련된 다른 데이터 집합이 잠재적으로 다른 시간에 시스템에서 제거됩니다.

| 포함된 제품 | 효과 |
| --- | --- |
| `identity`만 | Experience Platform에서 삭제 요청이 수신되었다는 확인을 전송하는 즉시 제공된 ID가 삭제됩니다. 해당 ID 그래프에서 생성된 프로필은 여전히 남아 있지만 이제 ID 연결이 제거되므로 새 데이터가 수집될 때 업데이트되지 않습니다. 프로필과 연결된 데이터도 데이터 레이크에 유지됩니다. |
| `identity` 및 `ProfileService` | Experience Platform에서 삭제 요청이 수신되었다는 확인을 전송하는 즉시 제공된 ID가 삭제됩니다. 프로필과 연결된 데이터는 데이터 레이크에 유지됩니다. |
| `identity` 및 `aepDataLake` | Experience Platform에서 삭제 요청이 수신되었다는 확인을 전송하는 즉시 제공된 ID가 삭제됩니다. 해당 ID 그래프에서 생성된 프로필은 여전히 남아 있지만 이제 ID 연결이 제거되므로 새 데이터가 수집될 때 업데이트되지 않습니다.<br><br>Data Lake 제품이 요청을 받았으며 현재 처리 중이라는 응답을 보내면 프로필과 연결된 데이터가 일시 삭제되므로 [!DNL Experience Platform] 서비스에서 액세스할 수 없습니다. 작업이 완료되면 데이터가 데이터 레이크에서 완전히 제거됩니다. |
| `identity`, `ProfileService` 및 `aepDataLake` | Experience Platform에서 삭제 요청이 수신되었다는 확인을 전송하는 즉시 제공된 ID가 삭제됩니다.<br><br>Data Lake 제품이 요청을 받았으며 현재 처리 중이라는 응답을 보내면 프로필과 연결된 데이터가 일시 삭제되므로 [!DNL Experience Platform] 서비스에서 액세스할 수 없습니다. 작업이 완료되면 데이터가 데이터 레이크에서 완전히 제거됩니다. |

작업 상태 추적에 대한 자세한 내용은 [[!DNL Privacy Service] 설명서](../privacy-service/home.md#monitor)를 참조하세요.

## 다음 단계

이 문서를 읽고 [!DNL Identity Service]의 개인 정보 보호 요청 처리와 관련된 중요한 개념을 이해하게 되었습니다. 다른 [!DNL Experience Cloud] 응용 프로그램에 대한 개인 정보 보호 요청 처리에 대한 자세한 내용은 [[!DNL Privacy Service] 및 [!DNL Experience Cloud] 응용 프로그램](../privacy-service/experience-cloud-apps.md)에 대한 문서를 참조하십시오.
