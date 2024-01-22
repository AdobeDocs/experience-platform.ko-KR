---
title: Google 광고 연결
description: 이전에 Google AdWords로 알려졌던 Google Ads는 기업이 텍스트 기반 검색, 그래픽 디스플레이, YouTube 비디오 및 인앱 모바일 디스플레이에서 클릭당 과금 광고를 할 수 있도록 해주는 온라인 광고 서비스입니다.
exl-id: 7143f476-49a8-42aa-bfb4-b11fc2b8f5c3
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '949'
ht-degree: 2%

---

# [!DNL Google Ads] 연결

## 개요 {#overview}

[!DNL Google Ads], 이전에 [!DNL Google AdWords]는 기업이 텍스트 기반 검색, 그래픽 디스플레이 전반에 걸쳐 클릭당 과금 광고를 할 수 있는 온라인 광고 서비스입니다. [!DNL YouTube] 비디오 및 인앱 모바일 디스플레이.

## 대상 세부 사항 {#specifics}

다음의 세부 사항에 유의하십시오. [!DNL Google Ads] 대상:

* 활성화된 대상은에서 프로그래밍 방식으로 만들어집니다. [!DNL Google] 플랫폼.
* [!DNL Platform] 현재 성공적인 활성화를 확인하기 위한 측정 지표는 포함되어 있지 않습니다. 통합의 유효성을 검사하고 대상 타깃팅 크기를 이해하려면 Google의 대상 수 를 참조하십시오.

>[!IMPORTANT]
>
>을(를) 사용하여 첫 번째 대상을 만들려는 경우 [!DNL Google Ads] 및 이(가) 을(를) 활성화하지 않음 [ID 동기화 기능](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) 과거의 Experience Cloud ID 서비스(Audience Manager 또는 기타 애플리케이션 포함)에서 ID 동기화를 활성화하려면 Adobe 컨설팅 또는 고객 지원 센터에 문의하십시오. 이전에 Audience Manager에서 Google 통합을 설정한 경우 설정한 ID가 플랫폼으로 이월됩니다.

## 지원되는 ID {#supported-identities}

[!DNL Google Ads] 는 아래 표에 설명된 id 활성화를 지원합니다.

| 대상 ID | 설명 | 고려 사항 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | 소스 ID가 GAID 네임스페이스인 경우 이 대상 ID를 선택합니다. |
| IDFA | [!DNL Apple ID for Advertisers] | 소스 ID가 IDFA 네임스페이스인 경우 이 대상 ID를 선택합니다. |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html)라고도 함 [!DNL Device ID]. Audience Manager이 상호 작용하는 각 장치에 연결하는 숫자 38자리 장치 ID입니다. | Google 사용 [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html) Google 를 사용하십시오. |
| [!DNL Google] 쿠키 ID | [!DNL Google] 쿠키 ID | [!DNL Google] 은 이 ID를 사용하여 캘리포니아 외부의 사용자를 타깃팅합니다. |
| 리다 | Advertising용 Roku ID. 이 ID는 Roku 장치를 고유하게 식별합니다. |  |
| 하녀 | Microsoft 광고 ID. 이 ID는 Windows 10을 실행하는 장치를 고유하게 식별합니다. |  |
| Amazon Fire TV ID | 이 ID는 Amazon Fire TV를 고유하게 식별합니다. |  |

{style="table-layout:auto"}

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ 덧신 | Experience Platform을 통해 생성된 대상자 [세분화 서비스](../../../segmentation/home.md). |
| 사용자 정의 업로드 | ✓ | 대상 [가져옴](../../../segmentation/ui/overview.md#import-audience) csv 파일에서 Experience Platform으로 변환했습니다. |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 대상자 내보내기]** | 대상의 모든 구성원을 Google 대상으로 내보내고 있습니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 전제 조건 {#prerequisites}

### 기존 항목 [!DNL Google Ads] account

>[!IMPORTANT]
>
> [!DNL Google] 더 이상 사용되지 않는 새로운 기능 포함 [!DNL Google Ads] 쿠키와 타사 공급업체의 통합. 다음 섹션의 허용 목록에 추가하다 단계를 수행하려면 와 기존의 통합이 있어야 합니다 [!DNL Google Ads]. 따라서 사용에 대한 권장 접근 방식 [!DNL Google Ads] 을(를) 설정하는 중 [!DNL Google Customer Match] 통합. 만들기에 대한 자세한 내용은 [!DNL Google Customer Match] 통합에서 만들기 자습서를 참조하십시오. [[!DNL Google Customer Match]](./google-customer-match.md) 연결.

### 허용 목록 {#allow-listing}

>[!NOTE]
>
>첫 번째 항목을 설정하기 전에 허용 목록은 필수입니다. [!DNL Google Ads] 대상(플랫폼 내) 아래 설명된 허용 목록 프로세스가 다음 기한까지 완료되었는지 확인합니다. [!DNL Google] 대상을 만들기 전에.
>이 규칙의 예외는 다음과 같습니다 [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html) 고객. Audience Manager에서 이 Google 대상에 대한 연결을 이미 만든 경우 허용 목록 프로세스를 다시 진행할 필요가 없으며 다음 단계를 진행할 수 있습니다.

만들기 전에 [!DNL Google Ads] 플랫폼의 대상입니다. 다음으로 문의해야 합니다 [!DNL Google] Adobe을 허용된 데이터 공급자 목록에 추가하고 계정을 허용 목록에 추가하다에 추가하는 경우. 연락처 [!DNL Google] 다음 정보를 입력하십시오.

* **계정 ID**: Google이 있는 Adobe의 계정 ID. 계정 ID: 87933855.
* **고객 ID**: Google이 있는 Adobe의 고객 계정 ID. 고객 ID: 89690775.
* 계정 유형: **애드워즈**
* **Google AdWords ID**: 이 ID는 와(과) 동일합니다. [!DNL Google]. ID 형식은 일반적으로 123-456-7890입니다.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

이 대상에 연결하려면 다음과같이 하십시오. [대상 구성 자습서](../../ui/connect-destination.md).

### 연결 매개변수 {#parameters}

While [설정 중](../../ui/connect-destination.md) 이 대상에는 다음 정보를 제공해야 합니다.

* **[!UICONTROL 이름]**: 이 대상의 기본 이름을 입력합니다.
* **[!UICONTROL 설명]**: 선택 사항입니다. 예를 들어 이 대상을 사용하는 캠페인을 언급할 수 있습니다.
* **[!UICONTROL 계정 유형]**: AdWords만 사용할 수 있습니다.
* **[!UICONTROL 계정 ID]**: 다음으로 계정 ID 입력 [!DNL Google Ads]. ID 형식은 일반적으로 123-456-7890입니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 다음 안내서를 참조하십시오. [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보를 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

다음을 참조하십시오 [대상 데이터를 스트리밍 대상 내보내기 대상으로 활성화](../../ui/activate-segment-streaming-destinations.md) 이 대상에 대한 대상자 활성화에 대한 지침을 참조하십시오.

## 내보낸 데이터

데이터가 성공적으로 로 내보내졌는지 확인하려면 [!DNL Google Ads] 대상, 다음을 확인: [!DNL Google Ads] 계정입니다. 활성화가 성공하면 계정에 대상자가 채워집니다.

## 문제 해결 {#troubleshooting}

### 400 잘못된 요청 오류 메시지 {#bad-request}

이 대상을 구성할 때 다음 오류가 표시될 수 있습니다.

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

이 오류는 고객 계정이 [전제 조건](#prerequisites) 또는 고객이 기존 항목 없이 대상을 구성하려고 할 때 [!DNL Google Ads] 계정입니다.

[!DNL Google] 더 이상 사용되지 않는 새로운 기능 포함 [!DNL Google Ads] 쿠키와 타사 공급업체의 통합. 다음을 수행하십시오. [허용 목록](#allow-listing) 단계, 와 기존의 통합이 있어야 합니다. [!DNL Google Ads].

사용에 대한 권장 접근 방식 [!DNL Google Ads] 을(를) 설정하는 중 [[!DNL Google Customer Match]](google-customer-match.md) 통합.
