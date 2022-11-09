---
keywords: google ad manager;google ad;doubleclick;DoubleClick AdX;DoubleClick;Google Ad Manager;Google 광고 관리자; DFP
title: Google Ad Manager 연결
description: 이전에 DoubleClick for Publishers 또는 DoubleClick AdX라고 알려진 Google Ad Manager는 비디오 및 모바일 앱을 통해 게시자가 웹 사이트에서 광고를 표시할 수 있는 방법을 제공하는 Google의 광고 서비스 플랫폼입니다.
exl-id: e93f1bd5-9d29-43a1-a9a6-8933f9d85150
source-git-commit: 94cd05ca8b5c8331b1b49e5172daf499918d2320
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 3%

---

# [!DNL Google Ad Manager] 연결

## 개요 {#overview}

[!DNL Google Ad Manager]이전에는 [!DNL DoubleClick for Publishers] (DFP) 또는 [!DNL DoubleClick AdX]는 의 광고 서비스 플랫폼입니다. [!DNL Google] 이를 통해 게시자는 비디오 및 모바일 앱을 통해 웹 사이트에서 광고 표시를 관리할 수 있습니다.

## 대상 세부 사항 {#specifics}

에 해당하는 다음 세부 사항을 참고하십시오 [!DNL Google Ad Manager] 대상:

* 활성화된 대상은 프로그래밍 방식으로 [!DNL Google] 플랫폼.
* [!DNL Platform] 현재 에는 성공적인 활성화를 확인하기 위한 측정 지표가 포함되어 있지 않습니다. 통합의 유효성을 확인하고 대상 타깃팅 크기를 이해하려면 Google의 대상 카운트를 참조하십시오.
* 세그먼트를 [!DNL Google Ad Manager] 대상, 세그먼트 이름이 [!DNL Google Ad Manager] 사용자 인터페이스.
* 세그먼트 모집단에 표시되려면 24-48시간이 필요합니다 [!DNL Google Ad Manager]. 또한 세그먼트를 표시하려면 대상 크기가 50개 이상인 프로필이어야 합니다 [!DNL Google Ad Manager]. 대상 크기가 50보다 작은 세그먼트는 [!DNL Google Ad Manager].

## 지원되는 ID {#supported-identities}

[!DNL Google Ad Manager] 은 아래 표에 설명된 id의 활성화를 지원합니다.

| Target ID | 설명 | 고려 사항 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | 소스 ID가 GAID 네임스페이스이면 이 대상 ID를 선택합니다. |
| IDFA | [!DNL Apple ID for Advertisers] | 소스 ID가 IDFA 네임스페이스인 경우 이 타겟 ID를 선택합니다. |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html)라고도 함 [!DNL Device ID]. Audience Manager이 상호 작용하는 각 장치에 연결하는 38자리 숫자 장치 ID입니다. | Google 사용 [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en) 를 사용 중인지 여부에 따라 Google 쿠키 ID가 다른 모든 사용자를 타깃팅하려면 를 사용해야 합니다. |
| [!DNL Google] 쿠키 ID | [!DNL Google] 쿠키 ID | [!DNL Google] 는 이 ID를 사용하여 캘리포니아 외부의 사용자를 타깃팅합니다. |
| RIDA | 광고용 Roku ID. 이 ID는 Roku 장치를 고유하게 식별합니다. |  |
| 가정부 | Microsoft 광고 ID. 이 ID는 Windows 10을 실행하는 장치를 고유하게 식별합니다. |  |
| Amazon Fire TV ID | 이 ID는 Amazon Fire TV를 고유하게 식별합니다. |  |

{style=&quot;table-layout:auto&quot;}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 세그먼트 내보내기]** | 세그먼트(대상)의 모든 구성원을 Google 대상으로 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상 설정&quot; API 기반 연결입니다. 세그먼트 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터는 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## 전제 조건 {#prerequisites}

을 사용하여 첫 번째 대상을 만들려면 [!DNL Google Ad Manager] 및 [ID 동기화 기능](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) 과거(Audience Manager 또는 기타 애플리케이션 포함)에 Experience Cloud ID 서비스에서 ID 동기화를 활성화하려면 Adobe 컨설팅 또는 고객 지원 센터에 문의하십시오. 이전에 설정한 경우 [!DNL Google] 통합에서 설정한 ID 동기화를 Platform으로 이월합니다.

### 허용 목록 {#allow-listing}

>[!NOTE]
>
>첫 번째 목록을 설정하기 전에 허용 목록이 필수입니다 [!DNL Google Ad Manager] 대상 을 참조하십시오. 아래 설명된 허용 목록 프로세스가 [!DNL Google] 대상을 만들기 전에
>이 규칙의 예외는 입니다 [Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/aam-home.html) 고객. Audience Manager에서 이 Google 대상에 이미 연결을 만든 경우 허용 목록 프로세스를 다시 진행할 필요가 없으며 다음 단계를 계속 진행할 수 있습니다.

만들기 전 [!DNL Google Ad Manager] 플랫폼의 대상은 [!DNL Google] Adobe이 허용된 데이터 공급자 목록에 추가되고 허용 목록에 계정이 추가되도록 하는 경우입니다. 연락처 [!DNL Google] 및 는 다음 정보를 제공합니다.

* **계정 ID**: Adobe의 계정 ID와 Google. 계정 ID: 87933855.
* **고객 ID**: Google을 사용하는 Adobe의 고객 계정 ID입니다. 고객 ID: 89690775.
* **네트워크 코드**: 이건 네 거야 [!DNL Google Ad Manager] 네트워크 ID에 있습니다. **[!UICONTROL 관리자 > 전역 설정]** 뿐만 아니라 URL에도 포함되어 있습니다.
* **대상 링크 ID**: 와 관련된 특정 식별자입니다 [!DNL Google Ad Manager] 네트워크(아님) [!DNL Network code]), 에도 있습니다. **[!UICONTROL 관리자 > 전역 설정]** ( Google 인터페이스)를 참조하십시오.
* 계정 유형입니다. Google 또는 AdX 구매자의 DFP.

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
   * 사용 `DFP by Google` 대상 [!DNL DoubleClick] 게시자
   * 사용 `AdX buyer` 대상 [!DNL Google AdX]
* **[!UICONTROL 계정 ID]**: 대상 링크 ID를 [!DNL Google].

>[!NOTE]
>
>설정 시 [!DNL Google Ad Manager] 대상: [!DNL Google Account Manager] 또는 Adobe 담당자에게 문의하십시오.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상으로 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보 제공을 마치면 를 선택합니다 **[!UICONTROL 다음]**.

## 세그먼트를 이 대상에 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

자세한 내용은 [스트리밍 세그먼트 내보내기 대상으로 대상 데이터 활성화](../../ui/activate-segment-streaming-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

## 내보낸 데이터 {#exported-data}

데이터를 로 성공적으로 내보냈는지 확인하려면 [!DNL Google Ad Manager] 대상, [!DNL Google Ad Manager] 계정이 필요합니다. 활성화가 성공하면 계정에 대상이 채워집니다.
