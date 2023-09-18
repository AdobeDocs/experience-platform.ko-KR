---
title: (Beta) 트레이드 데스크 - CRM 연결
description: CRM 데이터를 기반으로 대상 타기팅 및 억제에 대한 프로필을 트레이드 데스크 계정에 활성화합니다.
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: e09eaede-5525-4a51-a0e6-00ed5fdc662b
source-git-commit: 661ef040398a9e2ef8dd9cebdf7bd27d4268636b
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 4%

---

# (베타) [!DNL Trade Desk] - CRM 연결

>[!IMPORTANT]
>
>[!DNL The Trade Desk - CRM] 플랫폼의 대상은 현재 베타 버전입니다. 설명서 및 기능은 변경될 수 있습니다.
>
>EUID(유럽 통합 ID)가 출시되면서 이제 두 개의 [!DNL The Trade Desk - CRM] 대상이 [대상 카탈로그](/help/destinations/catalog/overview.md)에 표시됩니다.
>* EU에서 소스 데이터를 제공하는 경우 **[!DNL The Trade Desk - CRM (EU)]** 대상을 사용하십시오.
>* APAC 또는 NAMER 지역에서 소스 데이터를 제공하는 경우 **[!DNL The Trade Desk - CRM (NAMER & APAC)]** 대상을 사용하십시오.
>
>Experience Platform의 두 대상 모두 현재 베타 버전입니다. 이 대상 커넥터 및 설명서 페이지는 *[!DNL Trade Desk]* 팀. 문의 사항이나 업데이트 요청이 있으면 다음으로 문의하십시오. [!DNL Trade Desk] 대표적으로 설명서와 기능은 변경될 수 있습니다.

## 개요 {#overview}

이 문서는 다음에 대한 프로필을 활성화하는 데 도움이 되도록 설계되었습니다. [!DNL Trade Desk] crm 데이터를 기반으로 대상 타기팅 및 억제에 대해 설명합니다.

[!DNL The Trade Desk(TTD)] 은 이메일 주소의 업로드 파일을 언제든지 직접 처리하지 않으며 [!DNL The Trade Desk] 원시(해시되지 않은) 이메일을 저장합니다.

>[!TIP]
>
>사용 [!DNL The Trade Desk] 이메일 또는 해시된 이메일 주소와 같은 CRM 데이터 매핑을 위한 CRM 대상. 사용 [기타 무역 데스크 대상](/help/destinations/catalog/advertising/tradedesk.md) 쿠키 및 장치 ID 매핑을 위한 Adobe Experience Platform 카탈로그에서.

## 전제 조건 {#prerequisites}

대상자를 활성화하기 전에 [!DNL The Trade Desk], 다음으로 문의해야 합니다. [!DNL The Trade Desk] 계정 관리자가 CRM 온보딩 계약에 서명합니다. [!DNL The Trade Desk] 그런 다음 권한을 부여하고 광고주 ID를 공유하여 대상을 구성합니다.

## ID 일치 요구 사항 {#id-matching-requirements}

Adobe Experience Platform에 수집하는 ID 유형에 따라 해당 요구 사항을 준수해야 합니다. 다음을 읽으십시오. [ID 네임스페이스 개요](/help/identity-service/namespaces.md) 추가 정보.

## 지원되는 ID {#supported-identities}

[!DNL The Trade Desk] 는 아래 표에 설명된 id 활성화를 지원합니다. 자세히 알아보기 [id](/help/identity-service/namespaces.md).

Adobe Experience Platform은 일반 텍스트와 SHA256 해시 이메일 주소를 모두 지원합니다. ID 일치 요구 사항 섹션의 지침에 따라 일반 텍스트 및 해시된 이메일 주소에 적절한 네임스페이스를 각각 사용하십시오.

| 대상 ID | 설명 | 고려 사항 |
|---|---|---|
| 이메일 | 이메일 주소(텍스트 지우기) | 입력 `email` 소스 ID가 이메일 네임스페이스 또는 속성인 경우 타겟 ID로. |
| Email_LC_SHA256 | 이메일 주소는 SHA256 및 소문자를 사용하여 해시해야 합니다. 다음 중 하나를 따르십시오. [이메일 표준화](https://github.com/UnifiedID2/uid2docs/tree/main/api#email-address-normalization) 규칙이 필요합니다. 나중에 이 설정을 변경할 수 없습니다. | 입력 `hashed_email` 소스 ID가 Email_LC_SHA256 네임스페이스 또는 속성일 경우 타겟 ID로 사용됩니다. |

{style="table-layout:auto"}

## 이메일 해시 요구 사항 {#hashing-requirements}

이메일 주소를 Adobe Experience Platform에 수집하기 전에 해시하거나 원시 이메일 주소를 사용할 수 있습니다.

Experience Platform에서 이메일 주소 수집에 대해 알아보려면 [일괄 처리 수집 개요](/help/ingestion/batch-ingestion/overview.md).

이메일 주소를 직접 해시하도록 선택하는 경우 다음 요구 사항을 준수해야 합니다.

* 선행 및 후행 공백을 제거합니다.
* 모든 ASCII 문자를 소문자로 변환합니다.
* 위치 `gmail.com` 이메일 주소에서 이메일 주소의 사용자 이름 부분에서 다음 문자를 제거합니다.
   * 마침표(. (ASCII 코드 46). 예를 들어 를 정규화합니다. `jane.doe@gmail.com` 끝 `janedoe@gmail.com`.
   * 더하기 기호(+(ASCII 코드 43)) 및 모든 후속 문자 예를 들어 를 정규화합니다. `janedoe+home@gmail.com` 끝 `janedoe@gmail.com`.

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 대상자 내보내기]** | Trade Desk 대상에 사용된 식별자(이메일 또는 해시된 이메일)로 대상자의 모든 구성원을 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL 일별 일괄 처리]** | 프로필은 대상 평가를 기반으로 Experience Platform에서 업데이트되므로 프로필(ID)은 대상 플랫폼으로 하루에 한 번 업데이트됩니다. 자세한 내용 [일괄 내보내기](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

### 대상에 인증 {#authenticate}

[!DNL The Trade Desk] CRM 대상은 일별 일괄 처리 파일 업로드이며, 사용자의 인증이 필요하지 않습니다.

### 대상 세부 사항 입력 {#fill-in-details}

대상 데이터를 대상으로 보내거나 활성화하려면 먼저 고유한 대상 플랫폼에 대한 연결을 설정해야 합니다. While [설정 중](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/connect-destination.html?lang=en) 이 대상에는 다음 정보를 제공해야 합니다.

* **[!UICONTROL 계정 유형]**: 다음 항목을 선택하십시오. **[!UICONTROL 기존 계정]** 옵션을 선택합니다.
* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 광고주 ID]**: 사용자 [!DNL Trade Desk Advertiser ID], 다음 중 하나에서 공유할 수 있습니다. [!DNL Trade Desk] 계정 관리자 또는 다음에서 찾을 수 있음 [!DNL Advertiser Preferences] 다음에서 [!DNL Trade Desk] UI.

![대상 세부 정보를 채우는 방법을 보여 주는 플랫폼 UI 스크린샷입니다.](/help/destinations/assets/catalog/advertising/tradedesk/configuredestination2.png)

대상에 연결할 때 데이터 거버넌스 정책을 설정하는 것은 완전히 선택 사항입니다. Experience Platform을 검토하십시오. [데이터 거버넌스 개요](/help/data-governance/policies/overview.md) 을 참조하십시오.

## 이 대상에 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.
>* 내보내려면 *id*, 다음이 필요합니다. **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). <br> ![워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다.](/help/destinations/assets/overview/export-identities-to-destination.png "워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다."){width="100" zoomable="yes"}

읽기 [대상자 데이터를 일괄 프로필 내보내기 대상으로 활성화](/help/destinations/ui/activate-batch-profile-destinations.md) 대상을 대상으로 활성화하는 방법에 대한 지침입니다.

다음에서 **[!UICONTROL 예약]** 페이지에서 내보내는 각 대상에 대해 일정 및 파일 이름을 구성할 수 있습니다. 예약을 구성해야 하지만, 파일 이름을 구성하는 것은 선택 사항입니다.

![대상자 활성화를 예약하기 위한 Platform UI 스크린샷](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment1.png)

>[!NOTE]
>
>에 대해 활성화된 모든 대상자 [!DNL The Trade Desk] CRM 대상은 매일 빈도와 전체 파일 내보내기로 자동 설정됩니다.

![대상자 활성화를 예약하기 위한 Platform UI 스크린샷](/help/destinations/assets/catalog/advertising/tradedesk/schedulesegment2.png)

다음에서 **[!UICONTROL 매핑]** 페이지에서 소스 열에서 속성 또는 id 네임스페이스를 선택하고 대상 열에 매핑해야 합니다.

![대상자 활성화를 매핑하기 위한 Platform UI 스크린샷입니다.](/help/destinations/assets/catalog/advertising/tradedesk/mappingsegment1.png)

아래는 대상자를 활성화할 때 올바른 ID 매핑의 예입니다 [!DNL The Trade Desk] CRM 대상입니다.

>[!IMPORTANT]
>
> [!DNL The Trade Desk] CRM 대상은 동일한 활성화 플로우에서 원시 및 해시된 이메일 주소를 ID로 허용하지 않습니다. 원시 이메일 주소와 해시된 이메일 주소에 대해 별도의 활성화 흐름을 만듭니다.

소스 필드 선택:

* 다음 항목 선택 `Email` 데이터 수집에 원시 이메일 주소를 사용하는 경우 네임스페이스 또는 속성을 소스 id로 사용합니다.
* 다음 항목 선택 `Email_LC_SHA256` 데이터 수집 시 고객 이메일 주소를 Platform으로 해시한 경우 네임스페이스 또는 속성을 소스 ID로 사용합니다.

대상 필드 선택:

* 입력  `email` 소스 네임스페이스 또는 속성이 인 경우 타겟 ID로 `Email`.
* 입력  `hashed_email` 소스 네임스페이스 또는 속성이 인 경우 타겟 ID로 `Email_LC_SHA256`.

## 데이터 내보내기 유효성 검사 {#validate}

데이터가 Experience Platform 외부로 및 로 올바르게 내보내졌는지 확인하려면 [!DNL The Trade Desk], 내의 1PD 데이터 타일 Adobe 아래에서 대상자를 찾으십시오. [!DNL The Trade Desk] DMP(데이터 관리 플랫폼). 다음은에서 해당 ID를 찾는 단계입니다. [!DNL Trade Desk] UI:

1. 먼저 **[!UICONTROL 데이터]** 탭 및 검토 **[!UICONTROL 자사]**.
2. 페이지를 아래로 스크롤하여 **[!UICONTROL 가져온 데이터]**, 다음을 찾을 수 있습니다. **[!UICONTROL Adobe 1PD 타일]**.
3. 을(를) 클릭합니다**[!UICONTROL Adobe 1PD]**를 클릭하면 타일에 활성화된 모든 대상자가 [!DNL Trade Desk] 광고주의 대상. 검색 기능을 사용할 수도 있습니다.
4. 세그먼트의 Experience Platform ID 번호 는 의 세그먼트 이름으로 나타납니다. [!DNL Trade Desk] UI.

## 데이터 사용 및 관리 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스 시행, 다음을 참조하십시오. [데이터 거버넌스 개요](/help/data-governance/home.md).
