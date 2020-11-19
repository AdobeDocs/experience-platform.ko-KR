---
keywords: streaming;
title: HTTP 대상은 프로필 데이터를 타사 HTTP 끝점으로 보내는 데 도움이 되는 실시간 고객 데이터 플랫폼 대상입니다.
seo-title: HTTP 대상은 프로필 데이터를 타사 HTTP 끝점으로 보내는 데 도움이 되는 실시간 고객 데이터 플랫폼 대상입니다.
description: HTTP 대상은 프로필 데이터를 타사 HTTP 끝점으로 보내는 데 도움이 되는 실시간 고객 데이터 플랫폼 대상입니다.
seo-description: HTTP 대상은 프로필 데이터를 타사 HTTP 끝점으로 보내는 데 도움이 되는 실시간 고객 데이터 플랫폼 대상입니다.
translation-type: tm+mt
source-git-commit: 6eabcd70b133051205b669253f280cb92c24412f
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 2%

---


# (알파) [!DNL HTTP] 대상

>[!IMPORTANT]
>
>Adobe 실시간 CDP의 [!DNL HTTP] 대상은 현재 알파에 있습니다. 설명서 및 기능은 변경될 수 있습니다.

## 개요 {#overview}

대상 [!DNL HTTP] 은 [!DNL Real-time Customer Data Platform] 프로필 데이터를 타사 끝점으로 보내는 데 도움이 되는 스트리밍 [!DNL HTTP] 대상입니다.

끝점에 프로필 데이터를 [!DNL HTTP] 보내려면 먼저 해당 대상의 대상에 연결해야 합니다 [[!DNL Real-time Customer Data Platform]](#connect-destination).

## 사용 사례 {#use-cases}

대상 [!DNL HTTP] 은 XDM 프로필 데이터 및 대상 세그먼트를 일반 [!DNL HTTP] 끝점으로 내보내야 하는 고객을 대상으로 합니다.

[!DNL HTTP] 끝점은 고객의 자체 시스템 또는 타사 솔루션일 수 있습니다.

## 대상에 연결 {#connect-destination}

1. [ **[!UICONTROL 연결]** ] > **[!UICONTROL 대상]**&#x200B;에서 [!DNL HTTP API]를 선택하고 구성을 **[!UICONTROL 선택합니다]**.

   ![HTTP 대상 활성화](assets/activate-http-destination.png)

   >[!NOTE]
   >
   >이 대상과의 연결이 이미 있는 경우 대상 카드에 **[!UICONTROL 활성화]** 단추가 표시됩니다. 활성화 및 구성 **[!UICONTROL 의 차이에 대한 자세한]****[!UICONTROL 내용은 대상 작업 공간 설명서의]**&#x200B;카탈로그 [섹션을](../destinations/destinations-workspace.md#catalog) 참조하십시오.
   >
   >![HTTP 대상 활성화](assets/connect-http-destination.png)

2. 계정 [!UICONTROL 단계에서] HTTP 끝점 연결 세부 사항을 정의해야 합니다. [ **[!UICONTROL 새 계정]** ]을 선택하고 연결할 HTTP 끝점에 대한 연결 세부 사항을 입력합니다.
   * **[!UICONTROL httpEndpoint]**:프로필 데이터 [!DNL URL] 를 보낼 HTTP 끝점의 완성입니다.
      * 선택적으로 [!UICONTROL httpEndpoint에 쿼리 매개 변수를 추가할 수 있습니다] [!DNL URL].
   * **[!UICONTROL authEndpoint]**:인증에 사용된 HTTP 끝점 [!DNL URL] 의 [!DNL OAuth2] 전체
   * **[!UICONTROL 클라이언트 ID]**:클라이언트 자격 증명에 사용되는 [!DNL clientID] 매개 [!DNL OAuth2] 변수입니다.
   * **[!UICONTROL 클라이언트 암호]**:클라이언트 자격 증명에 사용되는 [!DNL clientSecret] 매개 [!DNL OAuth2] 변수입니다.

   >[!NOTE]
   >
   >현재 [!DNL OAuth2] 클라이언트 자격 증명만 지원됩니다.

   ![HTTP 끝점 연결](assets/connect-http-endpoint.png)
3. 대상에 **[!UICONTROL 연결을 클릭합니다]**.
4. 연결이 성공하면 [다음]을 **[!UICONTROL 클릭합니다]**.
5. 인증 [!UICONTROL 단계에서] 계정 인증 자격 증명을 입력합니다.
   * **[!UICONTROL 이름]**:나중에 이 대상을 인식할 이름을 입력합니다.
   * **[!UICONTROL 설명]**:나중에 이 대상을 식별하는 데 도움이 되는 설명을 입력합니다.
   * **[!UICONTROL 사용자 지정 헤더]**:이 형식을 따라 대상 호출에 포함할 사용자 지정 헤더를 입력합니다. `header1:value1,header2:value2,...headerN:valueN`.

      >[!IMPORTANT]
      >
      >현재 구현에는 하나 이상의 사용자 지정 헤더가 필요합니다. 이 제한은 향후 업데이트로 해결됩니다.
   ![HTTP 인증](assets/authentication-http-connection.png)

6. **[!UICONTROL 마케팅 활용 사례]**:마케팅 사용 사례에서는 데이터를 대상으로 내보내려는 의도를 나타냅니다. Adobe에서 정의한 마케팅 사용 사례에서 선택하거나 고유한 마케팅 사용 사례를 만들 수 있습니다. 마케팅 활용 사례에 대한 자세한 내용은 실시간 CDP의 [데이터 거버넌스](../privacy/data-governance-overview.md#destinations) 페이지를 참조하십시오. 개별 Adobe에서 정의한 마케팅 사용 사례에 대한 자세한 내용은 [데이터 사용 정책 개요를 참조하십시오](../../data-governance/policies/overview.md#core-actions).
7. 대상 **[!UICONTROL 만들기를 클릭합니다]**.

## 세그먼트 활성화

세그먼트 [활성화 워크플로에 대한 자세한 내용은 대상에](activate-destinations.md#select-attributes) 프로필 및 세그먼트 활성화를 참조하십시오.

## 대상 속성

속성 [[!UICONTROL 선택]](activate-destinations.md#select-attributes) 단계 동안 세그먼트를 [대상으로](activate-destinations.md) 활성화할 [!DNL HTTP] 때 [조합 스키마에서 고유 식별자를 선택하는 것이 좋습니다](../../profile/home.md#profile-fragments-and-union-schemas). 대상으로 내보낼 고유 식별자 및 기타 XDM 필드를 선택합니다.

## 내보낸 데이터 {#exported-data}

내보낸 [!DNL Experience Platform] 데이터는 JSON 형식으로 [!DNL HTTP] 대상에 배치됩니다. 예를 들어, 아래 이벤트에는 특정 세그먼트에 자격을 부여하여 다른 세그먼트를 종료한 대상자의 이메일 주소 프로필 속성이 포함되어 있습니다. 이 잠재 고객의 ID는 [!DNL ECID] 및 이메일입니다.

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
