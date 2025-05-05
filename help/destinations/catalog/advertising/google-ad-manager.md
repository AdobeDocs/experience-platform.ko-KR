---
keywords: google ad manager;google ad;doubleclick;DoubleClick AdX;DoubleClick;Google Ad Manager;Google ad manager; DFP
title: Google Ad Manager 연결
description: 이전에 DoubleClick for Publishers 또는 DoubleClick AdX로 알려졌던 Google Ad Manager는 게시자에게 웹 사이트, 비디오 및 모바일 앱에서 광고 표시를 관리하는 수단을 제공하는 Google의 광고 서비스 제공 플랫폼입니다.
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 7%

---

# [!DNL Google Ad Manager] 연결

>[!IMPORTANT]
>
> Google은 유럽 연합([EU 사용자 동의 정책](https://www.google.com/about/company/user-consent-policy/))의 [디지털 시장법](https://digital-markets-act.ec.europa.eu/index_en)&#x200B;(DMA)에 정의된 준수 및 동의 관련 요구 사항을 지원하기 위해 [Google Ads API](https://developers.google.com/google-ads/api/docs/start), [고객 일치](https://ads-developers.googleblog.com/2023/10/updates-to-customer-match-conversion.html) 및 [디스플레이 및 비디오 360 API](https://developers.google.com/display-video/api/guides/getting-started/overview)에 대한 변경 사항을 출시합니다. 동의 요구 사항에 대한 이러한 변경 사항의 시행은 2024년 3월 6일부터 시작됩니다.
><br/>
>EU 사용자 동의 정책을 준수하고 유럽 경제 영역(EEA)의 사용자에 대한 대상 목록을 계속 만들려면 광고주와 파트너는 대상 데이터를 업로드할 때 최종 사용자 동의를 전달하는지 확인해야 합니다. Google 파트너로서 Adobe는 유럽연합의 DMA에 따른 이러한 동의 요구 사항을 준수하는 데 필요한 도구를 제공합니다.
><br/>
>Adobe Privacy &amp; Security Shield를 구매하고 동의하지 않은 프로필을 필터링하도록 [동의 정책](../../../data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation)을(를) 구성한 고객은 별도의 조치를 취할 필요가 없습니다.
><br/>
>Adobe Privacy &amp; Security Shield를 구매하지 않은 고객은 [세그먼트 빌더](../../../segmentation/ui/segment-builder.md) 내의 [세그먼트 정의](../../../segmentation/home.md#segment-definitions) 기능을 사용하여 동의하지 않은 프로필을 필터링해야 기존 Real-Time CDP Google 대상을 중단 없이 계속 사용할 수 있습니다.


이전에 DFP([!DNL DoubleClick for Publishers]) 또는 [!DNL DoubleClick AdX]&#x200B;(으)로 알려졌던 [!DNL Google Ad Manager]은(는) 게시자에게 웹 사이트, 비디오 및 모바일 앱에서 광고 표시를 관리할 수 있는 수단을 제공하는 [!DNL Google]의 광고 제공 플랫폼입니다.

## 대상 세부 사항 {#specifics}

[!DNL Google Ad Manager] 대상에 해당하는 다음 세부 정보를 참고하십시오.

* 활성화된 대상은 [!DNL Google] 플랫폼에서 프로그래밍 방식으로 만들어집니다.
* [!DNL Experience Platform]은(는) 현재 성공적인 활성화를 확인하기 위한 측정 지표를 포함하지 않습니다. 통합의 유효성을 검사하고 대상 타깃팅 크기를 이해하려면 Google의 대상 수 를 참조하십시오.
* 대상을 [!DNL Google Ad Manager] 대상에 매핑하면 대상 이름이 [!DNL Google Ad Manager] 사용자 인터페이스에 바로 나타납니다.
* [!DNL Google Ad Manager]에 세그먼트 모집단을 표시하려면 24-48시간이 필요합니다. 또한 [!DNL Google Ad Manager]에 표시하려면 대상의 크기가 최소 50개 프로필이어야 합니다. 크기가 50개 프로필보다 작은 대상은 [!DNL Google Ad Manager]에서 채워지지 않습니다.

## 지원되는 ID {#supported-identities}

[!DNL Google Ad Manager]은(는) 아래 표에 표시된 ID를 기반으로 대상자 활성화를 지원합니다. [ID](/help/identity-service/features/namespaces.md)에 대해 자세히 알아보세요.

| ID | 설명 | 고려 사항 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] |  |
| IDFA | [!DNL Apple ID for Advertisers] |  |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=ko)&#x200B;(일명 [!DNL Device ID]). Audience Manager이 상호 작용하는 각 장치에 연결하는 숫자 38자리 장치 ID입니다. | Google은 [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=ko)을(를) 사용하여 캘리포니아에 있는 사용자를 타깃팅하고 다른 모든 사용자의 Google 쿠키 ID를 사용합니다. |
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

[!DNL Google Ad Manager]을(를) 사용하여 첫 번째 대상을 만들려고 하는데 이전에 Experience Cloud ID 서비스에서 [ID 동기화 기능](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html?lang=ko)을(를) 활성화하지 않은 경우(Audience Manager 또는 기타 응용 프로그램 사용) Adobe Consulting 또는 고객 지원 센터에 연락하여 ID 동기화를 활성화하십시오. 이전에 Audience Manager에서 [!DNL Google] 통합을 설정한 경우 설정한 ID 동기화가 Experience Platform으로 이월됩니다.

### 허용 목록 {#allow-listing}

Experience Platform에서 첫 번째 [!DNL Google Ad Manager] 대상을 설정하기 전에 허용 목록이 필수입니다. 대상을 만들기 전에 아래에 설명된 허용 목록 프로세스를 완료해야 합니다.

1. [Google Ad Manager 설명서](https://support.google.com/admanager/answer/3289669?hl=en)에 설명된 단계에 따라 Adobe을 연결된 데이터 관리 플랫폼(DMP)으로 추가합니다.
2. [!DNL Google Ad Manager] 인터페이스에서 **[!UICONTROL 관리자]** > **[!UICONTROL 전역 설정]** > **[!UICONTROL 네트워크 설정]**(으)로 이동하여 **[!UICONTROL API 액세스]** 슬라이더를 사용하도록 설정합니다.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오.

### 연결 매개변수 {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam_appendSegmentID"
>title="대상자 이름에 대상자 ID 추가"
>abstract="Google Ad Manager에서 대상자 이름에 다음과 같이 Experience Platform의 대상자 ID가 포함되도록 하려면 이 옵션을 선택하십시오. `Audience Name (Audience ID)`"

[이 대상을 설정](../../ui/connect-destination.md)하는 동안 다음 정보를 제공해야 합니다.

* **[!UICONTROL 이름]**: 이 대상의 기본 이름을 입력하십시오.
* **[!UICONTROL 설명]**: 선택 사항입니다. 예를 들어 이 대상을 사용하는 캠페인을 언급할 수 있습니다.
* **[!UICONTROL 계정 ID]**: [!DNL Google] 계정에서 [!DNL Audience Link ID]을(를) 입력하십시오. [!DNL Network code]이(가) 아닌 [!DNL Google Ad Manager] 네트워크와 연결된 특정 식별자입니다. [!DNL Google Ad Manager] 인터페이스의 **[!UICONTROL 관리자 > 전역 설정]**&#x200B;에서 찾을 수 있습니다.
* **[!UICONTROL 계정 유형]**: Google 계정에 따라 옵션을 선택하십시오.
   * 게시자에 대해 [!DNL DoubleClick]에 `DFP by Google` 사용
   * [!DNL Google AdX]에 `AdX buyer` 사용
* **[!UICONTROL 대상 이름에 대상 ID 추가]**: Google Ad Manager의 대상 이름에 다음과 같이 Experience Platform의 대상 ID가 포함되도록 하려면 이 옵션을 선택하십시오. `Audience Name (Audience ID)`.

>[!NOTE]
>
>[!DNL Google Ad Manager] 대상을 설정할 때 [!DNL Google Account Manager] 또는 Adobe 담당자와 협력하여 보유한 계정 유형을 파악하십시오.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 모두 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 대한 대상 활성화에 대한 지침은 [대상 데이터를 스트리밍 대상 내보내기 대상으로 활성화](../../ui/activate-segment-streaming-destinations.md)를 참조하십시오.

## 내보낸 데이터 {#exported-data}

데이터를 [!DNL Google Ad Manager] 대상으로 내보냈는지 확인하려면 [!DNL Google Ad Manager] 계정을 확인하세요. 활성화가 성공하면 계정에 대상자가 채워집니다.

## 문제 해결 {#troubleshooting}

이 대상을 사용하는 동안 오류가 발생하여 Adobe 또는 Google에 연결해야 하는 경우 다음 ID를 즉시 사용하십시오.

Adobe의 Google 계정 ID입니다.

* **[!UICONTROL 계정 ID]**: 87933855
* **[!UICONTROL 고객 ID]**: 89690775