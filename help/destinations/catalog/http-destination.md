---
keywords: 스트리밍;
title: HTTP 연결
description: Adobe Experience Platform의 HTTP 대상을 사용하면 프로필 데이터를 타사 HTTP 종단점으로 보낼 수 있습니다.
exl-id: 165a8085-c8e6-4c9f-8033-f203522bb288
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 3%

---

# (알파) [!DNL HTTP] 연결

>[!IMPORTANT]
>
>플랫폼의 [!DNL HTTP] 대상이 현재 알파에 있습니다. 설명서 및 기능은 변경될 수 있습니다.

## 개요 {#overview}

[!DNL HTTP] 대상은 프로필 데이터를 타사 [!DNL HTTP] 종단점으로 전송하는 데 도움이 되는 [!DNL Adobe Experience Platform] 스트리밍 대상입니다.

프로필 데이터를 [!DNL HTTP] 종단점으로 보내려면 먼저 [[!DNL Adobe Experience Platform]](#connect-destination)에서 대상에 연결해야 합니다.

## 사용 사례 {#use-cases}

[!DNL HTTP] 대상은 XDM 프로필 데이터 및 대상 세그먼트를 일반 [!DNL HTTP] 종단점으로 내보내야 하는 고객을 대상으로 합니다.

[!DNL HTTP] 엔드포인트는 고객의 시스템 또는 타사 솔루션일 수 있습니다.

## 대상에 연결 {#connect}

이 대상에 연결하려면 [대상 구성 자습서](../ui/connect-destination.md)에 설명된 단계를 따르십시오.

### 연결 매개 변수 {#parameters}

[이 대상을 설정할 때 다음 정보를 제공해야 합니다.](../ui/connect-destination.md)

* **[!UICONTROL httpEndpoint]**: 프로필 데이터 [!DNL URL] 를 보낼 HTTP 끝점의 끝점입니다.
   * 원할 경우 [!UICONTROL httpEndpoint] [!DNL URL]에 쿼리 매개 변수를 추가할 수 있습니다.
* **[!UICONTROL authEndpoint]**: 인증 [!DNL URL] 에 사용되는 HTTP 끝점의  [!DNL OAuth2] 끝점입니다.
* **[!UICONTROL 클라이언트 ID]**: 클라이언트  [!DNL clientID] 자격 증명에 사용되는  [!DNL OAuth2] 매개 변수입니다.
* **[!UICONTROL 클라이언트 암호]**: 클라이언트  [!DNL clientSecret] 자격 증명에 사용되는  [!DNL OAuth2] 매개 변수입니다.

   >[!NOTE]
   >
   >현재 [!DNL OAuth2] 클라이언트 자격 증명만 지원됩니다.

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 이름을 입력합니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명을 입력합니다.
* **[!UICONTROL 사용자 지정 헤더]**: 다음 형식을 사용하여 대상 호출에 포함할 사용자 지정 헤더를 입력합니다.  `header1:value1,header2:value2,...headerN:valueN`.

   >[!IMPORTANT]
   >
   >현재 구현에는 하나 이상의 사용자 지정 헤더가 필요합니다. 이 제한은 향후 업데이트에서 해결됩니다.

## 세그먼트를 이 대상에 활성화 {#activate}

대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침은 [스트리밍 프로필 내보내기 대상으로 대상 활성화](../ui/activate-streaming-profile-destinations.md)를 참조하십시오.

### 대상 속성 {#attributes}

[[!UICONTROL 속성 선택]](../ui/activate-streaming-profile-destinations.md#select-attributes) 단계의 Adobe에서 [결합 스키마](../../profile/home.md#profile-fragments-and-union-schemas)에서 고유 식별자를 선택하는 것이 좋습니다. 대상으로 내보낼 고유 식별자 및 기타 모든 XDM 필드를 선택합니다.

## 내보낸 데이터 {#exported-data}

내보낸 [!DNL Experience Platform] 데이터가 [!DNL HTTP] 대상에 JSON 형식으로 전달됩니다. 예를 들어, 아래 이벤트는 특정 세그먼트에 대해 자격이 있고 다른 세그먼트를 종료한 대상의 이메일 주소 프로필 속성을 포함합니다. 이 잠재 고객의 ID는 [!DNL ECID] 및 이메일입니다.

```json
{
  "person": {
    "email": "yourstruly@adobe.con"
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
