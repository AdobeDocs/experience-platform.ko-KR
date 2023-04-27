---
keywords: DoubleClick 입찰 관리자;DoubleClick 입찰 관리자;DoubleClick;Display & Video 360;디스플레이 360;비디오 360;비디오 360;디스플레이 360;디스플레이 및 비디오
title: Google 디스플레이 및 비디오 360 연결
description: 이전에 DoubleClick Bid Manager라고 알려진 Display & Video 360은 디스플레이, 비디오 및 모바일 인벤토리 소스에서 재타겟팅하고 대상 지정 디지털 캠페인을 실행하는 데 사용되는 도구입니다.
exl-id: bdd3b3fd-891f-44ec-bd47-daf7f3289f92
source-git-commit: 326127996a27df41383ef67da765f7b0818f17f2
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 2%

---

# [!DNL Google Display & Video 360] 연결

## 개요 {#overview}

[!DNL Display & Video 360]이전에는 [!DNL DoubleClick Bid Manager]는 디스플레이, 비디오 및 모바일 인벤토리 소스에서 재타겟팅되고 대상 타겟팅된 디지털 캠페인을 실행하는 데 사용되는 도구입니다.

## 대상 세부 사항 {#specifics}

에 해당하는 다음 세부 사항을 참고하십시오 [!DNL Google Display & Video 360] 대상:

* 활성화된 대상은 Google 플랫폼에서 프로그래밍 방식으로 생성됩니다.
* 대상 백칠이 [!DNL Google Display & Video 360] 대상이 세그먼트가 대상 연결에 처음 매핑되면 24-48시간 후에 발생하도록 예약되었습니다. 이 업데이트는 데이터를 수집할 때까지 24시간을 대기하는 Google의 정책에 응답하며 실시간 CDP와 [!DNL Google Display & Video 360]. 이 구성은 이 대상에만 적용할 수 있는 백엔드 구성이며 UI의 고객 구성 가능한 예약 옵션과 관련이 없습니다.

>[!IMPORTANT]
>
>Google Display &amp; Video 360을 사용하여 첫 번째 대상을 만들고 를 활성화하지 않은 경우 [ID 동기화 기능](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) 과거(Adobe Audience Manager 또는 다른 애플리케이션 사용) Experience Cloud ID 서비스에서 ID 동기화를 활성화하려면 Adobe 컨설팅 또는 고객 지원 센터에 문의하십시오. 이전에 Audience Manager에서 Google 통합을 설정한 경우 설정한 ID 동기화가 Platform으로 전달됩니다.

## 지원되는 ID {#supported-identities}

[!DNL Google Display & Video 360] 은 아래 표에 설명된 id의 활성화를 지원합니다.

| Target ID | 설명 | 고려 사항 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | 소스 ID가 GAID 네임스페이스이면 이 대상 ID를 선택합니다. |
| IDFA | [!DNL Apple ID for Advertisers] | 소스 ID가 IDFA 네임스페이스인 경우 이 타겟 ID를 선택합니다. |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html)라고도 함 [!DNL Device ID]. Audience Manager이 상호 작용하는 각 장치에 연결하는 38자리 숫자 장치 ID입니다. | Google 사용 [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=ko-KR) 를 사용 중인지 여부에 따라 Google 쿠키 ID가 다른 모든 사용자를 타깃팅하려면 를 사용해야 합니다. |
| [!DNL Google] 쿠키 ID | [!DNL Google] 쿠키 ID | [!DNL Google] 는 이 ID를 사용하여 캘리포니아 외부의 사용자를 타깃팅합니다. |
| RIDA | 광고용 Roku ID. 이 ID는 Roku 장치를 고유하게 식별합니다. |  |
| 가정부 | Microsoft 광고 ID. 이 ID는 Windows 10을 실행하는 장치를 고유하게 식별합니다. |  |
| Amazon Fire TV ID | 이 ID는 Amazon Fire TV를 고유하게 식별합니다. |  |

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 세그먼트 내보내기]** | 세그먼트(대상)의 모든 구성원을 Google 대상으로 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상 설정&quot; API 기반 연결입니다. 세그먼트 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터는 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

## 사전 요구 사항 {#prerequisites}

### 허용 목록 {#allow-listing}

>[!NOTE]
>
>첫 번째 목록을 설정하기 전에 허용 목록이 필수입니다 [!DNL Google Display & Video 360] 대상 을 참조하십시오. 아래 설명된 허용 목록 프로세스가 [!DNL Google] 대상을 만들기 전에
>이 규칙의 예외는 입니다 [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html) 고객. Audience Manager에서 이 Google 대상에 이미 연결을 만든 경우 허용 목록 프로세스를 다시 진행할 필요가 없으며 다음 단계를 계속 진행할 수 있습니다.

만들기 전 [!DNL Google Display & Video 360] Platform의 대상은 Google에 연락하여 Adobe이 허용된 데이터 공급자 목록에 추가되도록 하고, 계정을 허용 목록에 추가하도록 요청해야 합니다. Google에 문의하여 다음 정보를 제공하십시오.

* **계정 ID**: Adobe의 계정 ID와 Google. 계정 ID: 87933855.
* **고객 ID**: Google을 사용하는 Adobe의 고객 계정 ID입니다. 고객 ID: 89690775.
* **계정 유형**: 사용 **[!DNL Invite advertiser]** Display &amp; Video 360 계정에서 특정 브랜드에만 대상을 공유할 수 있도록 하거나 **[!DNL Invite partner]** 디스플레이 및 비디오 360 계정의 모든 브랜드에 대상을 공유할 수 있도록 허용합니다.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md).

### 연결 매개 변수 {#parameters}

While [설정](../../ui/connect-destination.md) 이 대상을 사용하려면 다음 정보를 제공해야 합니다.

* **[!UICONTROL 이름]**: 이 대상의 기본 이름을 입력합니다.
* **[!UICONTROL 설명]**: 선택 사항입니다. 예를 들어 이 대상을 사용하는 캠페인을 언급할 수 있습니다.
* **[!UICONTROL 계정 유형]**: Google을 사용하는 계정에 따라 옵션을 선택합니다.
   * 사용 `Invite Advertiser` Display &amp; Video 360 계정의 특정 브랜드에만 대상을 공유할 수 있도록 하는 것입니다.
   * 사용 `Invite Partner` 디스플레이 및 비디오 360 계정의 모든 브랜드에 대상을 공유할 수 있도록 허용합니다.
* **[!UICONTROL 계정 ID]**: 을 입력합니다. **[!DNL Invite partner]** 또는 **[!DNL Invite advertiser]** 계정 ID(Google 포함). 일반적으로 6자리 또는 7자리 ID입니다.

>[!NOTE]
>
>설정 시 [!DNL Google Display & Video 360] 대상: [!DNL Google Account Manager] 또는 Adobe 담당자에게 문의하십시오.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상으로 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보 제공을 마치면 를 선택합니다 **[!UICONTROL 다음]**.

## 세그먼트를 이 대상에 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

자세한 내용은 [스트리밍 세그먼트 내보내기 대상으로 대상 데이터 활성화](../../ui/activate-segment-streaming-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

## 내보낸 데이터

데이터를 로 성공적으로 내보냈는지 확인하려면 [!DNL Google Display & Video 360] 대상, [!DNL Google Display & Video 360] 계정이 필요합니다. 활성화가 성공하면 계정에 대상이 채워집니다.

## 문제 해결 {#troubleshooting}

### 400 잘못된 요청 오류 메시지 {#bad-request}

이 대상을 구성할 때 다음 오류가 표시될 수 있습니다.

`{"message":"Google Error: AuthorizationError.USER_PERMISSION_DENIED","code":"400 BAD_REQUEST"}`

이 오류는 고객 계정이 [전제 조건](#prerequisites). 이 문제를 해결하려면 Google에 문의하여 계정이 허용 목록에 추가되었는지 확인하십시오.