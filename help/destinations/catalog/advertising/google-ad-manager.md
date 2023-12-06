---
keywords: google ad manager;google ad;doubleclick;DoubleClick AdX;DoubleClick;Google Ad Manager;Google ad manager; DFP
title: Google Ad Manager 연결
description: 이전에 DoubleClick for Publishers 또는 DoubleClick AdX로 알려졌던 Google Ad Manager는 게시자에게 웹 사이트, 비디오 및 모바일 앱에서 광고 표시를 관리하는 수단을 제공하는 Google의 광고 서비스 제공 플랫폼입니다.
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: a7dbb5e274058a059ae1231281fd9efd509b029f
workflow-type: tm+mt
source-wordcount: '938'
ht-degree: 5%

---

# [!DNL Google Ad Manager] 연결

## 개요 {#overview}

[!DNL Google Ad Manager], 이전에 [!DNL DoubleClick for Publishers] (DFP) 또는 [!DNL DoubleClick AdX]는 의 광고 서비스 제공 플랫폼입니다 [!DNL Google] 이는 게시자에게 비디오와 모바일 앱을 통해 웹 사이트의 광고 표시를 관리할 수 있는 수단을 제공합니다.

## 대상 세부 사항 {#specifics}

다음의 세부 사항에 유의하십시오. [!DNL Google Ad Manager] 대상:

* 활성화된 대상은에서 프로그래밍 방식으로 만들어집니다. [!DNL Google] 플랫폼.
* [!DNL Platform] 현재 성공적인 활성화를 확인하기 위한 측정 지표는 포함되어 있지 않습니다. 통합의 유효성을 검사하고 대상 타깃팅 크기를 이해하려면 Google의 대상 수 를 참조하십시오.
* 대상자를 다음에 매핑 [!DNL Google Ad Manager] 대상, 대상 이름이 [!DNL Google Ad Manager] 사용자 인터페이스.
* 세그먼트 모집단을 표시하려면 24-48시간이 필요합니다. [!DNL Google Ad Manager]. 또한 대상자에는에서 표시되려면 대상 크기가 최소 50개의 프로필이어야 합니다 [!DNL Google Ad Manager]. 크기가 50개 프로필보다 작은 대상은에서 채워지지 않습니다. [!DNL Google Ad Manager].

## 지원되는 ID {#supported-identities}

[!DNL Google Ad Manager] 는 아래 표에 표시된 id를 기반으로 대상의 활성화를 지원합니다. 자세히 알아보기 [id](/help/identity-service/namespaces.md).

| 신원 | 설명 | 고려 사항 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] |  |
| IDFA | [!DNL Apple ID for Advertisers] |  |
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

을(를) 사용하여 첫 번째 대상을 만들려는 경우 [!DNL Google Ad Manager] 및 이(가) 을(를) 활성화하지 않음 [ID 동기화 기능](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) 과거의 Experience Cloud ID 서비스(Audience Manager 또는 기타 애플리케이션 포함)에서 ID 동기화를 활성화하려면 Adobe 컨설팅 또는 고객 지원 센터에 문의하십시오. 이전에 을 설정한 경우 [!DNL Google] Audience Manager의 통합, 설정한 ID 동기화를 플랫폼으로 이월합니다.

### 허용 목록 {#allow-listing}

첫 번째 항목을 설정하기 전에 허용 목록은 필수입니다. [!DNL Google Ad Manager] 대상(플랫폼 내) 대상을 만들기 전에 아래에 설명된 허용 목록 프로세스를 완료해야 합니다.

1. 다음에 설명된 단계를 수행합니다. [Google Ad Manager 설명서](https://support.google.com/admanager/answer/3289669?hl=en) Adobe을 연결된 DMP(데이터 관리 플랫폼)로 추가합니다.
2. 다음에서 [!DNL Google Ad Manager] 인터페이스, 이동 **[!UICONTROL 관리자]** > **[!UICONTROL 전역 설정]** > **[!UICONTROL 네트워크 설정]**, 및 활성화 **[!UICONTROL API 액세스]** 슬라이더.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

이 대상에 연결하려면 다음과같이 하십시오. [대상 구성 자습서](../../ui/connect-destination.md).

### 연결 매개변수 {#parameters}

>[!CONTEXTUALHELP]
>id="platform_destinations_gam_appendSegmentID"
>title="대상자 이름에 대상자 ID 추가"
>abstract="Google Ad Manager에서 대상자 이름에 다음과 같이 Experience Platform의 대상자 ID가 포함되도록 하려면 이 옵션을 선택하십시오. `Audience Name (Audience ID)`"

While [설정 중](../../ui/connect-destination.md) 이 대상에는 다음 정보를 제공해야 합니다.

* **[!UICONTROL 이름]**: 이 대상의 기본 이름을 입력합니다.
* **[!UICONTROL 설명]**: 선택 사항입니다. 예를 들어 이 대상을 사용하는 캠페인을 언급할 수 있습니다.
* **[!UICONTROL 계정 ID]**: 다음을 입력합니다. [!DNL Audience Link ID] (으)로부터 [!DNL Google] 계정입니다. 와 연관된 특정 식별자입니다. [!DNL Google Ad Manager] 네트워크(네트워크 아님) [!DNL Network code]). 아래에서 찾을 수 있습니다. **[!UICONTROL 관리자 > 전역 설정]** 다음에서 [!DNL Google Ad Manager] 인터페이스.
* **[!UICONTROL 계정 유형]**: Google의 계정에 따라 옵션을 선택합니다.
   * 사용 `DFP by Google` 대상 [!DNL DoubleClick] 게시자용
   * 사용 `AdX buyer` 대상 [!DNL Google AdX]
* **[!UICONTROL 대상 이름에 대상 ID 추가]**: Google Ad Manager의 대상 이름에 다음과 같이 Experience Platform의 대상 ID가 포함되도록 하려면 이 옵션을 선택합니다. `Audience Name (Audience ID)`.

>[!NOTE]
>
>를 설정할 때 [!DNL Google Ad Manager] 대상, (으)로 작업 [!DNL Google Account Manager] 또는 Adobe 담당자를 통해 보유하고 있는 계정 유형을 파악할 수 있습니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 다음 안내서를 참조하십시오. [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보를 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

다음을 참조하십시오 [대상 데이터를 스트리밍 대상 내보내기 대상으로 활성화](../../ui/activate-segment-streaming-destinations.md) 이 대상에 대한 대상자 활성화에 대한 지침을 참조하십시오.

## 내보낸 데이터 {#exported-data}

데이터가 성공적으로 로 내보내졌는지 확인하려면 [!DNL Google Ad Manager] 대상, 다음을 확인: [!DNL Google Ad Manager] 계정입니다. 활성화가 성공하면 계정에 대상자가 채워집니다.

## 문제 해결 {#troubleshooting}

이 대상을 사용하는 동안 오류가 발생하여 Adobe 또는 Google에 연결해야 하는 경우 다음 ID를 즉시 사용하십시오.

Adobe의 Google 계정 ID입니다.

* **[!UICONTROL 계정 ID]**: 87933855
* **[!UICONTROL 고객 ID]**: 89690775