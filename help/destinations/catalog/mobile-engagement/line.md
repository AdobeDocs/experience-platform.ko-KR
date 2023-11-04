---
keywords: 모바일;모바일 참여 대상;LINE;LINE 모바일 참여 대상
title: LINE 연결
description: LINE 대상을 사용하면 Platform 대상자에 프로필을 추가하고 연결된 사용자에게 개인화된 경험을 전달할 수 있습니다.
last-substantial-update: 2022-11-08T00:00:00Z
exl-id: 9981798a-61f2-4a09-9a33-57e63eb36d43
source-git-commit: 05e996f9e33e0d8be3d15a9ab3baaaf6d8152b5a
workflow-type: tm+mt
source-wordcount: '1214'
ht-degree: 2%

---

# [!DNL LINE] 연결

## 개요 {#overview}

[[!DNL LINE]](https://line.me/en/) 사람, 서비스, 정보를 연결하는 대중적인 커뮤니케이션 플랫폼으로 채팅 앱에서 엔터테인먼트, 소셜, 일상 활동을 위한 허브로 성장하였다.

이 [!DNL Adobe Experience Platform] [대상](/help/destinations/home.md) 을 활용합니다. [[!DNL LINE] 메시징 API](https://developers.line.biz/en/reference/messaging-api/). Experience Platform 대상의 프로필을 다음 내에서 연결로 활성화할 수 있습니다. [!DNL LINE] 비즈니스 요구 사항 충족

[!DNL LINE] 는 인증 메커니즘으로 전달자 토큰을 사용하여 [!DNL LINE] 메시징 API. 에 대한 인증 지침 [!DNL LINE] 인스턴스는 아래에 더 있습니다. [대상에 인증](#authenticate) 섹션.

## 사용 사례 {#use-cases}

마케터는 내장된 대상을 사용하여 모바일 참여 대상에서 사용자를 타깃팅할 수 있습니다 [!DNL Adobe Experience Platform]. 또한 의 속성을 기반으로 개인화된 경험을 제공할 수 있습니다 [!DNL Adobe Experience Platform] 대상자 및 프로필이 업데이트되는 즉시 프로필 [!DNL Adobe Experience Platform].

## 전제 조건 {#prerequisites}

### [!DNL LINE] 전제 조건 {#prerequisites-destination}

에서 다음 전제 조건을 참고하십시오. [!DNL LINE]: 데이터를 플랫폼에서 로 내보내기 [!DNL LINE] 계정:

#### 다음을 수행해야 합니다. [!DNL LINE] account {#prerequisites-account}

을(를) 등록하고 만들어야 합니다. [!DNL LINE] 계정, 아직 계정이 없는 경우. 계정을 만들려면 다음 작업을 수행하십시오.

1. 다음 위치로 이동 [!DNL LINE] [계정 로그인](https://account.line.biz/login?redirectUri=https%3A%2F%2Fmanager.line.biz%2F) 페이지
2. 선택 **[!UICONTROL 계정 만들기]**.

#### 다음을 수집합니다. [!DNL LINE channel access token (long-lived)] 다음에서 [!DNL LINE] 개발자 콘솔 {#gather-credentials}

Platform의 액세스 허용 [!DNL LINE] 리소스, 다음이 필요합니다. *[!DNL Channel access token (long-lived)]* 원하는 대로 [!DNL LINE] *메시징 API* 채널.

1. 로 로그인 [!DNL LINE] 계정 대상: [[!DNL LINE] 개발자 콘솔](https://developers.line.biz/console).
1. 그런 다음 *[!DNL Providers]* 목록을 만든 다음 *[!DNL Provider]* 관심 있는 항목 및 마지막으로 *메시징 API* 채널 을 통해 설정에 액세스할 수 있습니다. Developer Console에 처음 액세스하는 경우 [[!DNL LINE] 설명서](https://developers.line.biz/en/docs/messaging-api/getting-started/) 공급자를 만드는 데 필요한 단계를 완료합니다.
1. 마지막으로 ***[!DNL Channel access token]*** 섹션 및 복사 ***[!DNL Channel access token (long-lived)]*** 다음 범위 내에 필요한 값: [대상에 인증](#authenticate) 단계.

| 자격 증명 | 설명 | 예 |
| --- | --- | --- |
| `[!DNL Channel access token (long-lived)]` | 사용자 [!DNL LINE Channel access token (long-lived)]. | `aaa2112XSMWqLXR7..........nyilFU=` |

다음을 참조하십시오. [[!DNL LINE] 설명서](https://developers.line.biz/en/docs/messaging-api/getting-started/) 채널 만들기 또는 기존 채널에 채널 추가에 대한 지침 [!DNL LINE] 계정 스루 [!DNL LINE] 개발자 콘솔.

## 지원되는 ID {#supported-identities}

[!DNL LINE] 는 아래 표에 설명된 id 업데이트 및 내보내기를 지원합니다. 자세히 알아보기 [id](/help/identity-service/namespaces.md).

| 대상 ID | 설명 |
|---|---|
| 광고주용 ID(IFA) | 소스 ID가 IFA인 경우 IFA(광고주) 타겟 ID에 대한 ID를 선택합니다 *(광고주용 Apple ID)* 또는 GAID *(Google Advertising ID) 네임스페이스입니다. |
| LINE 사용자 ID | 소스 ID가 LINE 사용자 ID인 경우 UserID 대상 ID를 선택합니다. |

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | 에 사용된 식별자(이름, 전화번호 또는 기타)를 사용하여 대상자의 모든 구성원을 내보냅니다. [!DNL LINE] 대상. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
>
>대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

이 대상에 연결하려면 다음과같이 하십시오. [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

다음 범위 내 **[!UICONTROL 대상]** > **[!UICONTROL 카탈로그]** 검색 대상 [!DNL LINE]. 또는 아래에서 찾을 수 있습니다 **[!UICONTROL 모바일 참여]** 범주.

### 대상으로 인증 {#authenticate}

대상에 인증하려면 다음을 선택합니다. **[!UICONTROL 대상에 연결]**.
![인증 방법을 보여 주는 플랫폼 UI 스크린샷입니다.](../../assets/catalog/mobile-engagement/line/authenticate-destination.png)

아래의 필수 필드를 입력하십시오.
* **[!UICONTROL 전달자 토큰]**: 사용자 [!DNL LINE Channel access token (long-lived)] 다음에서 [!DNL LINE] 개발자 콘솔. 다음을 참조하십시오. [자격 증명 수집](#gather-credentials) 섹션.

제공된 세부 정보가 유효한 경우 UI에 **[!UICONTROL 연결됨]** 녹색 확인 표시가 있는 상태. 그런 다음 다음 다음 단계로 진행할 수 있습니다.

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.
![대상 세부 사항을 보여주는 플랫폼 UI 스크린샷입니다.](../../assets/catalog/mobile-engagement/line/destination-details.png)

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 대상자 유형]**: 선택 **[!UICONTROL 광고주용 ID(IFA)]** 내보내려는 id가 유형인 경우 *광고주용 ID(IFA)*. 선택 **[!UICONTROL LINE 사용자 ID]** 내보내려는 id가 유형인 경우 *LINE 사용자 ID*. 다음을 참조하십시오. [지원되는 ID](#supported-identities) 섹션에 자세히 설명되어 있습니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 다음 안내서를 참조하십시오. [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보를 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.
>* 내보내려면 *id*, 다음이 필요합니다. **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). <br> ![워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다.](/help/destinations/assets/overview/export-identities-to-destination.png "워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다."){width="100" zoomable="yes"}

읽기 [스트리밍 대상자 내보내기 대상으로 프로필 및 대상자 활성화](/help/destinations/ui/activate-segment-streaming-destinations.md) 이 대상에 대한 대상자 활성화에 대한 지침을 참조하십시오.

### 속성 및 ID 매핑 {#map}

대상 데이터를 Adobe Experience Platform에서 로 올바르게 보내려면 [!DNL LINE] 대상, 필드 매핑 단계를 거쳐야 합니다. 매핑은 Platform 계정의 XDM(Experience Data Model) 스키마 필드와 대상 대상의 해당 필드 간에 링크를 만드는 것으로 구성됩니다. XDM 필드를 [!DNL LINE] 대상 필드에서 다음 단계를 수행합니다.

소스 ID에 따라 다음 대상 ID 네임스페이스를 매핑해야 합니다. | Target ID | 소스 필드 | 대상 필드 | | — | — | — | | 광고주용 ID(IFA) | `IDFA` 또는 `GAID` | `LineId` | | LINE 사용자 ID | `UserID` | `LineId` |

대상 ID가 다음과 같은 경우 *LINE 사용자 ID* 다음이 필요합니다.
![타겟 ID에 LINE 사용자 ID를 사용할 때 타겟 매핑을 보여주는 플랫폼 UI 스크린샷 예입니다.](../../assets/catalog/mobile-engagement/line/mappings-userid.png)

대상 ID가 *광고주용 ID(IFA)* 다음이 필요합니다.
![타겟 ID에 IFA(광고주)용 ID를 사용할 때 Target 매핑을 보여주는 플랫폼 UI 스크린샷 예입니다.](../../assets/catalog/mobile-engagement/line/mappings-idfa.png)

## 데이터 내보내기 유효성 검사 {#exported-data}

Experience Platform에서 데이터를 성공적으로 내보내면 [!DNL LINE] 대상 은 내에 새 대상을 만듭니다. [!DNL LINE] 선택한 대상 이름을 사용합니다.

대상을 올바르게 설정했는지 확인하려면 아래 단계를 수행하십시오.

1. 위치 [!DNL LINE]에 로그인합니다. [관리자 콘솔](https://manager.line.biz/).

1. 다음으로 이동 **[!UICONTROL 데이터 컨트롤]** > **[!UICONTROL 대상]** 및 내에서 선택한 대상자와 일치하는 이름을 확인합니다. **[!UICONTROL 대상 이름]** 열.

1. 업데이트된 볼륨은 세그먼트 내의 카운트와 일치합니다.

1. 다음 *유형* 열이 언급됨 **[!UICONTROL 사용자 ID]** 내보낸 id가 유형인 경우 *사용자 ID*. 마찬가지로 *유형* 열이 언급됨 **[!UICONTROL 모바일 광고 ID]** 내보낸 id가 유형인 경우 *IDFA*.

내의 예제 설정 [!DNL LINE] 다음이 표시됩니다.
![대상 볼륨을 보여 주는 LINE UI 스크린샷입니다.](../../assets/catalog/mobile-engagement/line/audience-volume.png)

## 데이터 사용 및 관리 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스 시행, 다음을 참조하십시오. [데이터 거버넌스 개요](/help/data-governance/home.md).
