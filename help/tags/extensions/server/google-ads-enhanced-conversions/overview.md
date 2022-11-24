---
title: Google 광고 향상된 전환 확장
description: Adobe Experience Platform의 이벤트 전달을 위한 Google 광고 향상된 전환 확장에 대해 알아봅니다.
exl-id: 65cdff40-276f-4481-9621-6c6861dbd412
source-git-commit: bfbad3c11df64526627e4ce2d766b527df678bca
workflow-type: tm+mt
source-wordcount: '1314'
ht-degree: 1%

---

# [!DNL Google Ads] 향상된 전환 확장

사용 [!DNL Google Ads] API를 사용하면 [향상된 전환](https://support.google.com/google-ads/answer/9888656) 전환 조정 형태로 자사 고객 데이터를 전송합니다. Google은 이 추가 데이터를 사용하여 광고 상호 작용에 의해 제어되는 온라인 전환의 보고를 개선합니다.

다음 [[!DNL Google Ads] 향상된 전환 이벤트 전달 확장](https://exchange.adobe.com/apps/ec/108630/google-ads-enhanced-conversions) (이하 &quot;다음&quot;이라 한다) [!DNL Enhanced Conversions] 확장)은 for the [!DNL Google Ads] API.

>[!IMPORTANT]
>
>향상된 전환은 구독, 등록 및 구매와 같이 고객 데이터가 있는 전환 유형에만 작동합니다. 다음의 경우 필요하므로 고객 데이터 중 하나 이상을 사용할 수 있어야 합니다 [전환 작업 구성](#conversion-action-event-forwarding) 이벤트 전달 규칙:
>
>* 이메일 주소(기본 설정)
>* 이름 및 집 주소(주소, 도시, 주/지역 및 우편 번호)
>* 전화 번호(위의 다른 두 가지 정보 중 하나에 추가로 제공되어야 함)


## 구현 개요

향상된 전환은 [!DNL Google Ads] 클라이언트 장치(일반적으로 웹 사이트)에서 발생한 변환에 자사 데이터를 추가하는 API입니다. 즉, 향상된 전환을 구현하는 두 가지 단계가 있습니다.

1. 클라이언트에서 전환을 보냅니다.
1. 이벤트 전달을 사용하여 클라이언트에서 보낸 변환 데이터를 향상시키는 추가 자사 데이터를 보냅니다.

>[!TIP]
>
>클라이언트측 전환 이벤트를 이벤트 전달에서 보낸 자사 데이터와 연결하려면 `transaction_ID` 는 두 호출 모두에서 동일해야 합니다. 각 서비스에 대해 이 값을 제공해야 하는 위치에 대한 자세한 내용은 [태그](#conversion-action-tags) 및 [이벤트 전달](#conversion-action-event-forwarding)각각 입니다.

전환 이벤트 전송에는 클라이언트측 및 서버측 구현이 모두 포함되므로 이 문서에서는 클라이언트측 설정을 위한 사전 요구 절차를 다룹니다 [[!DNL Google Global Site Tag] (gtag) 확장](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag) 그리고 [!DNL Enhanced Conversions] 이벤트 전달을 위한 확장.

다음 비디오에서는 를 소개합니다 [!DNL Enhanced Conversions] 확장을 살펴보고 다음 높은 수준에서 구현 단계를 안내합니다.

>[!VIDEO](https://video.tv.adobe.com/v/3411365?quality=12&learn=on)

## 태그를 사용하여 전환 보내기

웹 사이트에서 전환 이벤트를 보내려면 [!DNL Google Global Site Tag] (gtag)를 배포해야 합니다. 을 구성 및 설치하여 태그를 사용하여 이 작업을 수행할 수 있습니다 [!DNL Google Global Site Tag] (gtag) 확장.

### 구성 및 설치 [!DNL Google Global Site Tag] 확장

로 이동합니다 [!UICONTROL 데이터 수집] UI 또는 Experience Platform UI를 선택하고 **[!UICONTROL 태그]** 을 클릭합니다. 확장을 설치할 태그 속성을 선택하고 을 선택합니다 **[!UICONTROL 확장]** 을 클릭합니다. 아래에 **[!UICONTROL 카탈로그]** 탭에서 를 찾습니다 [!UICONTROL Google 전역 사이트 태그(gtag)] 확장을 선택하고 **[!UICONTROL 설치]**.

![다음 [!UICONTROL Google 전역 사이트 태그(gtag)] 확장 아래에서 선택 중 [!UICONTROL 확장] 에서 보기 [!UICONTROL 데이터 수집] UI.](../../../images/extensions/server/google-ads-enhanced-conversions/install-gtag-extension.png)

설치 대화 상자가 나타납니다. 여기에서 을 선택합니다. **[!UICONTROL 계정 추가]** 및 메시지가 표시되면 다음 값을 제공합니다.

| 계정 속성 | 설명 |
| --- | --- |
| 계정 이름 | 계정의 고유 이름입니다. 이 이름은 태그 UI 내에서만 사용됩니다. |
| 계정 ID | 사용자 [!DNL Google Ads] 계정 ID. 이 값을 찾으려면 [!DNL Google Ads] 다음 위치로 이동합니다. **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Install the Tag yourself]**. 계정 ID 문자열은 `AW-` 또는 `d`. |
| 제품 | 선택 **[!UICONTROL Google 광고(AdWords)]**. |

{style=&quot;table-layout:auto&quot;}

완료되면 을 선택합니다 **[!UICONTROL 계정 추가]**&#x200B;를 선택하고 을 선택합니다. **[!UICONTROL 저장]**.

### 전환 보내기 작업 추가 {#conversion-action-tags}

확장을 설치한 후에 태그 규칙에 전환 작업 포함을 시작할 수 있습니다. 개선할 변환을 수신하는 규칙을 만들거나 편집할 때 을 선택합니다 **[!UICONTROL 추가]** 아래에 [!UICONTROL 작업]. 다음 대화 상자에서 다음을 선택합니다 **[!UICONTROL Google 전역 사이트 태그(gtag)]** 에서 [!UICONTROL 확장] 드롭다운을 선택한 다음 **[!UICONTROL 이벤트 보내기]** 아래에 [!UICONTROL 작업 유형].

![다음 [!UICONTROL 이벤트 보내기] 규칙 편집 워크플로우의 작업 구성 보기 내에서 선택 중인 작업 유형입니다.](../../../images/extensions/server/google-ads-enhanced-conversions/select-client-action.png)

추가 컨트롤을 사용하면 [!DNL gtag] 이벤트. 최소한 다음 필드를 입력해야 합니다.

1. **[!UICONTROL 이벤트 이름(작업)]**: Enter 키 `conversion` 를 값으로 채우는 방법을 설명합니다.
1. 키가 인 새 필드 추가 `transaction_id` 그리고 값은 [데이터 요소](../../../ui/managing-resources/data-elements.md) 여기에는 다음 항목이 포함됩니다 [거래 ID](https://support.google.com/google-ads/answer/6386790) 값.
1. **[!UICONTROL 변환 레이블]**: 에서 적절한 전환 레이블을 입력합니다 [!DNL Google Ads] 계정이 필요합니다. 이 값을 찾으려면 Google Ads에 로그인하고 **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Use Google Tag Manager]**. 변환 레이블은 [!DNL Instructions].
   >[!IMPORTANT]
   >
   >가 페이지의 태그 설정 영역에 있는 동안 [!DNL Google Ads] account에서 향상된 전환이 활성화되었는지 확인합니다. 이렇게 하려면 Terms of Service를 검토하고 수락한 다음 을 선택합니다. **[!DNL Turn on enhanced conversions]** 및 **[!DNL API]** 를 구현 메서드로 사용할 수 있습니다.

작업을 구성한 후 을 선택합니다 **[!UICONTROL 변경 내용 유지]** 를 눌러 규칙 구성에 작업을 추가합니다. 규칙에 만족하면 을 선택합니다 **[!UICONTROL 라이브러리에 저장]**.

마지막으로 새 [빌드](../../../ui/publishing/builds.md) 를 클릭하여 라이브러리에 대한 변경 사항을 활성화합니다.

## 이벤트 전달을 사용하여 자사 데이터 보내기

클라이언트 측에서 전환 이벤트를 전송할 수 있으면 를 사용하여 이러한 전환을 향상시킬 수 있습니다. [!DNL Enhanced Conversions] 이벤트 전달 확장.

### Google OAuth 2 암호 및 데이터 요소 만들기 {#create-secret-data-element}

확장을 구성하기 전에 인증을 받으려면 이벤트 전달에 액세스 토큰을 만들어야 합니다 [!DNL Google Ads] API.

다음 안내서를 참조하십시오. [이벤트 전달 암호 만들기](../../../ui/event-forwarding/secrets.md) 자세한 단계. 다음을 선택해야 합니다 **[!UICONTROL Google OAuth 2]** 비밀 종류로 화면의 지시를 계속 따르고 Google 계정 프로필을 선택하라는 메시지가 표시되면 구성하는 전환 작업에 액세스할 수 있는 계정을 선택합니다.

비밀이 만들어지면 [새 데이터 요소 만들기](../../../ui/managing-resources/data-elements.md#create-a-data-element) 을(를) 선택합니다. **[!UICONTROL 비밀]** 를 반환합니다. 각 환경에 적합한 Google OAuth 2 암호를 선택하고 을(를) 선택합니다 **[!UICONTROL 라이브러리에 저장]**.

### 구성 및 설치 [!DNL Enhanced Conversions] 확장 {#install-enhanced-conversions}

를 찾습니다. [!UICONTROL Google 광고 향상된 전환] 이벤트 전달 카탈로그의 확장을 선택하고 을(를) 선택합니다. **[!UICONTROL 설치]**.

![다음 [!UICONTROL Google 광고 향상된 전환] 확장 아래에서 선택 중 [!UICONTROL 확장] 에서 보기 [!UICONTROL 데이터 수집] UI.](../../../images/extensions/server/google-ads-enhanced-conversions/install-enhanced-conversions.png)

확장을 구성하려면 다음 두 개의 필수 필드를 채워야 합니다.

1. **[!UICONTROL 고객 ID]**: 를 고유하게 식별하는 ID입니다 [!DNL Google Ads] 계정이 필요합니다. 이 값을 찾으려면 [!DNL Google Ads] 및 **[!DNL Help]** > **[!DNL Customer ID]**.
1. **[!UICONTROL 액세스 토큰 데이터 요소]**: 데이터 요소 아이콘(![데이터 요소 아이콘](../../../images/extensions/server/google-ads-enhanced-conversions/data-element-icon.png))을 클릭하고 원하는 Google OAuth 2 암호 데이터 요소를 선택합니다 [이전 단계에서 구성](#create-secret-data-element) 메뉴 아래의 제품에서 사용할 수 있습니다.

완료되면 을 선택합니다 **[!UICONTROL 저장]** 확장을 설치하려면 다음을 수행하십시오.

### 추가 [!UICONTROL 전환 보내기] 규칙에 대한 작업 {#conversion-action-event-forwarding}

확장이 설치되면 다음을 포함할 수 있습니다 [!UICONTROL 전환 보내기] 이벤트 전달 규칙의 작업입니다. 개선할 변환을 수신하는 규칙을 만들거나 편집할 때 을 선택합니다 **[!UICONTROL 추가]** 아래에 [!UICONTROL 작업]. 다음 대화 상자에서 다음을 선택합니다 **[!UICONTROL Google 광고 향상된 전환]** 에서 [!UICONTROL 확장] 드롭다운을 선택한 다음 **[!UICONTROL 전환 보내기]** 아래에 [!UICONTROL 작업 유형].

![다음 [!UICONTROL 전환 보내기] 규칙 편집 워크플로우의 작업 구성 보기 내에서 선택 중인 작업 유형입니다.](../../../images/extensions/server/google-ads-enhanced-conversions/select-server-action.png)

전환을 구성할 수 있는 새 컨트롤이 오른쪽 패널에 나타납니다. 최소한 다음 필드를 완료해야 합니다.

**변환 정보**

| 입력 | 설명 |
| --- | --- |
| 고객 ID | 사용자 [!DNL Google Ads] 고객 ID. 기본값은 [확장 설치](#install-enhanced-conversions). |
| 전환 ID 또는 전환 레이블 | 에서 가져온 추적 값 [!DNL Google Ads] 전환 추적을 설정할 때. 값은 다음으로 시작 `AW-`.<br><br>이러한 값을 찾는 방법에 대한 자세한 내용은 [[!DNL Google Ads] 설명서](https://support.google.com/tagmanager/answer/6105160?hl=en). |
| 거래 ID | 동일한 거래 ID 값이 있는 데이터 요소를 선택합니다. [클라이언트 측에서 전송됨](#conversion-action-tags) 사용 [!DNL Google Global Site Tag] 확장. |

**사용자 식별**

* 세 사용자 식별자 중 하나 이상이 포함되어야 합니다.
   * 이메일
   * 전화 번호
   * 전체 주소

>[!TIP]
>
>사용자 ID 데이터는 Google에 전송되기 전에 해시해야 합니다. 이벤트 전달에서 데이터를 받을 때 데이터가 해시되지 않으면 을(를) 선택합니다. **[!UICONTROL 정규화 및 해시]** 주어진 필드를 토글하여 확장에 값을 해시하도록 지시합니다.
>
>![다음 [!UICONTROL 정규화 및 해시] 에 대해 활성화된 전환 [!UICONTROL 이메일] 내 입력 [!UICONTROL 전환 보내기] 작업 구성 양식입니다.](../../../images/extensions/server/google-ads-enhanced-conversions/hash-user-id-values.png)

완료되면 을 선택합니다 **[!UICONTROL 변경 내용 유지]** 를 눌러 규칙 구성에 작업을 추가합니다. 규칙에 만족하면 을 선택합니다 **[!UICONTROL 라이브러리에 저장]**.

마지막으로 새 이벤트 전달 게시 [빌드](../../../ui/publishing/builds.md) 를 클릭하여 라이브러리에 대한 변경 사항을 활성화합니다.

## 다음 단계

이 안내서에서는 전환 이벤트를 [!DNL Google Ads] 사용 [!DNL Enhanced Conversions] 이벤트 전달 확장. Experience Platform의 이벤트 전달 기능에 대한 자세한 내용은 [이벤트 전달 개요](../../../ui/event-forwarding/overview.md).
