---
keywords: Google 광고;google 광고;google adwords;Google AdWords;Google Adwords
title: Google 광고 연결
description: 이전에 Google AdWords라고 알려진 Google Ads는 텍스트 기반 검색, 그래픽 디스플레이, YouTube 비디오 및 인앱 모바일 디스플레이에서 클릭당 과금광고를 할 수 있도록 하는 온라인 광고 서비스입니다.
exl-id: 7143f476-49a8-42aa-bfb4-b11fc2b8f5c3
source-git-commit: f04ea9aed586c8582286de82bfeee3f6f04cc360
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 2%

---

# [!DNL Google Ads] 연결

## 개요 {#overview}

[!DNL Google Ads]이전에  [!DNL Google AdWords]라고 했던 는 텍스트 기반 검색, 그래픽 디스플레이,  [!DNL YouTube] 비디오 및 인앱 모바일 디스플레이에서 클릭당 과금을 통해 광고를 수행할 수 있도록 하는 온라인 광고 서비스입니다.

## 대상 세부 사항 {#specifics}

[!DNL Google Ads] 대상에 해당하는 다음 세부 사항을 참고하십시오.

* 활성화된 대상은 [!DNL Google] 플랫폼에서 프로그래밍 방식으로 만들어집니다.
* [!DNL Platform] 현재 에는 성공적인 활성화를 확인하기 위한 측정 지표가 포함되어 있지 않습니다. 통합의 유효성을 확인하고 대상 타깃팅 크기를 이해하려면 Google의 대상 카운트를 참조하십시오.

>[!IMPORTANT]
>
>[!DNL Google Ads]을(를) 사용하여 첫 번째 대상을 만들고, 과거에 Experience Cloud ID 서비스에서 [ID 동기화 기능](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html)을 활성화하지 않은 경우(Audience Manager 또는 다른 애플리케이션 사용) Adobe 컨설팅이나 고객 지원 센터에 연락하여 ID 동기화를 활성화하십시오. 이전에 Audience Manager에서 Google 통합을 설정한 경우, 설정한 ID 동기화를 Platform으로 이월합니다.

## 지원되는 ID {#supported-identities}

[!DNL Google Ad Manager] 은 아래 표에 설명된 id의 활성화를 지원합니다.

| Target ID | 설명 | 고려 사항 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | 소스 ID가 GAID 네임스페이스이면 이 대상 ID를 선택합니다. |
| IDFA | [!DNL Apple ID for Advertisers] | 소스 ID가 IDFA 네임스페이스인 경우 이 타겟 ID를 선택합니다. |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html)(라고도 함) [!DNL Device ID]. Audience Manager이 상호 작용하는 각 장치에 연결하는 38자리 숫자 장치 ID입니다. | Google은 [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en)를 사용하여 캘리포니아에 있는 사용자를 타깃팅하고 다른 모든 사용자에 대해 Google 쿠키 ID를 사용합니다. |
| [!DNL Google] 쿠키 ID | [!DNL Google] 쿠키 ID | [!DNL Google] 는 이 ID를 사용하여 캘리포니아 외부의 사용자를 타깃팅합니다. |
| RIDA | 광고용 Roku ID. 이 ID는 Roku 장치를 고유하게 식별합니다. |  |
| 가정부 | Microsoft 광고 ID. 이 ID는 Windows 10을 실행하는 장치를 고유하게 식별합니다. |  |
| Amazon Fire TV ID | 이 ID는 Amazon Fire TV를 고유하게 식별합니다. |  |

## 내보내기 유형 {#export-type}

**세그먼트 내보내기**  - 세그먼트(대상)의 모든 구성원을 Google 대상으로 내보냅니다.

## 전제 조건 {#prerequisites}

### 기존 [!DNL Google Ads] 계정

>[!IMPORTANT]
>
> [!DNL Google] 에는 타사  [!DNL Google Ads] 공급업체와의 새 쿠키 통합 사용이 더 이상 사용되지 않습니다. 다음 섹션에서 허용 목록 단계를 수행하려면 [!DNL Google Ads]과(와) 기존 통합이 있어야 합니다. 따라서 [!DNL Google Ads] 사용에 대한 권장 접근 방식은 [!DNL Google Customer Match] 통합을 설정하는 것입니다. [!DNL Google Customer Match] 통합 만들기에 대한 자세한 내용은 [[!DNL Google Customer Match]](./google-customer-match.md) 연결 만들기에 대한 자습서를 참조하십시오.

### 허용 목록 {#allow-listing}

>[!NOTE]
>
>Platform에서 첫 번째 [!DNL Google Ads] 대상을 설정하기 전에 허용 목록이 필수입니다. 대상을 만들기 전에 아래에 설명된 허용 목록 프로세스가 [!DNL Google]에 의해 완료되었는지 확인하십시오.

Platform에서 [!DNL Google Ads] 대상을 만들려면 먼저 [!DNL Google]에 연락하여 Adobe이 허용된 데이터 공급자 목록에 배치되고 허용 목록에 계정이 추가되도록 해야 합니다. [!DNL Google]에 문의하여 다음 정보를 제공하십시오.

* **계정 ID**: Google을 사용하는 Adobe 계정 ID입니다. 계정 ID: 87933855.
* **고객 ID**: Google을 사용하는 Adobe의 고객 계정 ID입니다. 고객 ID: 89690775.
* 계정 유형: **AdWords**
* **Google AdWords ID**: 사용할 ID입니다  [!DNL Google]. ID 형식은 일반적으로 123-456-7890.

## 대상에 연결 {#connect}

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오.

### 연결 매개 변수 {#parameters}

[이 대상을 설정할 때 다음 정보를 제공해야 합니다.](../../ui/connect-destination.md)

* **[!UICONTROL 이름]**: 이 대상의 기본 이름을 입력합니다.
* **[!UICONTROL 설명]**: 선택 사항입니다. 예를 들어 이 대상을 사용하는 캠페인을 언급할 수 있습니다.
* **[!UICONTROL 계정 유형]**: AdWords만 사용할 수 있습니다.
* **[!UICONTROL 계정 ID]**: 계정 ID를  [!DNL Google Ads]. ID 형식은 일반적으로 123-456-7890.

## 세그먼트를 이 대상에 활성화 {#activate}

대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침은 [스트리밍 세그먼트 내보내기 대상으로 대상 활성화](../../ui/activate-segment-streaming-destinations.md)를 참조하십시오.

## 내보낸 데이터

데이터를 [!DNL Google Ads] 대상으로 성공적으로 내보냈는지 확인하려면 [!DNL Google Ads] 계정을 확인하십시오. 활성화가 성공하면 계정에 대상이 채워집니다.

## 문제 해결 {#troubleshooting}

### 400 잘못된 요청 오류 메시지 {#bad-request}

이 대상을 구성할 때 다음 오류가 표시될 수 있습니다.

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

이 오류는 고객 계정이 [사전 요구 사항](#prerequisites)을 준수하지 않거나 고객이 기존 [!DNL Google Ads] 계정 없이 대상을 구성하려고 할 때 발생합니다.

[!DNL Google] 에는 타사  [!DNL Google Ads] 공급업체와의 새 쿠키 통합 사용이 더 이상 사용되지 않습니다. [allow-list](#allow-listing) 단계를 수행하려면 [!DNL Google Ads]와 기존 통합이 있어야 합니다.

[!DNL Google Ads] 사용에 대한 권장 접근 방식은 [[!DNL Google Customer Match]](google-customer-match.md) 통합을 설정하는 것입니다.
