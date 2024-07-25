---
title: Google Ads Enhanced Conversions 확장
description: Adobe Experience Platform의 이벤트 전달을 위한 Google Ads Enhanced Conversion 확장에 대해 알아봅니다.
exl-id: 65cdff40-276f-4481-9621-6c6861dbd412
last-substantial-update: 2022-11-23T00:00:00Z
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1296'
ht-degree: 1%

---

# [!DNL Google Ads] 향상된 전환 확장

[!DNL Google Ads] API를 사용하면 전환 조정 형식으로 자사 고객 데이터를 전송하여 [향상된 전환](https://support.google.com/google-ads/answer/9888656)을 활용할 수 있습니다. Google은 이 추가 데이터를 사용하여 광고 상호 작용에 따른 온라인 전환에 대한 보고를 향상시킵니다.

[[!DNL Google Ads] 향상된 전환 이벤트 전달 확장](https://exchange.adobe.com/apps/ec/108630/google-ads-enhanced-conversions)(이전의 [!DNL Enhanced Conversions] 확장)은 [!DNL Google Ads] API에 대한 향상된 전환을 쉽게 구현할 수 있는 사용자 친화적인 템플릿을 제공합니다.

>[!IMPORTANT]
>
>향상된 전환은 구독, 등록 및 구매와 같이 고객 데이터가 있는 전환 유형에만 작동합니다. 다음 고객 데이터 중 하나 이상을 사용할 수 있어야 합니다. 이벤트 전달 규칙에 대해 [전환 작업을 구성](#conversion-action-event-forwarding)할 때 필요합니다.
>
>* 이메일 주소(기본 설정)
>* 이름 및 집 주소(주소, 구/군/시, 시/도 및 우편 번호)
>* 전화번호(위의 다른 두 정보 중 하나와 함께 제공해야 함)

## 구현 개요

향상된 전환은 [!DNL Google Ads] API를 활용하여 클라이언트 장치(일반적으로 웹 사이트)에서 발생한 전환에 자사 데이터를 추가합니다. 즉, 향상된 전환을 구현하는 두 가지 단계가 있습니다.

1. 클라이언트에서 전환을 보냅니다.
1. 이벤트 전달을 사용하여 클라이언트에서 보낸 전환 데이터를 향상시키는 추가 자사 데이터를 보냅니다.

>[!TIP]
>
>클라이언트측 전환 이벤트를 이벤트 전달에서 보낸 자사 데이터와 연결하려면 `transaction_ID`이(가) 두 호출에서 동일해야 합니다. 각 서비스에 대해 이 값을 제공해야 하는 위치에 대한 자세한 내용은 각각 [태그](#conversion-action-tags) 및 [이벤트 전달](#conversion-action-event-forwarding)에 대한 전환 작업 구성에 대한 섹션을 참조하십시오.

전환 이벤트 전송에는 클라이언트측과 서버측 구현이 모두 포함되므로, 이 문서에서는 이벤트 전달을 위한 [!DNL Enhanced Conversions] 확장 외에 클라이언트측 [[!DNL Google Global Site Tag] (gtag) 확장](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag)을(를) 설정하는 사전 요구 단계를 다룹니다.

다음 비디오는 [!DNL Enhanced Conversions] 확장을 소개하고 구현 단계를 높은 수준으로 안내합니다.

>[!VIDEO](https://video.tv.adobe.com/v/3411365?quality=12&learn=on)

## 태그를 사용하여 변환 보내기

웹 사이트에서 전환 이벤트를 보내려면 [!DNL Google Global Site Tag](gtag)을(를) 배포해야 합니다. [!DNL Google Global Site Tag](gtag) 확장을 구성 및 설치하여 태그를 사용하여 이를 수행할 수 있습니다.

### [!DNL Google Global Site Tag] 확장 구성 및 설치

[!UICONTROL 데이터 수집] UI 또는 Experience Platform UI로 이동하고 왼쪽 탐색에서 **[!UICONTROL 태그]**&#x200B;를 선택합니다. 확장을 설치할 태그 속성을 선택한 다음 왼쪽 탐색에서 **[!UICONTROL 확장]**&#x200B;을 선택합니다. **[!UICONTROL 카탈로그]** 탭에서 [!UICONTROL Google 글로벌 사이트 태그(gtag)] 확장을 찾아 **[!UICONTROL 설치]**&#x200B;를 선택합니다.

![[!UICONTROL Google 전역 사이트 태그(gtag)] 확장이 [!UICONTROL 데이터 수집] UI의 [!UICONTROL 확장] 보기에서 선택됩니다.](../../../images/extensions/server/google-ads-enhanced-conversions/install-gtag-extension.png)

설치 대화 상자가 나타납니다. 여기에서 **[!UICONTROL 계정 추가]**&#x200B;를 선택하고 메시지가 표시되면 다음 값을 제공합니다.

| 계정 속성 | 설명 |
| --- | --- |
| 계정 이름 | 계정에 대한 고유한 이름. 이 이름은 태그 UI 내에서만 사용됩니다. |
| 계정 ID | [!DNL Google Ads] 계정 ID입니다. 이 값을 찾으려면 [!DNL Google Ads]에 로그인하고 **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Install the Tag yourself]**(으)로 이동합니다. 계정 ID 문자열은 `AW-` 또는 `d`(으)로 시작하는 코드 조각 창에서 찾을 수 있습니다. |
| 제품 | **[!UICONTROL Google 광고(AdWords)]**&#x200B;를 선택합니다. |

{style="table-layout:auto"}

완료되면 **[!UICONTROL 계정 추가]**&#x200B;를 선택한 다음 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

### 전환 보내기 작업 추가 {#conversion-action-tags}

확장을 설치한 후 태그 규칙에 전환 작업을 포함할 수 있습니다. 개선하려는 전환을 수신하는 규칙을 만들거나 편집할 때 [!UICONTROL 작업]에서 **[!UICONTROL 추가]**&#x200B;를 선택하십시오. 다음 대화 상자에서 [!UICONTROL 확장] 드롭다운에서 **[!UICONTROL Google 전역 사이트 태그(gtag)]**&#x200B;를 선택한 다음 [!UICONTROL 작업 유형]에서 **[!UICONTROL 이벤트 보내기]**&#x200B;를 선택합니다.

![규칙 편집 워크플로의 작업 구성 보기에서 [!UICONTROL 이벤트 보내기] 작업 유형을 선택하고 있습니다.](../../../images/extensions/server/google-ads-enhanced-conversions/select-client-action.png)

[!DNL gtag] 이벤트를 구성할 수 있는 추가 컨트롤이 나타납니다. 최소한 다음 필드를 작성해야 합니다.

1. **[!UICONTROL 이벤트 이름(작업)]**: 값으로 `conversion`을(를) 입력하십시오.
1. 키가 `transaction_id`이고 값이 [트랜잭션 ID](https://support.google.com/google-ads/answer/6386790) 값을 포함하는 [데이터 요소](../../../ui/managing-resources/data-elements.md)인 새 필드를 추가합니다.
1. **[!UICONTROL 전환 레이블]**: [!DNL Google Ads] 계정에서 적절한 전환 레이블을 입력합니다. 이 값을 찾으려면 Google Ads에 로그인한 다음 **[!DNL Tools and Settings]** > **[!DNL Conversions]** > **[!DNL Select a conversion action]** > **[!DNL Tag Setup]** > **[!DNL Use Google Tag Manager]**(으)로 이동합니다. 전환 레이블은 [!DNL Instructions]에서 찾을 수 있습니다.
   >[!IMPORTANT]
   >
   >[!DNL Google Ads] 계정의 태그 설정 영역에 있는 동안 향상된 전환이 활성화되어 있는지 확인하십시오. 이렇게 하려면 서비스 약관을 검토하고 동의한 다음 구현 방법으로 **[!DNL Turn on enhanced conversions]** 및 **[!DNL API]**&#x200B;을(를) 선택합니다.

작업을 구성한 후 **[!UICONTROL 변경 내용 유지]**&#x200B;를 선택하여 작업을 규칙 구성에 추가합니다. 규칙에 만족하면 **[!UICONTROL 라이브러리에 저장]**&#x200B;을 선택합니다.

마지막으로 새 [빌드](../../../ui/publishing/builds.md)를 게시하여 라이브러리에 대한 변경 사항을 활성화하십시오.

## 이벤트 전달을 사용하여 자사 데이터 보내기

클라이언트측에서 전환 이벤트를 보낼 수 있게 되면 [!DNL Enhanced Conversions] 이벤트 전달 확장을 사용하여 이러한 전환을 향상시킬 수 있습니다.

### Google OAuth 2 암호 및 데이터 요소 만들기 {#create-secret-data-element}

확장을 구성하기 전에 이벤트 전달에서 액세스 토큰을 만들어 [!DNL Google Ads] API를 인증해야 합니다.

자세한 단계는 [이벤트 전달 암호 만들기](../../../ui/event-forwarding/secrets.md)에 대한 안내서를 참조하세요. **[!UICONTROL Google OAuth 2]**&#x200B;을(를) 암호 유형으로 선택해야 합니다. 계속해서 화면의 지시를 따르고 Google 계정 프로필을 선택하라는 메시지가 표시되면 구성 중인 전환 작업에 액세스할 수 있는 계정을 선택합니다.

암호가 만들어지면 [새 데이터 요소를 만들고](../../../ui/managing-resources/data-elements.md#create-a-data-element) 데이터 요소 유형으로 **[!UICONTROL 암호]**&#x200B;를 선택하십시오. 각 환경에 적합한 Google OAuth 2 암호를 선택하고 **[!UICONTROL 라이브러리에 저장]**&#x200B;을 선택합니다.

### [!DNL Enhanced Conversions] 확장 구성 및 설치 {#install-enhanced-conversions}

이벤트 전달 카탈로그에서 [!UICONTROL Google 광고 향상된 전환] 확장을 찾아 **[!UICONTROL 설치]**&#x200B;를 선택합니다.

![[!UICONTROL Google 광고 향상된 전환] 확장이 [!UICONTROL 데이터 수집] UI의 [!UICONTROL 확장] 보기에서 선택됩니다.](../../../images/extensions/server/google-ads-enhanced-conversions/install-enhanced-conversions.png)

확장을 구성하려면 다음 두 필수 필드를 채워야 합니다.

1. **[!UICONTROL 고객 ID]**: [!DNL Google Ads] 계정을 고유하게 식별하는 ID입니다. 이 값을 찾으려면 [!DNL Google Ads]에 로그인한 다음 **[!DNL Help]** > **[!DNL Customer ID]**(으)로 이동합니다.
2. **[!UICONTROL 액세스 토큰 데이터 요소]**: 데이터 요소 아이콘(![데이터 요소 아이콘](/help/images/icons/database.png))을 선택하고 [이전 단계에서 구성한](#create-secret-data-element)Google OAuth 2 비밀 데이터 요소를 메뉴에서 선택합니다.

완료되면 **[!UICONTROL 저장]**&#x200B;을 선택하여 확장을 설치합니다.

### 규칙에 [!UICONTROL 전환 보내기] 작업 추가 {#conversion-action-event-forwarding}

확장이 설치되면 이벤트 전달 규칙에 [!UICONTROL 변환 보내기] 작업을 포함할 수 있습니다. 개선하려는 전환을 수신하는 규칙을 만들거나 편집할 때 [!UICONTROL 작업]에서 **[!UICONTROL 추가]**&#x200B;를 선택합니다. 다음 대화 상자에서 [!UICONTROL 확장] 드롭다운에서 **[!UICONTROL Google 광고 향상된 전환]**&#x200B;을 선택한 다음 [!UICONTROL 작업 유형]에서 **[!UICONTROL 전환 보내기]**&#x200B;를 선택합니다.

![규칙 편집 워크플로의 작업 구성 보기에서 [!UICONTROL 변환 보내기] 작업 유형을 선택하고 있습니다.](../../../images/extensions/server/google-ads-enhanced-conversions/select-server-action.png)

오른쪽 패널에 변환을 구성할 수 있는 새 컨트롤이 나타납니다. 최소한 다음 필드를 완료해야 합니다.

**전환 정보**

| 입력 | 설명 |
| --- | --- |
| 고객 ID | [!DNL Google Ads] 고객 ID입니다. 기본값은 [확장을 설치](#install-enhanced-conversions)할 때 입력한 고객 ID입니다. |
| 전환 ID 또는 전환 레이블 | 전환 추적을 설정할 때 [!DNL Google Ads]에서 가져온 추적 값입니다. 값은 `AW-`(으)로 시작합니다.<br><br>이러한 값을 찾는 방법에 대한 자세한 내용은 [[!DNL Google Ads] 설명서](https://support.google.com/tagmanager/answer/6105160?hl=en)를 참조하세요. |
| 거래 ID | [!DNL Google Global Site Tag] 확장을 사용하여 클라이언트 측에서 [보낸](#conversion-action-tags)과(와) 같은 트랜잭션 ID 값이 있는 데이터 요소를 선택하십시오. |

**사용자 식별**

* 다음 세 가지 사용자 식별자 중 하나 이상을 포함해야 합니다.
   * 이메일
   * 전화번호
   * 전체 주소

>[!TIP]
>
>사용자 ID 데이터를 Google으로 보내기 전에 해시해야 합니다. 이벤트 전달이 데이터를 받을 때 데이터가 해시되지 않으면 지정된 필드에서 **[!UICONTROL 정규화 및 해시]** 전환을 선택하여 확장에서 값을 해시하도록 지시합니다.
>
>![[!UICONTROL 변환 보내기] 작업 구성 양식의 [!UICONTROL 전자 메일] 입력에 대해 [!UICONTROL 정규화 및 해시] 토글을 사용할 수 있습니다.](../../../images/extensions/server/google-ads-enhanced-conversions/hash-user-id-values.png)

완료되면 **[!UICONTROL 변경 내용 유지]**&#x200B;를 선택하여 작업을 규칙 구성에 추가합니다. 규칙에 만족하면 **[!UICONTROL 라이브러리에 저장]**&#x200B;을 선택합니다.

마지막으로 새 이벤트 전달 [build](../../../ui/publishing/builds.md)을(를) 게시하여 라이브러리에 대한 변경 사항을 활성화하십시오.

## 다음 단계

이 안내서에서는 [!DNL Enhanced Conversions] 이벤트 전달 확장을 사용하여 전환 이벤트를 [!DNL Google Ads]에 보내는 방법을 다룹니다. Experience Platform의 이벤트 전달 기능에 대한 자세한 내용은 [이벤트 전달 개요](../../../ui/event-forwarding/overview.md)를 참조하세요.
