---
title: Google Display & Video 360 연결
description: 이전에 DoubleClick Bid Manager로 알려졌던 Display & Video 360은 디스플레이, 비디오 및 모바일 인벤토리 소스에 걸쳐 리타겟팅 및 대상자 타겟팅 디지털 캠페인을 실행하는 데 사용되는 도구입니다.
exl-id: bdd3b3fd-891f-44ec-bd47-daf7f3289f92
source-git-commit: 7d43abd507b5cee2b5c5d90af253d3e9290013a2
workflow-type: tm+mt
source-wordcount: '1158'
ht-degree: 2%

---

# [!DNL Google Display & Video 360] 연결

>[!IMPORTANT]
>
> Google은 의 변경 사항을 [Google Ads API](https://developers.google.com/google-ads/api/docs/start), [고객 일치](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html)및 [디스플레이 및 비디오 360 API](https://developers.google.com/display-video/api/guides/getting-started/overview) 아래에 정의된 준수 및 동의 관련 요구 사항을 지원하기 위해 [디지털 시장법](https://digital-markets-act.ec.europa.eu/index_en) 유럽 연합의 (DMA)[EU 사용자 동의 정책](https://www.google.com/about/company/user-consent-policy/)). 이러한 동의 요건 변경의 시행은 2024년 3월 6일부터 시행될 예정이다.
><br/>
>EU 사용자 동의 정책을 준수하고 유럽 경제 영역(EEA)의 사용자에 대한 대상 목록을 계속 만들려면 광고주와 파트너는 대상 데이터를 업로드할 때 최종 사용자 동의를 전달하는지 확인해야 합니다. Google 파트너인 Adobe은 유럽 연합의 DMA에 따라 이러한 동의 요구 사항을 준수하는 데 필요한 도구를 제공합니다.
><br/>
>Adobe 개인 정보 보호 및 보안 쉴드를 구매하고 [동의 정책](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) 동의하지 않은 프로필을 필터링하려면 별도의 조치를 취할 필요가 없습니다.
><br/>
>Adobe Privacy &amp; Security Shield를 구매하지 않은 고객은 [세그먼트 정의](../../../segmentation/home.md#segment-definitions) 내 기능 [세그먼트 빌더](../../../segmentation/ui/segment-builder.md) 기존 Real-Time CDP Google 대상을 중단 없이 계속 사용할 수 있도록 동의하지 않은 프로필을 필터링합니다.

[!DNL Display & Video 360], 이전에 [!DNL DoubleClick Bid Manager]는 디스플레이, 비디오 및 모바일 인벤토리 소스에 걸쳐 리타겟팅 및 대상자 타겟팅 디지털 캠페인을 실행하는 데 사용되는 도구입니다.

## 대상 세부 사항 {#specifics}

다음의 세부 사항에 유의하십시오. [!DNL Google Display & Video 360] 대상:

* 활성화된 대상은 Google 플랫폼에서 프로그래밍 방식으로 생성됩니다.
* 에 대한 대상 다시 채우기 활성화 [!DNL Google Display & Video 360] 대상은 대상이 대상 연결에 처음 매핑되고 24-48시간 후에 발생하도록 예약되어 있습니다. 이 업데이트는 데이터를 수집할 때까지 24시간 대기하는 Google의 정책에 대한 응답이며 Real-Time CDP과 간의 일치율을 향상시키기 위한 것입니다 [!DNL Google Display & Video 360]. 이는 이 대상에만 적용할 수 있는 백엔드 구성이며 UI의 고객이 구성할 수 있는 예약 옵션과 관련이 없습니다.

>[!IMPORTANT]
>
>Google Display &amp; Video 360으로 첫 번째 대상을 만들려고 하는데 [ID 동기화 기능](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) 과거 Experience Cloud ID 서비스(Adobe Audience Manager 또는 기타 애플리케이션 포함)에서 ID 동기화를 활성화하려면 Adobe 컨설팅 또는 고객 지원 센터에 문의하십시오. 이전에 Audience Manager에서 Google 통합을 설정한 경우 설정한 ID가 플랫폼으로 이월됩니다.

## 지원되는 ID {#supported-identities}

[!DNL Google Display & Video 360] 는 아래 표에 표시된 id를 기반으로 대상의 활성화를 지원합니다. 자세히 알아보기 [id](/help/identity-service/features/namespaces.md).

| 신원 | 설명 | 고려 사항 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] |  |
| IDFA | [!DNL Apple ID for Advertisers] |  |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html)라고도 함 [!DNL Device ID]. Audience Manager이 상호 작용하는 각 장치에 연결하는 숫자 38자리 장치 ID입니다. | Google 사용 [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html) Google 를 사용하십시오. |
| [!DNL Google] 쿠키 ID | [!DNL Google] 쿠키 ID | [!DNL Google] 은 이 ID를 사용하여 캘리포니아 외부의 사용자를 타깃팅합니다. |
| 리다 | Advertising용 Roku ID. 이 ID는 Roku 장치를 고유하게 식별합니다. |  |
| 하녀 | Microsoft 광고 ID. 이 ID는 Windows 10을 실행하는 장치를 고유하게 식별합니다. |  |
| Amazon Fire TV ID | 이 ID는 Amazon Fire TV를 고유하게 식별합니다. |  |

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

## 전제 조건 {#prerequisites}

### 허용 목록 {#allow-listing}

>[!NOTE]
>
>첫 번째 항목을 설정하기 전에 허용 목록은 필수입니다. [!DNL Google Display & Video 360] 대상(플랫폼 내) 아래 설명된 허용 목록 프로세스가 다음 기한까지 완료되었는지 확인합니다. [!DNL Google] 대상을 만들기 전에.
>이 규칙의 예외는 다음과 같습니다 [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html) 고객. Audience Manager에서 이 Google 대상에 대한 연결을 이미 만든 경우 허용 목록 프로세스를 다시 진행할 필요가 없으며 다음 단계를 진행할 수 있습니다.

만들기 전에 [!DNL Google Display & Video 360] destination in Platform에서는 Google에 문의하여 허용된 데이터 공급자 목록에 Adobe허용 목록에 추가하다 을 넣고 계정에 계정을 추가해야 합니다. Google에 연락하여 다음 정보를 제공하십시오.

* **계정 ID**: Google이 있는 Adobe의 계정 ID. 계정 ID: 87933855.
* **고객 ID**: Google이 있는 Adobe의 고객 계정 ID. 고객 ID: 89690775.
* **내 계정 유형**: 사용 **[!DNL Invite advertiser]** Display &amp; Video 360 계정 또는 사용에서 대상을 특정 브랜드와만 공유할 수 있도록 허용 **[!DNL Invite partner]** Display &amp; Video 360 계정의 모든 브랜드에 대상을 공유할 수 있도록 하려는 경우.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

이 대상에 연결하려면 다음과같이 하십시오. [대상 구성 자습서](../../ui/connect-destination.md).

### 연결 매개변수 {#parameters}

While [설정 중](../../ui/connect-destination.md) 이 대상에는 다음 정보를 제공해야 합니다.

* **[!UICONTROL 이름]**: 이 대상의 기본 이름을 입력합니다.
* **[!UICONTROL 설명]**: 선택 사항입니다. 예를 들어 이 대상을 사용하는 캠페인을 언급할 수 있습니다.
* **[!UICONTROL 계정 유형]**: Google의 계정에 따라 옵션을 선택합니다.
   * 사용 `Invite Advertiser` Display &amp; Video 360 계정의 특정 브랜드에만 대상을 공유할 수 있도록 허용합니다.
   * 사용 `Invite Partner` Display &amp; Video 360 계정의 모든 브랜드에 대상을 공유할 수 있도록 하려는 경우.
* **[!UICONTROL 계정 ID]**: 다음을 입력합니다. **[!DNL Invite partner]** 또는 **[!DNL Invite advertiser]** Google의 계정 ID. 일반적으로 6자리 또는 7자리 ID입니다.

>[!NOTE]
>
>를 설정할 때 [!DNL Google Display & Video 360] 대상, 다음 사용자와 작업 [!DNL Google Account Manager] 또는 Adobe 담당자를 통해 보유하고 있는 계정 유형을 파악할 수 있습니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 다음 안내서를 참조하십시오. [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보를 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

다음을 참조하십시오 [대상 데이터를 스트리밍 대상 내보내기 대상으로 활성화](../../ui/activate-segment-streaming-destinations.md) 이 대상에 대한 대상자 활성화에 대한 지침을 참조하십시오.

## 내보낸 데이터

데이터가 성공적으로 로 내보내졌는지 확인하려면 [!DNL Google Display & Video 360] 대상, 다음을 확인: [!DNL Google Display & Video 360] 계정입니다. 활성화가 성공하면 계정에 대상자가 채워집니다.

## 문제 해결 {#troubleshooting}

### 400 잘못된 요청 오류 메시지 {#bad-request}

이 대상을 구성할 때 다음 오류가 표시될 수 있습니다.

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

이 오류는 고객 계정이 [전제 조건](#prerequisites). 이 문제를 해결하려면 Google에 연락하여 계정이 허용 목록에 추가되었는지 확인하십시오.