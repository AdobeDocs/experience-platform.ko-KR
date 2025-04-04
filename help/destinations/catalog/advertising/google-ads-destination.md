---
title: Google 광고 연결
description: 이전에 Google AdWords로 알려졌던 Google Ads는 기업이 텍스트 기반 검색, 그래픽 디스플레이, YouTube 비디오 및 인앱 모바일 디스플레이에서 클릭당 과금 광고를 할 수 있도록 해주는 온라인 광고 서비스입니다.
exl-id: 7143f476-49a8-42aa-bfb4-b11fc2b8f5c3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 2%

---

# [!DNL Google Ads] 연결

## 개요 {#overview}

이전에 [!DNL Google AdWords]&#x200B;(으)로 알려졌던 [!DNL Google Ads]은(는) 기업이 텍스트 기반 검색, 그래픽 디스플레이, [!DNL YouTube] 비디오 및 인앱 모바일 디스플레이 전반에 걸쳐 클릭당 과금 광고를 할 수 있도록 해주는 온라인 광고 서비스입니다.

## 대상 세부 사항 {#specifics}

[!DNL Google Ads] 대상에 해당하는 다음 세부 정보를 참고하십시오.

* 활성화된 대상은 [!DNL Google] 플랫폼에서 프로그래밍 방식으로 만들어집니다.
* [!DNL Experience Platform]은(는) 현재 성공적인 활성화를 확인하기 위한 측정 지표를 포함하지 않습니다. 통합의 유효성을 검사하고 대상 타깃팅 크기를 이해하려면 Google의 대상 수 를 참조하십시오.

>[!IMPORTANT]
>
>[!DNL Google Ads]을(를) 사용하여 첫 번째 대상을 만들려고 하는데 이전에 Experience Cloud ID 서비스에서 [ID 동기화 기능](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html)을(를) 활성화하지 않은 경우(Audience Manager 또는 다른 응용 프로그램 사용) Adobe Consulting 또는 고객 지원 센터에 연락하여 ID 동기화를 활성화하십시오. 이전에 Audience Manager에서 Google 통합을 설정한 경우 설정한 ID 동기화가 Experience Platform으로 이월됩니다.

## 지원되는 ID {#supported-identities}

[!DNL Google Ads]은(는) 아래 표에 설명된 ID 활성화를 지원합니다.

| 대상 ID | 설명 | 고려 사항 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | 소스 ID가 GAID 네임스페이스인 경우 이 대상 ID를 선택합니다. |
| IDFA | [!DNL Apple ID for Advertisers] | 소스 ID가 IDFA 네임스페이스인 경우 이 대상 ID를 선택합니다. |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html)&#x200B;(일명 [!DNL Device ID]). Audience Manager이 상호 작용하는 각 장치에 연결하는 숫자 38자리 장치 ID입니다. | Google은 [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html)을(를) 사용하여 캘리포니아에 있는 사용자를 타깃팅하고 다른 모든 사용자의 Google 쿠키 ID를 사용합니다. |
| [!DNL Google] 쿠키 ID | [!DNL Google] 쿠키 ID | [!DNL Google]은(는) 이 ID를 사용하여 캘리포니아 외부의 사용자를 타깃팅합니다. |
| 리다 | Advertising용 Roku ID. 이 ID는 Roku 장치를 고유하게 식별합니다. |  |
| 하녀 | Microsoft Advertising ID. 이 ID는 Windows 10을 실행하는 장치를 고유하게 식별합니다. |  |
| Amazon Fire TV ID | 이 ID는 Amazon Fire TV를 고유하게 식별합니다. |  |

{style="table-layout:auto"}

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Experience Platform [세그먼테이션 서비스](../../../segmentation/home.md)를 통해 생성된 대상입니다. |
| 사용자 정의 업로드 | ✓ | CSV 파일에서 Experience Platform으로 대상 [가져옴](../../../segmentation/ui/audience-portal.md#import-audience). |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 대상자 내보내기]** | 대상의 모든 구성원을 Google 대상으로 내보내고 있습니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 전제 조건 {#prerequisites}

### 기존 [!DNL Google Ads] 계정

>[!IMPORTANT]
>
> [!DNL Google]은(는) 타사 공급업체와의 새로운 [!DNL Google Ads] 쿠키 통합을 더 이상 사용하지 않습니다. 다음 섹션에서 허용 목록에 추가하다 단계를 수행하려면 [!DNL Google Ads]과(와) 기존의 통합이 있어야 합니다. 따라서 [!DNL Google Ads]을(를) 사용하기 위한 권장 접근 방식은 [!DNL Google Customer Match] 통합을 설정하는 것입니다. [!DNL Google Customer Match] 통합 만들기에 대한 자세한 내용은 [[!DNL Google Customer Match]](./google-customer-match.md) 연결 만들기에 대한 자습서를 참조하십시오.

### 허용 목록 {#allow-listing}

>[!NOTE]
>
>Experience Platform에서 첫 번째 [!DNL Google Ads] 대상을 설정하기 전에 허용 목록이 필수입니다. 대상을 만들기 전에 [!DNL Google]이(가) 아래에 설명된 허용 목록 프로세스를 완료했는지 확인하십시오.
>이 규칙은 [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html) 고객에 대해 예외입니다. Audience Manager에서 이 Google 대상에 대한 연결을 이미 만든 경우 허용 목록 프로세스를 다시 진행할 필요가 없으며 다음 단계를 진행할 수 있습니다.

Experience Platform에서 [!DNL Google Ads] 대상을 만들기 전에 [!DNL Google]에 연락하여 Adobe을 허용된 데이터 공급자 목록에 추가하고 계정을 허용 목록에 추가하다에 추가해야 합니다. [!DNL Google]에게 연락하여 다음 정보를 제공하십시오.

* **계정 ID**: Adobe의 Google 계정 ID입니다. 계정 ID: 87933855.
* **고객 ID**: Adobe의 Google 고객 계정 ID입니다. 고객 ID: 89690775.
* 계정 유형: **AdWords**
* **Google AdWords ID**: [!DNL Google]의 ID입니다. ID 형식은 일반적으로 123-456-7890입니다.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오.

### 연결 매개변수 {#parameters}

[이 대상을 설정](../../ui/connect-destination.md)하는 동안 다음 정보를 제공해야 합니다.

* **[!UICONTROL 이름]**: 이 대상의 기본 이름을 입력하십시오.
* **[!UICONTROL 설명]**: 선택 사항입니다. 예를 들어 이 대상을 사용하는 캠페인을 언급할 수 있습니다.
* **[!UICONTROL 계정 유형]**: AdWords만 사용할 수 있습니다.
* **[!UICONTROL 계정 ID]**: [!DNL Google Ads]&#x200B;(으)로 계정 ID를 입력하십시오. ID 형식은 일반적으로 123-456-7890입니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 모두 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 대한 대상 활성화에 대한 지침은 [대상 데이터를 스트리밍 대상 내보내기 대상으로 활성화](../../ui/activate-segment-streaming-destinations.md)를 참조하십시오.

## 내보낸 데이터

데이터를 [!DNL Google Ads] 대상으로 내보냈는지 확인하려면 [!DNL Google Ads] 계정을 확인하세요. 활성화가 성공하면 계정에 대상자가 채워집니다.

## 문제 해결 {#troubleshooting}

### 400 잘못된 요청 오류 메시지 {#bad-request}

이 대상을 구성할 때 다음 오류가 표시될 수 있습니다.

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

이 오류는 고객 계정이 [필수 구성 요소](#prerequisites)를 준수하지 않거나 고객이 기존 [!DNL Google Ads] 계정 없이 대상을 구성하려고 할 때 발생합니다.

[!DNL Google]은(는) 타사 공급업체와의 새로운 [!DNL Google Ads] 쿠키 통합을 더 이상 사용하지 않습니다. 허용 목록에 추가하다 [단계](#allow-listing)를 수행하려면 [!DNL Google Ads]과의 기존 통합이 있어야 합니다.

[!DNL Google Ads]을(를) 사용하기 위한 권장 접근 방식은 [[!DNL Google Customer Match]](google-customer-match.md) 통합을 설정하는 것입니다.
