---
keywords: 스트리밍;
title: HTTP 연결
description: Adobe Experience Platform의 HTTP 대상을 사용하면 프로필 데이터를 타사 HTTP 끝점으로 보낼 수 있습니다.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 2%

---


# (알파) [!DNL HTTP] 연결

>[!IMPORTANT]
>
>플랫폼의 [!DNL HTTP] 대상이 현재 알파입니다. 설명서 및 기능은 변경될 수 있습니다.

## 개요 {#overview}

[!DNL HTTP] 대상은 제3자 [!DNL HTTP] 끝점으로 프로필 데이터를 보내는 데 도움이 되는 [!DNL Adobe Experience Platform] 스트리밍 대상입니다.

프로필 데이터를 [!DNL HTTP] 끝점으로 보내려면 먼저 [[!DNL Adobe Experience Platform]](#connect-destination)에서 대상에 연결해야 합니다.

## 사용 사례 {#use-cases}

[!DNL HTTP] 대상은 XDM 프로필 데이터 및 대상 세그먼트를 일반 [!DNL HTTP] 끝점으로 내보내야 하는 고객을 대상으로 합니다.

[!DNL HTTP] 끝점은 고객의 자체 시스템 또는 타사 솔루션일 수 있습니다.

## 대상 {#connect-destination}에 연결

**[!UICONTROL Connections]** > **[!UICONTROL Destinations]**&#x200B;에서 [!DNL HTTP API]를 선택하고 **[!UICONTROL Configure]**&#x200B;을 선택합니다.

![HTTP 대상 활성화](../assets/catalog/http/activate.png)

이 대상과의 연결이 이미 있는 경우 대상 카드에 **[!UICONTROL Activate]** 단추가 표시될 수 있습니다. **[!UICONTROL Activate]**&#x200B;과 **[!UICONTROL Configure]** 사이의 차이에 대한 자세한 내용은 대상 작업 공간 설명서의 [카탈로그](../ui/destinations-workspace.md#catalog) 섹션을 참조하십시오.

![HTTP 대상 활성화](../assets/catalog/http/connect.png)

[!UICONTROL Account] 단계에서 HTTP 끝점 연결 세부 사항을 정의해야 합니다. **[!UICONTROL New account]**&#x200B;을 선택하고 연결할 HTTP 끝점의 연결 세부 사항을 입력합니다.
- **[!UICONTROL httpEndpoint]**:프로필 데이터 [!DNL URL] 를 보낼 HTTP 끝점의 완성입니다.
   - 선택적으로 쿼리 매개 변수를 [!UICONTROL httpEndpoint] [!DNL URL]에 추가할 수 있습니다.
- **[!UICONTROL authEndpoint]**:인증에 사용되는 HTTP 끝점 [!DNL URL] 의  [!DNL OAuth2] 전체
- **[!UICONTROL Client ID]**:클라이언트  [!DNL clientID] 자격 증명에 사용되는  [!DNL OAuth2] 매개 변수입니다.
- **[!UICONTROL Client Secret]**:클라이언트  [!DNL clientSecret] 자격 증명에 사용되는  [!DNL OAuth2] 매개 변수입니다.

>[!NOTE]
>
>현재 [!DNL OAuth2] 클라이언트 자격 증명만 지원됩니다.

![HTTP 끝점 연결](../assets/catalog/http/connect.png)

**[!UICONTROL Connect to destination]**&#x200B;을 클릭합니다. 연결이 성공하면 **[!UICONTROL Next]**&#x200B;을 클릭합니다.

[!UICONTROL Authentication] 단계에서 계정 인증 자격 증명을 입력합니다.
- **[!UICONTROL Name]**:나중에 이 대상을 인식할 이름을 입력합니다.
- **[!UICONTROL Description]**:나중에 이 대상을 식별하는 데 도움이 되는 설명을 입력합니다.
- **[!UICONTROL Custom Headers]**:다음 형식을 따라 대상 호출에 포함할 사용자 지정 헤더를 입력합니다. `header1:value1,header2:value2,...headerN:valueN`.
- **[!UICONTROL Marketing actions]**:마케팅 작업은 데이터를 대상에 내보내려는 의도를 나타냅니다. Adobe 정의 마케팅 작업 중에서 선택하거나 자신의 마케팅 작업을 만들 수 있습니다. 마케팅 작업에 대한 자세한 내용은 Adobe Experience Platform](/help/data-governance/policies/overview.md) 페이지의 [데이터 거버넌스 페이지를 참조하십시오. 개별 Adobe 정의 마케팅 작업에 대한 자세한 내용은 [데이터 사용 정책 개요](/help/data-governance/policies/overview.md)를 참조하십시오.

>[!IMPORTANT]
>
>현재 구현에는 하나 이상의 사용자 지정 머리글이 필요합니다. 이 제한은 향후 업데이트로 해결됩니다.

![HTTP 인증](../assets/catalog/http/authenticate.png)

**[!UICONTROL Marketing action]**:마케팅 작업은 데이터를 대상에 내보내려는 의도를 나타냅니다. Adobe 정의 마케팅 작업 중에서 선택하거나 자신의 마케팅 작업을 만들 수 있습니다. 마케팅 작업에 대한 자세한 내용은 [데이터 사용 정책 개요](../../data-governance/policies/overview.md)를 참조하십시오.

**[!UICONTROL Create destination]**&#x200B;을 클릭합니다.

## 세그먼트 활성화

세그먼트 활성화 작업 과정에 대한 자세한 내용은 [프로필 및 세그먼트를 대상](../ui/activate-destinations.md#select-attributes)에 활성화를 참조하십시오.

## 대상 속성

[[!UICONTROL Select attributes]](../ui/activate-destinations.md#select-attributes) 단계 동안 [세그먼트](../ui/activate-destinations.md)를 [!DNL HTTP] 대상으로 활성화할 때 [union 스키마](../../profile/home.md#profile-fragments-and-union-schemas)에서 고유한 식별자를 선택하는 것이 좋습니다. 대상으로 내보낼 고유 식별자 및 기타 XDM 필드를 선택합니다.

## 내보낸 데이터 {#exported-data}

내보낸 [!DNL Experience Platform] 데이터는 JSON 형식으로 [!DNL HTTP] 대상에 포함됩니다. 예를 들어, 아래 이벤트에는 특정 세그먼트에 자격을 갖추고 다른 세그먼트를 종료한 대상자의 이메일 주소 프로필 속성이 포함되어 있습니다. 이 잠재 고객의 ID는 [!DNL ECID] 및 이메일입니다.

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
