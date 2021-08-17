---
keywords: 모바일; brize; 메시징;
title: 연결 브레이즈
description: Braze는 고객과 고객이 좋아하는 브랜드 간 연관성 있고 기억에 남을 경험을 제공하는 포괄적인 고객 참여 플랫폼입니다.
exl-id: 508e79ee-7364-4553-b153-c2c00cc85a73
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 2%

---

# (베타) [!DNL Braze] 연결

>[!IMPORTANT]
>
>Adobe Experience Platform의 브레이징 대상은 현재 베타에 있습니다. 설명서 및 기능은 변경될 수 있습니다.

## 개요 {#overview}

[!DNL Braze] 대상은 프로필 데이터를 [!DNL Braze]에 전송하는 데 도움이 됩니다.

[!DNL Braze] 는 고객과 고객이 좋아하는 브랜드 간 연관성 있고 기억에 남을 경험을 제공하는 포괄적인 고객 참여 플랫폼입니다.

프로필 데이터를 [!DNL Braze]에 보내려면 먼저 대상에 연결해야 합니다.

## 대상 세부 사항 {#specifics}

[!DNL Braze] 대상에 해당하는 다음 세부 사항을 참고하십시오.

* [!DNL Adobe Experience Platform] 세그먼트는 속성  [!DNL Braze] 아래에 로  `AdobeExperiencePlatformSegments` 내보내집니다.

>[!NOTE]
>
>추가 사용자 지정 특성을 [!DNL Braze]에 보내면 [!DNL Braze] 데이터 포인트 사용량이 늘어날 수 있습니다. 추가 사용자 지정 특성을 보내기 전에 [!DNL Braze] 계정 관리자에게 문의하십시오.

## 사용 사례 {#use-cases}

마케터는 [!DNL Adobe Experience Platform]에 작성된 세그먼트를 사용하여 모바일 참여 대상의 사용자를 타깃팅하려고 합니다. 또한 세그먼트와 프로필이 [!DNL Adobe Experience Platform]에서 업데이트되는 즉시 [!DNL Adobe Experience Platform] 프로필의 속성을 기반으로 개인화된 경험을 전달하려고 합니다.

## 지원되는 ID {#supported-identities}

[!DNL Braze] 은 아래 표에 설명된 id의 활성화를 지원합니다.

| Target ID | 설명 | 고려 사항 |
|---|---|---|
| external_id | 모든 ID의 매핑을 지원하는 사용자 지정 [!DNL Braze] 식별자입니다. | [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation)에 매핑하는 한 [identity](../../../identity-service/namespaces.md)를 [!DNL Braze] 대상에 보낼 수 있습니다. |

## 내보내기 유형 {#export-type}

**[!DNL Profile-based]** - 원하는 스키마 필드와 함께 세그먼트의 모든 멤버를 내보냅니다(예: 필드 매핑에 따라 이메일 주소, 전화번호, 성) 및/또는 id를 지정합니다.
[!DNL Adobe Experience Platform] 세그먼트는 속성  [!DNL Braze] 아래에 로  `AdobeExperiencePlatformSegments` 내보내집니다.

## 대상에 연결 {#connect}

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오.

### 연결 매개 변수 {#parameters}

[이 대상을 설정할 때 다음 정보를 제공해야 합니다.](../../ui/connect-destination.md)

* **[!UICONTROL 계정 토큰]** 브레이징: 이게 당신  [!DNL Braze] [!DNL API] 키예요 여기서 [!DNL API] 키를 가져오는 방법에 대한 자세한 지침은 다음과 같습니다. [REST API 키 개요](https://www.braze.com/docs/api/api_key/).
* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 이름을 입력합니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명을 입력합니다.
* **[!UICONTROL 끝점 인스턴스]**: 사용해야  [!DNL Braze] 하는 엔드포인트 인스턴스를 담당자에게 문의하십시오.

## 세그먼트를 이 대상에 활성화 {#activate}

대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침은 [스트리밍 세그먼트 내보내기 대상으로 대상 활성화](../../ui/activate-segment-streaming-destinations.md)를 참조하십시오.

## 매핑 고려 사항 {#mapping-considerations}

대상 데이터를 [!DNL Adobe Experience Platform]에서 [!DNL Braze] 대상으로 올바르게 전송하려면 필드 매핑 단계를 진행해야 합니다.

매핑은 [!DNL Platform] 계정의 [!DNL Experience Data Model] (XDM) 스키마 필드와 대상 대상의 해당 단축키 필드 간에 링크를 만드는 작업으로 이루어집니다.

XDM 필드를 [!DNL Braze] 대상 필드에 올바르게 매핑하려면 다음 단계를 수행합니다.

[!UICONTROL 매핑] 단계에서 **[!UICONTROL 새 매핑 추가]**&#x200B;를 클릭합니다.

![대상 추가 매핑 확장](../../assets/catalog/mobile-engagement/braze/mapping.png)

[!UICONTROL 소스 필드] 섹션에서 빈 필드 옆에 있는 화살표 단추를 클릭합니다.

![대상 소스 매핑 브레이징](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

[!UICONTROL 소스 필드 선택] 창에서 두 가지 XDM 필드 범주 중에서 선택할 수 있습니다.
* [!UICONTROL 속성 선택]: XDM 스키마의 특정 필드를 속성에 매핑하려면 이 옵션을  [!DNL Braze] 사용합니다.

![대상 매핑 소스 특성 브레이징](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL ID 네임스페이스를 선택합니다]. 이 옵션을 사용하여  [!DNL Platform] ID 네임스페이스를 네임스페이스에  [!DNL Braze] 매핑합니다.

![대상 매핑 소스 네임스페이스 브레이징](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

소스 필드를 선택한 다음 **[!UICONTROL 선택]**&#x200B;을 클릭합니다.

[!UICONTROL Target 필드] 섹션에서 필드 오른쪽의 매핑 아이콘을 클릭합니다.

![대상 대상 매핑 브레이징](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

[!UICONTROL 대상 필드 선택] 창에서 다음 세 가지 대상 필드 범주 중에서 선택할 수 있습니다.
* [!UICONTROL 속성 선택]: 이 옵션을 사용하여 XDM 속성을 표준 속성에  [!DNL Braze] 매핑합니다.
* [!UICONTROL ID 네임스페이스를 선택합니다]. 이 옵션을 사용하여 ID 네임스페이스 [!DNL Platform] 를 ID 네임스페이스에  [!DNL Braze] 매핑합니다.
* [!UICONTROL 사용자 지정 속성] 선택: 이 옵션을 사용하여 XDM 속성을  [!DNL Braze] 계정에서 정의한 사용자 지정 속성에  [!DNL Braze] 매핑합니다.
* 이 옵션을 사용하여 기존 XDM 속성의 이름을 [!DNL Braze]으로 바꿀 수도 있습니다. 예를 들어 `lastName` XDM 속성을 [!DNL Braze]의 사용자 지정 `Last_Name` 속성에 매핑하면 [!DNL Braze]에 `Last_Name` 속성이 아직 없는 경우 만들고 `lastName` XDM 속성을 이 속성에 매핑합니다.

![대상 대상 매핑 필드 이해](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

대상 필드를 선택한 다음 **[!UICONTROL 선택]**&#x200B;을 클릭합니다.

이제 목록에 필드 매핑이 표시됩니다.

![대상 매핑 확장 완료](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

매핑을 더 추가하려면 이전 단계를 반복합니다.

## 매핑 예 {#mapping-example}

XDM 프로필 스키마 및 [!DNL Braze] 인스턴스에 다음 속성 및 ID가 포함되어 있다고 가정합니다.

|  | XDM 프로필 스키마 | [!DNL Braze] 인스턴스 |
|---|---|---|
| 속성 | <ul><li>person.name.firstName</code></li><li>person.name.lastName</code></li><li>mobilePhone.number</code></li></ul> | <ul><li>FirstName</code></li><li>LastName</code></li><li>PhoneNumber</code></li></ul> |
| ID | <ul><li>이메일</code></li><li>Google 광고 ID(GAID)</code></li><li>광고주용 Apple ID(IDFA)</code></li></ul> | <ul><li>external_id</code></li></ul> |

올바른 매핑은 다음과 같습니다.

![브레이징 대상 매핑 예](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## 내보낸 데이터 {#exported-data}

데이터를 [!DNL Braze] 대상으로 성공적으로 내보냈는지 확인하려면 [!DNL Braze] 계정을 확인하십시오. [!DNL Adobe Experience Platform] 세그먼트는 속성  [!DNL Braze] 아래에 로  `AdobeExperiencePlatformSegments` 내보내집니다.

## 데이터 사용 및 거버넌스 {#data-usage-governance}

모든 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](../../../data-governance/home.md)를 참조하십시오.
