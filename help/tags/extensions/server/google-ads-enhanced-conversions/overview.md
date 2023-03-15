---
title: Google Ads Enhanced Conversions 확장
description: Adobe Experience Platform의 이벤트 전달을 위한 Google Ads Enhanced Conversion 확장에 대해 알아봅니다.
exl-id: 65cdff40-276f-4481-9621-6c6861dbd412
source-git-commit: bfbad3c11df64526627e4ce2d766b527df678bca
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 1%

---

# [!DNL Google Ads] 향상된 전환 확장

사용 [!DNL Google Ads] API, 다음을 활용할 수 있습니다. [향상된 전환](https://support.google.com/google-ads/answer/9888656) 전환 조정 형식으로 자사 고객 데이터를 전송합니다. Google은 이 추가 데이터를 사용하여 광고 상호 작용에 따른 온라인 전환에 대한 보고를 향상시킵니다.

다음 [[!DNL Google Ads] 향상된 전환 이벤트 전달 확장](https://exchange.adobe.com/apps/ec/108630/google-ads-enhanced-conversions) (따라서 [!DNL Enhanced Conversions] 확장)은에 대한 향상된 변환을 쉽게 구현할 수 있는 사용자 친화적인 템플릿을 제공합니다. [!DNL Google Ads] API.

>[!IMPORTANT]
>
>향상된 전환은 구독, 등록 및 구매와 같이 고객 데이터가 있는 전환 유형에만 작동합니다. 다음 고객 데이터 조각은 다음과 같은 경우에 필요하므로 하나 이상 사용할 수 있어야 합니다. [전환 작업 구성](#conversion-action-event-forwarding) 이벤트 전달 규칙의 경우:
>
>* 이메일 주소(기본 설정)
>* 이름 및 집 주소(주소, 구/군/시, 시/도 및 우편 번호)
>* 전화번호(위의 다른 두 정보 중 하나와 함께 제공해야 함)


## 구현 개요

향상된 전환은 [!DNL Google Ads] 클라이언트 장치(일반적으로 웹 사이트)에서 발생한 변환에 자사 데이터를 추가하기 위한 API입니다. 즉, 향상된 전환을 구현하는 두 가지 단계가 있습니다.

1. 클라이언트에서 전환을 보냅니다.
1. 이벤트 전달을 사용하여 클라이언트에서 보낸 전환 데이터를 향상시키는 추가 자사 데이터를 보냅니다.

>[!TIP]
>
>클라이언트측 전환 이벤트를 이벤트 전달에서 전송된 자사 데이터와 연결하려면 `transaction_ID` 두 호출에서 동일해야 합니다. 각 서비스에 대해 이 값을 제공해야 하는 위치에 대한 자세한 내용은 전환 작업 구성에 대한 섹션을 참조하십시오 [태그](#conversion-action-tags) 및 [이벤트 전달](#conversion-action-event-forwarding), 각각

전환 이벤트 전송에는 클라이언트측과 서버측 구현이 모두 포함되므로, 이 문서에서는 클라이언트측 설정을 위한 사전 요구 사항을 다룹니다 [[!DNL Google Global Site Tag] (gtag) 확장](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag) 및 [!DNL Enhanced Conversions] 이벤트 전달을 위한 확장입니다.

다음 비디오에서는 [!DNL Enhanced Conversions] 확장 및 는 높은 수준에서 구현 단계를 안내합니다.

>[!VIDEO](https://video.tv.adobe.com/v/3411365?quality=12&learn=on)

## 태그를 사용하여 변환 보내기

웹 사이트에서 전환 이벤트를 보내려면 [!DNL Google Global Site Tag] (gtag)를 배포해야 합니다. 를 구성하고 설치하여 태그를 사용하여 이를 수행할 수 있습니다. [!DNL Google Global Site Tag] (gtag) 확장.

### 구성 및 설치 [!DNL Google Global Site Tag] 확장

다음 위치로 이동 [!UICONTROL 데이터 수집] UI 또는 Experience Platform UI 및 선택 **[!UICONTROL 태그]** 왼쪽 탐색. 확장을 설치할 태그 속성을 선택한 다음 를 선택합니다 **[!UICONTROL 확장]** 왼쪽 탐색. 아래 **[!UICONTROL 카탈로그]** 탭에서 다음을 찾습니다. [!UICONTROL Google 글로벌 사이트 태그(gtag)] 확장 및 선택 **[!UICONTROL 설치]**.

![다음 [!UICONTROL Google 글로벌 사이트 태그(gtag)] 확장 프로그램 선택 중 [!UICONTROL 확장] 다음에서 보기 [!UICONTROL 데이터 수집] UI.](../../../images/extensions/server/google-ads-enhanced-conversions/install-gtag-extension.png)

설치 대화 상자가 나타납니다. 여기에서 다음을 선택합니다. **[!UICONTROL 계정 추가]** 메시지가 표시되면 다음 값을 제공합니다.

| 계정 속성 | 설명 |
| --- | --- |
| 계정 이름 | 계정에 대한 고유한 이름. 이 이름은 태그 UI 내에서만 사용됩니다. |
| 계정 ID | 사용자 [!DNL Google Ads] 계정 ID. 이 값을 찾으려면 로그인합니다. [!DNL Google Ads] 다음 위치로 이동합니다. **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Install the Tag yourself]**. 계정 ID 문자열은 다음으로 시작하는 코드 조각 창에서 찾을 수 있습니다. `AW-` 또는 `d`. |
| 제품 | 선택 **[!UICONTROL Google 광고(AdWords)]**. |

{style="table-layout:auto"}

완료되면 다음을 선택합니다. **[!UICONTROL 계정 추가]**&#x200B;을 선택한 다음 을 선택합니다. **[!UICONTROL 저장]**.

### 전환 보내기 작업 추가 {#conversion-action-tags}

확장을 설치한 후 태그 규칙에 전환 작업을 포함할 수 있습니다. 개선하려는 전환을 수신하는 규칙을 만들거나 편집할 때 다음을 선택합니다. **[!UICONTROL 추가]** 아래에 [!UICONTROL 작업]. 다음 대화 상자에서 을 선택합니다. **[!UICONTROL Google 글로벌 사이트 태그(gtag)]** 다음에서 [!UICONTROL 확장] 드롭다운을 선택한 다음 을 선택합니다. **[!UICONTROL 이벤트 보내기]** 아래에 [!UICONTROL 작업 유형].

![다음 [!UICONTROL 이벤트 보내기] 규칙 편집 워크플로의 작업 구성 보기에서 작업 유형을 선택하고 있습니다.](../../../images/extensions/server/google-ads-enhanced-conversions/select-client-action.png)

을 구성할 수 있는 추가 컨트롤이 나타납니다. [!DNL gtag] 이벤트. 최소한 다음 필드를 작성해야 합니다.

1. **[!UICONTROL 이벤트 이름(작업)]**: 입력 `conversion` 을 값으로 추가합니다.
1. 키가 있는 새 필드 추가 `transaction_id` 및 값은 입니다. [데이터 요소](../../../ui/managing-resources/data-elements.md) 다음을 포함하는 [거래 ID](https://support.google.com/google-ads/answer/6386790) 값.
1. **[!UICONTROL 전환 레이블]**: 다음에서 적절한 전환 레이블을 입력합니다. [!DNL Google Ads] 계정입니다. 이 값을 찾으려면 Google Ads에 로그인하여 **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Use Google Tag Manager]**. 전환 레이블은 다음에서 찾을 수 있습니다. [!DNL Instructions].
   >[!IMPORTANT]
   >
   >의 태그 설정 영역에 있는 동안 [!DNL Google Ads] 계정, 향상된 전환이 활성화되어 있는지 확인합니다. 이렇게 하려면 서비스 약관을 검토하고 동의한 다음 을 선택합니다. **[!DNL Turn on enhanced conversions]** 및 **[!DNL API]** 를 구현 방법으로 사용하십시오.

작업을 구성한 후 다음을 선택합니다. **[!UICONTROL 변경 내용 유지]** 작업을 규칙 구성에 추가합니다. 규칙에 만족하면 다음을 선택합니다. **[!UICONTROL 라이브러리에 저장]**.

마지막으로, 새 항목 게시 [빌드](../../../ui/publishing/builds.md) 라이브러리에 대한 변경 사항을 활성화합니다.

## 이벤트 전달을 사용하여 자사 데이터 보내기

클라이언트측에서 전환 이벤트를 보낼 수 있으면 [!DNL Enhanced Conversions] 이벤트 전달 확장.

### Google OAuth 2 암호 및 데이터 요소 만들기 {#create-secret-data-element}

확장을 구성하기 전에 이벤트 전달 시 인증할 액세스 토큰을 생성해야 합니다. [!DNL Google Ads] API.

다음 안내서를 참조하십시오 [이벤트 전달 암호 만들기](../../../ui/event-forwarding/secrets.md) 을 참조하십시오. 다음을 선택했는지 확인합니다. **[!UICONTROL Google OAuth 2]** 암호 유형으로 사용해야 합니다. 계속해서 화면의 지시를 따르고 Google 계정 프로필을 선택하라는 메시지가 표시되면 구성 중인 전환 작업에 액세스할 수 있는 계정을 선택합니다.

비밀이 만들어지면 [새 데이터 요소 만들기](../../../ui/managing-resources/data-elements.md#create-a-data-element) 및 선택 **[!UICONTROL 암호]** : 데이터 요소 유형입니다. 각 환경에 적합한 Google OAuth 2 암호를 선택하고 **[!UICONTROL 라이브러리에 저장]**.

### 구성 및 설치 [!DNL Enhanced Conversions] 확장 {#install-enhanced-conversions}

다음 찾기 [!UICONTROL Google Ads 향상된 전환] 이벤트 전달 카탈로그의 확장명을 선택하고 **[!UICONTROL 설치]**.

![다음 [!UICONTROL Google Ads 향상된 전환] 확장 프로그램 선택 중 [!UICONTROL 확장] 다음에서 보기 [!UICONTROL 데이터 수집] UI.](../../../images/extensions/server/google-ads-enhanced-conversions/install-enhanced-conversions.png)

확장을 구성하려면 다음 두 필수 필드를 채워야 합니다.

1. **[!UICONTROL 고객 ID]**: 를 고유하게 식별하는 ID입니다. [!DNL Google Ads] 계정입니다. 이 값을 찾으려면 로그인합니다. [!DNL Google Ads] 다음 위치로 이동 **[!DNL Help]** > **[!DNL Customer ID]**.
1. **[!UICONTROL 액세스 토큰 데이터 요소]**: 데이터 요소 아이콘(![데이터 요소 아이콘](../../../images/extensions/server/google-ads-enhanced-conversions/data-element-icon.png)) 원하는 Google OAuth 2 암호 데이터 요소를 선택합니다 [이전 단계에서 구성됨](#create-secret-data-element) 메뉴에서 삭제할 수 있습니다.

완료되면 다음을 선택합니다. **[!UICONTROL 저장]** 확장을 설치합니다.

### 추가 [!UICONTROL 변환 전송] 규칙에 대한 작업 {#conversion-action-event-forwarding}

확장이 설치되면 다음을 시작할 수 있습니다. [!UICONTROL 변환 전송] 이벤트 전달 규칙의 작업입니다. 개선하려는 전환을 수신하는 규칙을 만들거나 편집할 때 다음을 선택합니다 **[!UICONTROL 추가]** 아래에 [!UICONTROL 작업]. 다음 대화 상자에서 을 선택합니다. **[!UICONTROL Google Ads 향상된 전환]** 다음에서 [!UICONTROL 확장] 드롭다운을 선택한 다음 을 선택합니다. **[!UICONTROL 변환 전송]** 아래에 [!UICONTROL 작업 유형].

![다음 [!UICONTROL 변환 전송] 규칙 편집 워크플로의 작업 구성 보기에서 작업 유형을 선택하고 있습니다.](../../../images/extensions/server/google-ads-enhanced-conversions/select-server-action.png)

오른쪽 패널에 변환을 구성할 수 있는 새 컨트롤이 나타납니다. 최소한 다음 필드를 완료해야 합니다.

**전환 정보**

| 입력 | 설명 |
| --- | --- |
| 고객 ID | 사용자 [!DNL Google Ads] 고객 ID. 기본값은 다음과 같은 경우 입력한 고객 ID로 설정됩니다. [확장 설치](#install-enhanced-conversions). |
| 전환 ID 또는 전환 레이블 | 다음에서 얻은 추적 값 [!DNL Google Ads] 전환 추적을 설정할 때. 값 시작 문자 `AW-`.<br><br>이러한 값을 찾는 방법에 대한 자세한 내용은 [[!DNL Google Ads] 설명서](https://support.google.com/tagmanager/answer/6105160?hl=en). |
| 거래 ID | 다음과 동일한 거래 ID 값을 가진 데이터 요소를 선택합니다. [클라이언트측에서 보냄](#conversion-action-tags) 사용 [!DNL Google Global Site Tag] 확장명. |

**사용자 식별**

* 다음 세 가지 사용자 식별자 중 하나 이상을 포함해야 합니다.
   * 이메일
   * 전화 번호
   * 전체 주소

>[!TIP]
>
>사용자 ID 데이터를 Google으로 보내기 전에 해시해야 합니다. 이벤트 전달이 데이터를 받을 때 데이터가 해시되지 않으면 **[!UICONTROL 정규화 및 해시]** 해당 필드를 전환하여 확장에서 값을 해시하도록 지시합니다.
>
>![다음 [!UICONTROL 정규화 및 해시] 다음에 대해 활성화됨 [!UICONTROL 이메일] 다음 내에 입력: [!UICONTROL 변환 전송] 작업 구성 양식입니다.](../../../images/extensions/server/google-ads-enhanced-conversions/hash-user-id-values.png)

완료되면 다음을 선택합니다. **[!UICONTROL 변경 내용 유지]** 작업을 규칙 구성에 추가합니다. 규칙에 만족하면 다음을 선택합니다. **[!UICONTROL 라이브러리에 저장]**.

마지막으로 새 이벤트 전달을 게시합니다. [빌드](../../../ui/publishing/builds.md) 라이브러리에 대한 변경 사항을 활성화합니다.

## 다음 단계

이 안내서에서는 전환 이벤트를에 보내는 방법을 다룹니다. [!DNL Google Ads] 사용 [!DNL Enhanced Conversions] 이벤트 전달 확장. Experience Platform의 이벤트 전달 기능에 대한 자세한 내용은 [이벤트 전달 개요](../../../ui/event-forwarding/overview.md).
