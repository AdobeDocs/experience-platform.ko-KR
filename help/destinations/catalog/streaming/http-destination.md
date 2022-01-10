---
keywords: 스트리밍;
title: HTTP API 연결
description: Adobe Experience Platform의 HTTP API 대상을 사용하면 프로필 데이터를 타사 HTTP 엔드포인트로 보낼 수 있습니다.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: b0c2c8313e05d1316f23dc15d99893e1887f8dcf
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 1%

---

# (베타) [!DNL HTTP] API 연결

>[!IMPORTANT]
>
>다음 [!DNL HTTP] 플랫폼의 대상은 현재 베타 버전입니다. 설명서 및 기능은 변경될 수 있습니다.

## 개요 {#overview}

다음 [!DNL HTTP] API 대상은 [!DNL Adobe Experience Platform] 프로필 데이터를 타사 사용자에게 전송하는 데 도움이 되는 스트리밍 대상 [!DNL HTTP] 엔드포인트.

프로필 데이터를 로 보내려면 [!DNL HTTP] 끝점은 먼저 대상의 대상에 연결해야 합니다 [[!DNL Adobe Experience Platform]](#connect-destination).

## 사용 사례 {#use-cases}

다음 [!DNL HTTP] 대상은 XDM 프로필 데이터 및 대상 세그먼트를 일반 세그먼트로 내보내야 하는 고객을 대상으로 합니다 [!DNL HTTP] 엔드포인트.

[!DNL HTTP] 엔드포인트는 고객의 시스템 또는 타사 솔루션일 수 있습니다.

## 대상에 연결 {#connect}

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md).

### 연결 매개 변수 {#parameters}

While [설정](../../ui/connect-destination.md) 이 대상을 사용하려면 다음 정보를 제공해야 합니다.

* **[!UICONTROL httpEndpoint]**: a [!DNL URL] 프로필 데이터를 보낼 HTTP 끝점입니다.
   * 선택적으로 쿼리 매개 변수를 [!UICONTROL httpEndpoint] [!DNL URL].
* **[!UICONTROL authEndpoint]**: a [!DNL URL] 에 사용되는 HTTP 끝점의 [!DNL OAuth2] 인증.
* **[!UICONTROL 클라이언트 ID]**: a [!DNL clientID] 에 사용된 매개 변수 [!DNL OAuth2] 클라이언트 자격 증명입니다.
* **[!UICONTROL 클라이언트 암호]**: a [!DNL clientSecret] 에 사용된 매개 변수 [!DNL OAuth2] 클라이언트 자격 증명입니다.

   >[!NOTE]
   >
   >전용 [!DNL OAuth2] 클라이언트 자격 증명은 현재 지원됩니다.

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 이름을 입력합니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명을 입력합니다.
* **[!UICONTROL 사용자 지정 헤더]**: 다음 형식을 사용하여 대상 호출에 포함할 사용자 지정 헤더를 입력합니다. `header1:value1,header2:value2,...headerN:valueN`.

   >[!IMPORTANT]
   >
   >현재 구현에는 하나 이상의 사용자 지정 헤더가 필요합니다. 이 제한은 향후 업데이트에서 해결됩니다.

## 세그먼트를 이 대상에 활성화 {#activate}

자세한 내용은 [스트리밍 프로필 내보내기 대상으로 대상 데이터 활성화](../../ui/activate-streaming-profile-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

### 대상 속성 {#attributes}

에서 [[!UICONTROL 속성 선택]](../../ui/activate-streaming-profile-destinations.md#select-attributes) Adobe은 사용자 지정 페이지에서 고유 식별자를 선택할 것을 권장합니다 [조합 스키마](../../../profile/home.md#profile-fragments-and-union-schemas). 대상으로 내보낼 고유 식별자 및 기타 모든 XDM 필드를 선택합니다.

## 프로필 내보내기 동작 {#profile-export-behavior}

Experience Platform은 세그먼트 자격 또는 기타 중요한 이벤트 후에 프로필에 대한 관련 업데이트가 발생한 경우에만 데이터를 API 종단점으로 내보내도록 프로필 내보내기 동작을 HTTP API 대상에 최적화합니다. 프로필은 다음과 같은 상황에서 대상에 내보내집니다.

* 대상에 매핑된 세그먼트 중 하나 이상에 대한 세그먼트 멤버십 변경으로 프로필 업데이트가 트리거되었습니다. 예를 들어 프로필이 대상에 매핑된 세그먼트 중 하나에 적격이거나 대상에 매핑된 세그먼트 중 하나를 끝냈습니다.
* 프로필 업데이트는 [id 맵](/help/xdm/field-groups/profile/identitymap.md). 예를 들어 대상에 매핑된 세그먼트 중 하나에 대해 이미 자격이 있는 프로필이 ID 맵 속성에 새 ID를 추가했습니다.
* 대상에 매핑된 특성 중 하나 이상에 대한 특성 변경으로 프로필 업데이트가 트리거되었습니다. 예를 들어 매핑 단계에서 대상에 매핑된 속성 중 하나가 프로필에 추가됩니다.

위에 설명된 모든 경우 관련 업데이트가 발생한 프로필만 대상으로 내보내집니다. 예를 들어 대상 플로우에 매핑된 세그먼트에 100개의 멤버가 있고 5개의 새 프로필이 세그먼트에 대한 자격이 있는 경우 대상에 내보내기는 증분 결과이며 5개의 새 프로필만 포함합니다.

변경 사항이 있는 위치에 상관없이 모든 매핑된 속성이 프로필에 대해 내보내집니다. 따라서 위의 예에서 이러한 5개의 새 프로필에 대해 매핑된 속성은 속성 자체가 변경되지 않았더라도 내보내집니다.

## 내보낸 데이터 {#exported-data}

내보낸 [!DNL Experience Platform] 데이터가 [!DNL HTTP] JSON 형식으로 대상을 타깃팅합니다. 예를 들어, 아래 이벤트는 특정 세그먼트에 대해 자격이 있고 다른 세그먼트를 종료한 대상의 이메일 주소 프로필 속성을 포함합니다. 이 잠재 고객의 ID는 [!DNL ECID] 및 이메일을 사용할 수 있습니다.

```json
{
  "person": {
    "birthDate": "YYYY-MM-DD",
    "name": {
      "firstName": "John",
      "lastName": "Doe"
    }
  },
  "personalEmail": {
    "address": "john.doe@acme.com"
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
