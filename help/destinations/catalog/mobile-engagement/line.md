---
keywords: 모바일;모바일 참여 대상;LINE;LINE 모바일 참여 대상
title: LINE 연결
description: LINE 대상을 사용하면 Platform 대상자에 프로필을 추가하고 연결된 사용자에게 개인화된 경험을 전달할 수 있습니다.
last-substantial-update: 2022-11-08T00:00:00Z
exl-id: 9981798a-61f2-4a09-9a33-57e63eb36d43
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1190'
ht-degree: 2%

---

# [!DNL LINE] 연결

## 개요 {#overview}

[[!DNL LINE]](https://line.me/en/)은(는) 사람, 서비스 및 정보를 연결하는 인기 있는 커뮤니케이션 플랫폼으로 채팅 앱에서 엔터테인먼트, 소셜 및 일상적인 활동을 위한 허브로 성장했습니다.

이 [!DNL Adobe Experience Platform] [대상](/help/destinations/home.md)은(는) [[!DNL LINE] 메시징 API](https://developers.line.biz/en/reference/messaging-api/)를 활용합니다. Experience Platform 대상의 프로필을 비즈니스 요구 사항에 맞게 [!DNL LINE] 내의 연결로 활성화할 수 있습니다.

[!DNL LINE]은(는) 전달자 토큰을 인증 메커니즘으로 사용하여 [!DNL LINE] 메시징 API와 통신합니다. [!DNL LINE] 인스턴스에 대한 인증 지침은 [대상에 대한 인증](#authenticate) 섹션 아래에 나와 있습니다.

## 사용 사례 {#use-cases}

마케터는 [!DNL Adobe Experience Platform]에 내장된 대상을 사용하여 모바일 참여 대상에서 사용자를 타깃팅할 수 있습니다. 또한 대상자와 프로필이 [!DNL Adobe Experience Platform]에서 업데이트되는 즉시 [!DNL Adobe Experience Platform] 프로필의 특성을 기반으로 개인화된 경험을 제공할 수 있습니다.

## 전제 조건 {#prerequisites}

### [!DNL LINE]개 필수 구성 요소 {#prerequisites-destination}

플랫폼에서 [!DNL LINE] 계정으로 데이터를 내보내려면 [!DNL LINE]의 다음 필수 구성 요소를 참고하십시오.

#### [!DNL LINE] 계정이 있어야 합니다. {#prerequisites-account}

아직 계정이 없는 경우 [!DNL LINE] 계정을 등록하고 만들어야 합니다. 계정을 만들려면 다음 작업을 수행하십시오.

1. [!DNL LINE] [계정 로그인](https://account.line.biz/login?redirectUri=https%3A%2F%2Fmanager.line.biz%2F) 페이지로 이동
2. **[!UICONTROL 계정 만들기]**&#x200B;를 선택합니다.

#### [!DNL LINE] 개발자 콘솔에서 [!DNL LINE channel access token (long-lived)] 수집 {#gather-credentials}

플랫폼에서 [!DNL LINE] 리소스에 액세스할 수 있도록 하려면 원하는 [!DNL LINE] *메시징 API* 채널의 *[!DNL Channel access token (long-lived)]*&#x200B;이(가) 필요합니다.

1. [!DNL LINE] 계정으로 [[!DNL LINE] 개발자 콘솔](https://developers.line.biz/console)에 로그인합니다.
1. 그런 다음 *[!DNL Providers]* 목록에 액세스한 다음 관심 *[!DNL Provider]*&#x200B;을(를) 선택하고 마지막으로 *메시징 API* 채널을 선택하여 해당 설정에 액세스합니다. 개발자 콘솔에 처음 액세스하는 경우 [[!DNL LINE] 설명서](https://developers.line.biz/en/docs/messaging-api/getting-started/)를 따라 공급자를 만드는 데 필요한 단계를 완료하십시오.
1. 마지막으로 ***[!DNL Channel access token]*** 섹션으로 이동하여 [대상에 인증](#authenticate) 단계 내에 필요한 ***[!DNL Channel access token (long-lived)]*** 값을 복사합니다.

| 자격 증명 | 설명 | 예 |
| --- | --- | --- |
| `[!DNL Channel access token (long-lived)]` | 내 [!DNL LINE Channel access token (long-lived)]. | `aaa2112XSMWqLXR7..........nyilFU=` |

[!DNL LINE] 개발자 콘솔을 통해 채널을 만들거나 기존 [!DNL LINE] 계정에 채널을 추가하는 방법에 대한 지침은 [[!DNL LINE] 설명서](https://developers.line.biz/en/docs/messaging-api/getting-started/)를 참조하세요.

## 지원되는 ID {#supported-identities}

[!DNL LINE]은(는) 아래 표에 설명된 ID 업데이트 및 내보내기를 지원합니다. [ID](/help/identity-service/features/namespaces.md)에 대해 자세히 알아보세요.

| 대상 ID | 설명 |
|---|---|
| 광고주용 ID(IFA) | 소스 ID가 IFA *(광고주용 Apple ID)* 또는 GAID *(Google Advertising ID) 네임스페이스인 경우 광고주(IFA) 대상 ID를 선택합니다. |
| LINE 사용자 ID | 소스 ID가 LINE 사용자 ID인 경우 UserID 대상 ID를 선택합니다. |

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | [!DNL LINE] 대상에 사용된 식별자(이름, 전화번호 또는 기타)를 사용하여 대상자의 모든 구성원을 내보내고 있습니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
>
>대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

**[!UICONTROL 대상]** > **[!UICONTROL 카탈로그]** 내에서 [!DNL LINE] 검색 또는 **[!UICONTROL Mobile 참여]** 범주 아래에서 찾을 수 있습니다.

### 대상으로 인증 {#authenticate}

대상에 인증하려면 **[!UICONTROL 대상에 연결]**을 선택하세요.
인증 방법을 보여 주는 ![플랫폼 UI 스크린샷입니다.](../../assets/catalog/mobile-engagement/line/authenticate-destination.png)

아래의 필수 필드를 입력하십시오.
* **[!UICONTROL 전달자 토큰]**: [!DNL LINE] 개발자 콘솔의 [!DNL LINE Channel access token (long-lived)]. [자격 증명 수집](#gather-credentials) 섹션을 참조하십시오.

제공된 세부 정보가 유효하면 UI에 녹색 확인 표시와 함께 **[!UICONTROL 연결됨]** 상태가 표시됩니다. 그런 다음 다음 다음 단계로 진행할 수 있습니다.

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.
![대상 세부 정보를 표시하는 플랫폼 UI 스크린샷입니다.](../../assets/catalog/mobile-engagement/line/destination-details.png)

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 대상 유형]**: 내보내려는 ID가 *ID for Advertisers(IFA)* 유형인 경우 **[!UICONTROL ID for Advertisers(IFA)]**&#x200B;을(를) 선택합니다. 내보내려는 ID가 *LINE 사용자 ID* 유형인 경우 **[!UICONTROL LINE 사용자 ID]**&#x200B;을(를) 선택하십시오. ID 유형에 대한 자세한 내용은 [지원되는 ID](#supported-identities) 섹션을 참조하십시오.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 모두 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

이 대상으로 대상을 활성화하는 방법에 대한 지침은 [프로필 및 대상을 스트리밍 대상 내보내기 대상으로 활성화](/help/destinations/ui/activate-segment-streaming-destinations.md)를 참조하십시오.

### 속성 및 ID 매핑 {#map}

대상 데이터를 Adobe Experience Platform에서 [!DNL LINE] 대상으로 올바르게 보내려면 필드 매핑 단계를 거쳐야합니다. 매핑은 Platform 계정의 XDM(Experience Data Model) 스키마 필드와 대상 대상의 해당 필드 간에 링크를 만드는 것으로 구성됩니다. XDM 필드를 [!DNL LINE] 대상 필드에 올바르게 매핑하려면 다음 단계를 따르십시오.

소스 ID에 따라 다음 대상 ID 네임스페이스를 매핑해야 합니다.
| 대상 ID | Source 필드 | 대상 필드 |
| — | — | — |
| 광고주용 ID(IFA) | `IDFA` 또는 `GAID` | `LineId` |
| LINE 사용자 ID | `UserID` | `LineId` |

대상 ID가 *LINE 사용자 ID*인 경우 다음이 필요합니다.
![대상 ID에 대해 LINE 사용자 ID를 사용할 때 Target 매핑을 보여 주는 Platform UI 스크린샷 예](../../assets/catalog/mobile-engagement/line/mappings-userid.png)

대상 ID가 *IFA(광고주용 ID)*인 경우 다음이 필요합니다.
![대상 ID에 대해 IFA(광고주)용 ID를 사용할 때 Target 매핑을 보여주는 Platform UI 스크린샷 예](../../assets/catalog/mobile-engagement/line/mappings-idfa.png)

## 데이터 내보내기 유효성 검사 {#exported-data}

Experience Platform에서 데이터를 성공적으로 내보내면 [!DNL LINE] 대상이 선택한 대상 이름을 사용하여 [!DNL LINE] 내에 새 대상을 만듭니다.

대상을 올바르게 설정했는지 확인하려면 아래 단계를 수행하십시오.

1. [!DNL LINE]에서 [관리자 콘솔](https://manager.line.biz/)에 로그인합니다.

1. 그런 다음 **[!UICONTROL 데이터 컨트롤]** > **[!UICONTROL 대상]**(으)로 이동하여 **[!UICONTROL 대상 이름]** 열에서 선택한 대상과 일치하는 이름을 확인합니다.

1. 업데이트된 볼륨은 세그먼트 내의 카운트와 일치합니다.

1. 내보낸 ID가 *UserID* 유형인 경우 *Type* 열에서 **[!UICONTROL UserID]**&#x200B;이(가) 언급됩니다. 마찬가지로 내보낸 ID가 *IDFA* 유형인 경우 *Type* 열에 **[!UICONTROL Mobile 광고 ID]**&#x200B;이(가) 언급됩니다.

[!DNL LINE] 내의 예제 설정이 아래에 표시되어 있습니다.
대상 볼륨을 보여 주는 ![LINE UI 스크린샷입니다.](../../assets/catalog/mobile-engagement/line/audience-volume.png)

## 데이터 사용 및 관리 {#data-usage-governance}

데이터를 처리할 때 모든 [!DNL Adobe Experience Platform] 대상이 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](/help/data-governance/home.md)를 참조하십시오.
