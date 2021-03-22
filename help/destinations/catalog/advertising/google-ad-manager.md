---
keywords: google 광고 관리자;google ad;doubleclick;DoubleClick AdX;DoubleClick;Google 광고 관리자;Google 광고 관리자;google ad manager;google ad manager
title: Google 광고 관리자 연결
description: '이전에 발행자를 위한 DoubleClick 또는 DoubleClick AdX로 알려졌던 Google Ad Manager는 발행자가 비디오 및 모바일 앱을 통해 자사 웹 사이트의 광고 표시를 관리할 수 있는 수단을 제공하는 Google의 광고 서비스 플랫폼입니다.  '
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 0%

---


# [!DNL Google Ad Manager] 연결

## 개요 {#overview}

[!DNL Google Ad Manager]이전에 게시자 또 [!DNL DoubleClick] 는 [!DNL DoubleClick AdX]는 [!DNL Google] 는 광고 표시를 발행자에게 자사 웹 사이트, 비디오 및 모바일 앱을 통해 관리할 수있는 수단을 제공하는 광고 서비스 플랫폼입니다.

## 대상 사양

[!DNL Google Ad Manager] 대상에 대한 다음 세부 정보를 참조하십시오.

* 활성화된 대상은 [!DNL Google] 플랫폼에서 프로그래밍 방식으로 생성됩니다.
* 현재 플랫폼에 성공적인 활성화를 확인할 측정 지표가 포함되어 있지 않습니다. 통합을 확인하고 대상 타깃팅 크기를 이해하려면 Google의 대상 수를 참조하십시오.

>[!IMPORTANT]
>
>[!DNL Google Ad Manager]을(를) 사용하여 첫 번째 대상을 만들고 이전에 Experience Cloud ID 서비스에서 [ID 동기화 기능](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html)을(를) 활성화하지 않은 경우(Audience Manager 또는 다른 응용 프로그램 포함) Adobe 컨설팅 또는 고객 지원 센터에 문의하여 ID 동기화를 활성화하십시오. 이전에 Audience Manager에서 [!DNL Google] 통합을 설정한 경우 설정한 ID 동기화가 플랫폼으로 이월됩니다.

## 지원되는 ID {#supported-identities}

[!DNL Google Ad Manager] 에서는 아래 표에 설명된 ID 활성화를 지원합니다.

| Target ID | 설명 | 고려 사항 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | 소스 ID가 GAID 네임스페이스인 경우 이 대상 ID를 선택합니다. |
| IDFA | [!DNL Apple ID for Advertisers] | 소스 ID가 IDFA 네임스페이스인 경우 이 대상 ID를 선택합니다. |
| AAM UUID | [Adobe Audience Manager [!DNL Unique User ID]](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html)(라고도 함) [!DNL Device ID]. Audience Manager이 상호 작용하는 각 장치에 연결하는 38자리 숫자 장치 ID입니다. | Google은 [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en)를 사용하여 캘리포니아에 있는 사용자를 타게팅하고 다른 모든 사용자에 대해 Google 쿠키 ID를 사용합니다. |
| [!DNL Google] 쿠키 ID | [!DNL Google] 쿠키 ID | [!DNL Google] 이 ID를 사용하여 캘리포니아 외부의 사용자를 타깃팅합니다. |
| RIDA | 광고에 대한 Roku ID. 이 ID는 Roku 장치를 고유하게 식별합니다. |  |
| 가정부 | Microsoft 광고 ID. 이 ID는 Windows 10을 실행하는 장치를 고유하게 식별합니다. |  |
| Amazon Fire TV ID | 이 ID는 Amazon Fire TV를 고유하게 식별합니다. |  |

## 내보내기 유형 {#export-type}

**세그먼트 내보내기**  - 세그먼트(대상)의 모든 구성원을 Google 대상으로 내보냅니다.

## 전제 조건

### 허용 목록

>[!NOTE]
>
>플랫폼에서 첫 번째 [!DNL Google Ad Manager] 대상을 설정하기 전에 허용 목록은 필수입니다. 대상을 만들기 전에 아래에 설명된 허용 목록 프로세스가 [!DNL Google]에 의해 완료되었는지 확인하십시오.

플랫폼에서 [!DNL Google Ad Manager] 대상을 만들기 전에 허용되는 데이터 공급자 목록에 Adobe을 배치하고 허용 목록에 계정을 추가하려면 [!DNL Google]에 문의해야 합니다. [!DNL Google]에 연락하여 다음 정보를 제공합니다.

* **계정 ID** :Adobe 계정 ID입니다 [!DNL Google]. 이 ID를 얻으려면 Adobe 고객 지원 센터 또는 Adobe 담당자에게 문의하십시오.
* **고객 ID** :Adobe의 고객 계정 ID입니다 [!DNL Google]. 이 ID를 얻으려면 Adobe 고객 지원 센터 또는 Adobe 담당자에게 문의하십시오.
* **네트워크 ID** :이 계정은  [!DNL Google Ad Manager]
* **대상 링크 ID** :이 계정은  [!DNL Google Ad Manager]
* 계정 유형. Google 또는 AdX 구매자의 DFP.

## 대상 구성

**[!UICONTROL Connections]** > **[!UICONTROL Destinations]**&#x200B;에서 **[!DNL Google Ad Manager]**&#x200B;를 선택하고 **[!UICONTROL Configure]**&#x200B;을 선택합니다.

![Google 광고 관리자 대상 연결](../../assets/catalog/advertising/google-ad-manager/catalog.png)

>[!NOTE]
>
>이 대상과의 연결이 이미 있는 경우 대상 카드에 **[!UICONTROL Activate]** 단추가 표시될 수 있습니다. **[!UICONTROL Activate]**&#x200B;과 **[!UICONTROL Configure]** 사이의 차이에 대한 자세한 내용은 대상 작업 공간 설명서의 [카탈로그](../../ui/destinations-workspace.md#catalog) 섹션을 참조하십시오.

대상 만들기 작업 과정의 **설정** 단계에서 대상에 대해 [!UICONTROL Basic Information]를 입력합니다.

![기본 정보 Google 광고 관리자](../../assets/catalog/advertising/google-ad-manager/setup.png)

* **[!UICONTROL Name]**:이 대상에 대한 기본 이름을 입력합니다.
* **[!UICONTROL Description]**: 선택 사항. 예를 들어 이 대상을 사용하는 캠페인을 언급할 수 있습니다.
* **[!UICONTROL Account Type]**:Google의 계정에 따라 옵션을 선택합니다.
   * 게시자에 대해 [!DNL DoubleClick]에 `DFP by Google` 사용
   * [!DNL Google AdX]에 `AdX buyer` 사용
* **[!UICONTROL Account ID]**:계정 ID를 다음으로 입력합니다 [!DNL Google]. 네트워크 ID 또는 대상 링크 ID일 수 있습니다. 일반적으로 8자리 ID입니다.
* **[!UICONTROL Marketing action]**:마케팅 작업은 데이터를 대상에 내보내려는 의도를 나타냅니다. Adobe 정의 마케팅 작업 중에서 선택하거나 자신의 마케팅 작업을 만들 수 있습니다. 마케팅 작업에 대한 자세한 내용은 [데이터 사용 정책 개요](../../../data-governance/policies/overview.md)를 참조하십시오.

>[!NOTE]
>
>[!DNL Google Ad Manager] 대상을 설정할 때는 [!DNL Google Account Manager] 또는 Adobe 담당자와 함께 작업하여 보유하고 있는 계정 유형을 파악하십시오.

## 세그먼트를 [!DNL Google Ad Manager]에 활성화

세그먼트를 [!DNL Google Ad Manager]에 활성화하는 방법에 대한 지침은 [대상에 데이터 활성화](../../ui/activate-destinations.md)를 참조하십시오.

## 내보낸 데이터

데이터를 [!DNL Google Ad Manager] 대상으로 성공적으로 내보냈는지 확인하려면 [!DNL Google Ad Manager] 계정을 확인하십시오. 활성화가 성공하면 고객이 계정에 채워집니다.