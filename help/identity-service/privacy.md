---
keywords: Experience Platform;홈;인기 있는 주제
title: Identity 서비스에서 개인 정보 보호 요청 처리
description: Adobe Experience Platform Privacy Service은 수많은 개인 정보 보호 규정에 명시된 대로 개인 데이터에 액세스하거나, 판매를 거부하거나, 삭제하기 위한 고객 요청을 처리합니다. 이 문서에서는 Identity 서비스에 대한 개인 정보 보호 요청 처리와 관련된 필수 개념을 다룹니다.
exl-id: ab84450b-1a4b-4fdd-b77d-508c86bbb073
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 1%

---

# 에서 개인 정보 보호 요청 처리 중 [!DNL Identity Service]

Adobe Experience Platform [!DNL Privacy Service] 는 GDPR(일반 데이터 보호 규정) 및 과 같은 개인 정보 보호 규정에 명시된 대로 개인 데이터에 액세스하거나, 판매를 거부하거나, 삭제하도록 고객 요청을 처리합니다. [!DNL California Consumer Privacy Act] (CCPA).

이 문서에서는 의 개인 정보 보호 요청 처리와 관련된 필수 개념을 다룹니다. [!DNL Identity Service] Adobe Experience Platform 내.

>[!NOTE]
>
>이 안내서에서는 Experience Platform의 ID 데이터 저장소에 대해 개인 정보 보호 요청을 하는 방법만 다룹니다. Platform 데이터 레이크에 대한 개인 정보 보호 요청을 하려는 경우 또는 [!DNL Real-Time Customer Profile], 의 안내서를 참조하십시오. [데이터 레이크에서 개인 정보 보호 요청 처리](../catalog/privacy.md) 및 의 안내서로 [프로필에 대한 개인 정보 보호 요청 처리](../profile/privacy.md) 이 튜토리얼 외에.
>
>다른 Adobe Experience Cloud 애플리케이션에 대한 개인 정보 보호 요청을 하는 방법에 대한 단계는 [Privacy Service 설명서](../privacy-service/experience-cloud-apps.md).

## 시작하기

다음 사항을 잘 알고 있는 것이 좋습니다 [!DNL Experience Platform] 이 안내서를 읽기 전의 서비스:

* [[!DNL Privacy Service]](../privacy-service/home.md): Adobe Experience Cloud 애플리케이션 전반에 걸친 개인 데이터 액세스, 판매 중지 또는 삭제에 대한 고객 요청을 관리합니다.
* [[!DNL Identity Service]](../identity-service/home.md): 디바이스와 시스템 간에 ID를 연결하여 고객 경험 데이터의 단편화로 인해 발생하는 근본적인 문제를 해결합니다.
* [[!DNL Real-Time Customer Profile]](home.md): 여러 소스의 집계 데이터를 기반으로 통합 실시간 소비자 프로필을 제공합니다.

## ID 네임스페이스 이해 {#namespaces}

Adobe Experience Platform [!DNL Identity Service] 시스템 및 장치 간에 고객 id 데이터를 연결합니다. [!DNL Identity Service] 사용 **id 네임스페이스** ID 값을 원래 시스템에 연결하여 컨텍스트를 제공합니다. 네임스페이스는 이메일 주소(&quot;이메일&quot;)와 같은 일반적인 개념을 나타내거나 Adobe Advertising Cloud ID(&quot;AdCloud&quot;) 또는 Adobe Target ID(&quot;TNTID&quot;)와 같은 특정 애플리케이션과 ID를 연결할 수 있습니다.

ID 서비스는 전역 정의(표준) 및 사용자 정의(사용자 정의) ID 네임스페이스 저장소를 유지 관리합니다. 표준 네임스페이스는 모든 조직에서 사용할 수 있으며(예: &quot;이메일&quot; 및 &quot;ECID&quot;), 조직에서는 특정 요구 사항에 맞게 사용자 정의 네임스페이스를 만들 수도 있습니다.

의 ID 네임스페이스에 대한 자세한 내용 [!DNL Experience Platform], 다음을 참조하십시오. [id 네임스페이스 개요](../identity-service/features/namespaces.md).

## 요청 제출 {#submit}

아래 섹션에서는 다음에 대한 개인 정보 보호 요청을 하는 방법에 대해 간략하게 설명합니다. [!DNL Identity Service] 사용 [!DNL Privacy Service] API 또는 UI. 이 섹션을 읽기 전에 다음을 검토하는 것이 좋습니다. [PRIVACY SERVICE API](../privacy-service/api/getting-started.md) 또는 [PRIVACY SERVICE UI](../privacy-service/ui/overview.md) 요청 페이로드에서 사용자 데이터의 형식을 제대로 지정하는 방법을 포함하여 개인 정보 보호 작업을 제출하는 방법에 대한 전체 단계에 대한 설명서입니다.

### API 사용

API에서 작업 요청을 만들 때 내에 제공된 모든 ID `userIDs` 은(는) 다음을 사용해야 합니다. `namespace` 및 `type`. 유효 [id 네임스페이스](#namespaces) 인식한 사람 [!DNL Identity Service] 다음에 대한 을(를) 제공해야 합니다. `namespace` 값, 반면에 `type` 은(는) 다음 중 하나여야 합니다. `standard` 또는 `unregistered` (표준 및 사용자 정의 네임스페이스의 경우 각각).

또한 `include` 요청 페이로드의 배열에는 요청이 수행되는 다양한 데이터 저장소에 대한 제품 값이 포함되어야 합니다. 에 요청할 때 [!DNL Identity], 배열에는 값이 포함되어야 합니다. `Identity`.

다음 요청은 의 단일 고객 데이터에 대해 GDPR에 따라 새 개인 정보 보호 작업을 만듭니다. [!DNL Identity] 저장. 에서 고객을 위한 두 가지 ID 값이 제공됩니다. `userIDs` 배열, 표준을 사용하는 배열 `Email` id 네임스페이스 및 를 사용하는 다른 네임스페이스 `ECID` 네임스페이스, 여기에는 제품 값도 포함됩니다. [!DNL Identity] (`Identity`)에 있는 `include` 배열:

>[!TIP]
>
>API를 사용하여 사용자 지정 네임스페이스를 삭제하는 경우 표시 이름 대신 ID 기호를 네임스페이스로 지정해야 합니다.

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
>UI를 사용하여 사용자 지정 네임스페이스를 삭제할 때 표시 이름 대신 ID 기호를 네임스페이스로 지정해야 합니다. 또한 비프로덕션 샌드박스에 대해 UI에서 사용자 정의 네임스페이스를 삭제할 수 없습니다.

UI에서 작업 요청을 만들 때 다음을 선택해야 합니다. **[!UICONTROL 신원]** 아래에 **[!UICONTROL 제품]** 에 저장된 데이터에 대한 작업을 처리하기 위해 [!DNL Identity Service].

![id-gdpr](./images/identity-gdpr.png)

## 삭제 요청 처리

날짜 [!DNL Experience Platform] 에서 삭제 요청을 수신합니다. [!DNL Privacy Service], [!DNL Platform] (으)로 확인 보내기 [!DNL Privacy Service] 요청을 수신하고 영향을 받는 데이터를 삭제하도록 표시했는지 여부. 개별 ID의 삭제는 제공된 네임스페이스 및/또는 ID 값을 기반으로 합니다. 또한 해당 조직과 연관된 모든 샌드박스에 대해 삭제가 수행됩니다.

실시간 고객 프로필도 포함했는지 여부에 따라 달라집니다(`ProfileService`) 및 데이터 레이크(`aepDataLake`)를 ID 서비스에 대한 개인 정보 보호 요청의 제품으로 사용(`identity`) id와 관련된 다른 데이터 세트는 잠재적으로 다른 시간에 시스템에서 제거됩니다.

| 포함된 제품 | 효과 |
| --- | --- |
| `identity` 전용 | 제공된 ID는 플랫폼이 삭제 요청이 수신되었다는 확인을 전송하는 즉시 삭제됩니다. 해당 ID 그래프에서 생성된 프로필은 여전히 남아 있지만 이제 ID 연결이 제거되므로 새 데이터가 수집될 때 업데이트되지 않습니다. 프로필과 연결된 데이터도 데이터 레이크에 유지됩니다. |
| `identity` 및 `ProfileService` | 제공된 ID는 플랫폼이 삭제 요청이 수신되었다는 확인을 전송하는 즉시 삭제됩니다. 프로필과 연결된 데이터는 데이터 레이크에 유지됩니다. |
| `identity` 및 `aepDataLake` | 제공된 ID는 플랫폼이 삭제 요청이 수신되었다는 확인을 전송하는 즉시 삭제됩니다. 해당 ID 그래프에서 생성된 프로필은 여전히 남아 있지만 이제 ID 연결이 제거되므로 새 데이터가 수집될 때 업데이트되지 않습니다.<br><br>데이터 레이크 제품이 요청을 받고 현재 처리 중이라는 응답을 하는 경우 프로필과 연관된 데이터가 일시 삭제되므로 다른 사용자도 해당 데이터에 액세스할 수 없습니다 [!DNL Platform] 서비스. 작업이 완료되면 데이터가 데이터 레이크에서 완전히 제거됩니다. |
| `identity`, `ProfileService` 및 `aepDataLake` | 제공된 ID는 플랫폼이 삭제 요청이 수신되었다는 확인을 전송하는 즉시 삭제됩니다.<br><br>데이터 레이크 제품이 요청을 받고 현재 처리 중이라는 응답을 하는 경우 프로필과 연관된 데이터가 일시 삭제되므로 다른 사용자도 해당 데이터에 액세스할 수 없습니다 [!DNL Platform] 서비스. 작업이 완료되면 데이터가 데이터 레이크에서 완전히 제거됩니다. |

다음을 참조하십시오. [[!DNL Privacy Service] 설명서](../privacy-service/home.md#monitor) 작업 상태 추적에 대한 자세한 내용을 참조하십시오.

## 다음 단계

이 문서를 읽으면에서 개인 정보 보호 요청 처리와 관련된 중요한 개념에 대해 소개합니다 [!DNL Identity Service]. 기타 개인 정보 보호 요청 처리에 대한 정보 [!DNL Experience Cloud] 응용 프로그램의 경우 다음 문서를 참조하십시오. [[!DNL Privacy Service] 및 [!DNL Experience Cloud] 응용 프로그램](../privacy-service/experience-cloud-apps.md).
