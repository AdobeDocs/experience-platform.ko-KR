---
keywords: DoubleClick 입찰 관리자;DoubleClick 입찰 관리자;DoubleClick;Display & Video 360;디스플레이 360;비디오 360;비디오 360;디스플레이 360;디스플레이 및 비디오
title: Google Display & Video 360 연결
description: 이전에 DoubleClick Bid Manager라고 알려진 Display & Video 360은 디스플레이, 비디오 및 모바일 인벤토리 소스에서 재타겟팅하고 대상 지정 디지털 캠페인을 실행하는 데 사용되는 도구입니다.
exl-id: bdd3b3fd-891f-44ec-bd47-daf7f3289f92
source-git-commit: 802b1844bec1e577e978da5d5a69de87278c04b9
workflow-type: tm+mt
source-wordcount: '671'
ht-degree: 2%

---

# [!DNL Google Display & Video 360] 연결

## 개요 {#overview}

[!DNL Display & Video 360]이전에  [!DNL DoubleClick Bid Manager]라고 함 은 디스플레이, 비디오 및 모바일 인벤토리 소스에서 재타겟팅된 디지털 캠페인을 실행하는 데 사용되는 도구입니다.

## 대상 세부 사항 {#specifics}

[!DNL Google Display & Video 360] 대상에 해당하는 다음 세부 사항을 참고하십시오.

* 활성화된 대상은 Google 플랫폼에서 프로그래밍 방식으로 생성됩니다.
* [!DNL Platform] 현재 에는 성공적인 활성화를 확인하기 위한 측정 지표가 포함되어 있지 않습니다. 통합의 유효성을 확인하고 대상 타깃팅 크기를 이해하려면 Google의 대상 카운트를 참조하십시오.

>[!IMPORTANT]
>
>Google Display &amp; Video 360으로 첫 번째 대상을 만들고 과거에 Experience Cloud ID 서비스에서 [ID 동기화 기능](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html)을 활성화하지 않은 경우(Adobe Audience Manager 또는 다른 애플리케이션 사용) Adobe 컨설팅이나 고객 지원 센터에 연락하여 ID 동기화를 활성화하십시오. 이전에 Audience Manager에서 Google 통합을 설정한 경우, 설정한 ID 동기화를 Platform으로 이월합니다.

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

## 전제 조건

### 허용 목록

>[!NOTE]
>
>Platform에서 첫 번째 [!DNL Google Display & Video 360] 대상을 설정하기 전에 허용 목록이 필수입니다. 대상을 만들기 전에 Google에서 아래 설명된 허용 목록 프로세스를 완료했는지 확인하십시오.

Platform에서 [!DNL Google Display & Video 360] 대상을 만들려면 먼저 Google에 Adobe을 허용된 데이터 공급자 목록에 추가하고, 허용 목록에 계정을 추가하도록 요청해야 합니다. Google에 문의하여 다음 정보를 제공하십시오.

* **계정 ID**: Google을 사용하는 Adobe 계정 ID입니다. 계정 ID: 87933855.
* **고객 ID**: Google을 사용하는 Adobe의 고객 계정 ID입니다. 고객 ID: 89690775.
* **계정 유형**: 디스플레이  **[!DNL Invite advertiser]** 및 비디오 360 계정에서 특정 브랜드에만 대상을 공유할 수 있도록 하거나 디스플레이 및 비디오 360 계정 **[!DNL Invite partner]** 에서 대상을 모든 브랜드에 공유할 수 있도록 하려면 을 사용합니다.

## 대상에 연결 {#connect}

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오.

### 연결 매개 변수 {#parameters}

[이 대상을 설정할 때 다음 정보를 제공해야 합니다.](../../ui/connect-destination.md)

* **[!UICONTROL 이름]**: 이 대상의 기본 이름을 입력합니다.
* **[!UICONTROL 설명]**: 선택 사항입니다. 예를 들어 이 대상을 사용하는 캠페인을 언급할 수 있습니다.
* **[!UICONTROL 계정 유형]**: Google을 사용하는 계정에 따라 옵션을 선택합니다.
   * Display &amp; Video 360 계정의 특정 브랜드에만 대상을 공유할 수 있도록 하려면 `Invite Advertiser` 을 사용하십시오.
   * Display &amp; Video 360 계정의 모든 브랜드에 대상을 공유할 수 있도록 하려면 `Invite Partner` 을 사용하십시오.
* **[!UICONTROL 계정 ID]**: 또는  **[!DNL Invite partner]** 계정  **[!DNL Invite advertiser]** ID를 Google로 입력합니다. 일반적으로 6자리 또는 7자리 ID입니다.

>[!NOTE]
>
>[!DNL Google Display & Video 360] 대상을 설정할 때 보유하고 있는 계정 유형을 이해하려면 [!DNL Google Account Manager] 또는 Adobe 담당자에게 문의하십시오.

## 세그먼트를 이 대상에 활성화 {#activate}

대상으로 대상 세그먼트를 활성화하는 방법에 대한 지침은 [대상 세그먼트 활성화](../../ui/activate-destinations.md)를 참조하십시오.

## 내보낸 데이터

데이터를 [!DNL Google Display & Video 360] 대상으로 성공적으로 내보냈는지 확인하려면 [!DNL Google Display & Video 360] 계정을 확인하십시오. 활성화가 성공하면 계정에 대상이 채워집니다.
