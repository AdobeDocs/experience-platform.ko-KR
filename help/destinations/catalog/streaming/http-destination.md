---
keywords: streaming;
title: HTTP 연결
description: Adobe Experience Platform의 HTTP API 대상을 사용하면 프로필 데이터를 타사 HTTP 엔드포인트로 보낼 수 있습니다.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 8d2c5ef477d4707be4c0da43ba1f672fac797604
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 1%

---

# (Beta) [!DNL HTTP] API connection

>[!IMPORTANT]
>
>다음 [!DNL HTTP] 플랫폼의 대상은 현재 베타 버전입니다. 설명서 및 기능은 변경될 수 있습니다.

## 개요 {#overview}

다음 [!DNL HTTP] API 대상은 [!DNL Adobe Experience Platform] 프로필 데이터를 타사 사용자에게 전송하는 데 도움이 되는 스트리밍 대상 [!DNL HTTP] 엔드포인트.

To send profile data to [!DNL HTTP] endpoints, you must first connect to the destination in [[!DNL Adobe Experience Platform]](#connect-destination).

## 사용 사례 {#use-cases}

다음 [!DNL HTTP] 대상은 XDM 프로필 데이터 및 대상 세그먼트를 일반 세그먼트로 내보내야 하는 고객을 대상으로 합니다 [!DNL HTTP] 엔드포인트.

[!DNL HTTP] endpoints can be either customers&#39; own systems  or third-party solutions.

## Connect to the destination {#connect}

To connect to this destination, follow the steps described in the [destination configuration tutorial](../../ui/connect-destination.md).

### 연결 매개 변수 {#parameters}

While [설정](../../ui/connect-destination.md) 이 대상을 사용하려면 다음 정보를 제공해야 합니다.

* **[!UICONTROL httpEndpoint]**: a [!DNL URL] 프로필 데이터를 보낼 HTTP 끝점입니다.
   * Optionally, you can add query parameters to the [!UICONTROL httpEndpoint] [!DNL URL].
* **[!UICONTROL authEndpoint]**: a [!DNL URL] 에 사용되는 HTTP 끝점의 [!DNL OAuth2] 인증.
* **[!UICONTROL 클라이언트 ID]**: a [!DNL clientID] 에 사용된 매개 변수 [!DNL OAuth2] 클라이언트 자격 증명입니다.
* **[!UICONTROL Client Secret]**: the [!DNL clientSecret] parameter used in the [!DNL OAuth2] client credentials.

   >[!NOTE]
   >
   >전용 [!DNL OAuth2] 클라이언트 자격 증명은 현재 지원됩니다.

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 이름을 입력합니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명을 입력합니다.
* **[!UICONTROL 사용자 지정 헤더]**: 다음 형식을 사용하여 대상 호출에 포함할 사용자 지정 헤더를 입력합니다. `header1:value1,header2:value2,...headerN:valueN`.

   >[!IMPORTANT]
   >
   >The current implementation requires at least one custom header. 이 제한은 향후 업데이트에서 해결됩니다.

## 세그먼트를 이 대상에 활성화 {#activate}

자세한 내용은 [스트리밍 프로필 내보내기 대상으로 대상 데이터 활성화](../../ui/activate-streaming-profile-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

### Destination attributes {#attributes}

에서 [[!UICONTROL 속성 선택]](../../ui/activate-streaming-profile-destinations.md#select-attributes) Adobe은 사용자 지정 페이지에서 고유 식별자를 선택할 것을 권장합니다 [조합 스키마](../../../profile/home.md#profile-fragments-and-union-schemas). Select the unique identifier and any other XDM fields that you want to export to the destination.

## Profile export behavior {#profile-export-behavior}

Experience Platform optimizes the profile export behavior to your HTTP API destination, to only export data to your API endpoint when relevant updates to a profile have occurred following segment qualification or other significant events. 프로필은 다음과 같은 상황에서 대상에 내보내집니다.

* The profile update was triggered by a change in segment membership for at least one of the segments mapped to the destination. For example, the profile has qualified for one of the segments mapped to the destination or has exited one of the segments mapped to the destination.
* 프로필 업데이트는 [id 맵](/help/xdm/field-groups/profile/identitymap.md). 예를 들어 대상에 매핑된 세그먼트 중 하나에 대해 이미 자격이 있는 프로필이 ID 맵 속성에 새 ID를 추가했습니다.
* The profile update was triggered by a change in attributes for at least one of the attributes mapped to the destination. For example, one of the attributes mapped to the destination in the mapping step is added to a profile.

위에 설명된 모든 경우 관련 업데이트가 발생한 프로필만 대상으로 내보내집니다. For example, if a segment mapped to the destination flow has a hundred members, and five new profiles qualify for the segment, the export to your destination is incremental and only includes the five new profiles.

Note that the all the mapped attributes are exported for a profile, no matter where the changes lie. 따라서 위의 예에서 이러한 5개의 새 프로필에 대해 매핑된 속성은 속성 자체가 변경되지 않았더라도 내보내집니다.

## 내보낸 데이터 {#exported-data}

내보낸 [!DNL Experience Platform] 데이터가 [!DNL HTTP] JSON 형식으로 대상을 타깃팅합니다. For example, the event below contains the email address profile attribute of an audience that has qualified for a certain segment and exited another segment. The identities for this prospect are [!DNL ECID] and email.

```json
{
  "person": {
    "email": "yourstruly@adobe.com"
  },
  "segmentMembership": {
    "ups": {
      "7841ba61-23c1-4bb3-a495-00d3g5fe1e93": {
        "lastQualificationTime": "2020-05-25T21:24:39Z",
        "status": "exited"
      },
      "59bd2fkd-3c48-4b18-bf56-4f5c5e6967ae": {
        "lastQualificationTime": "2020-05-25T23:37:33Z",
        "status": "existing"
      }
    }
  },
  "identityMap": {
    "ecid": [
      {
        "id": "14575006536349286404619648085736425115"
      },
      {
        "id": "66478888669296734530114754794777368480"
      }
    ],
    "email_lc_sha256": [
      {
        "id": "655332b5fa2aea4498bf7a290cff017cb4"
      },
      {
        "id": "66baf76ef9de8b42df8903f00e0e3dc0b7"
      }
    ]
  }
}
```
