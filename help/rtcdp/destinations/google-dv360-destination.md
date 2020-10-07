---
keywords: DoubleClick Bid Manager;DoubleClick bid manager;DoubleClick;Display & Video 360;display 360;video 360;Video 360;Display 360;display and video
title: Google 디스플레이 및 비디오 360 대상
seo-title: Google 디스플레이 및 비디오 360 대상
description: 디스플레이 및 비디오 360(이전 DoubleClick 입찰 관리자)은 디스플레이, 비디오 및 모바일 재고 소스에서 타깃팅된 디지털 캠페인 및 대상 재타깃팅을 실행하는 데 사용되는 도구입니다.
seo-description: '디스플레이 및 비디오 360(이전 DoubleClick 입찰 관리자)은 디스플레이, 비디오 및 모바일 재고 소스에서 타깃팅된 디지털 캠페인 및 대상 재타깃팅을 실행하는 데 사용되는 도구입니다. '
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 0%

---


# [!DNL Google Display & Video 360] 대상

## 개요

[!DNL Display & Video 360], 이전에 [!DNL DoubleClick Bid Manager]는 디스플레이, 비디오 및 모바일 인벤토리 소스에서 리타겟팅된 디지털 캠페인 및 대상 캠페인을 실행하는 데 사용되는 도구입니다.

## 대상 사양

대상에 대한 다음 세부 사항을 [!DNL Google Display & Video 360] 참고하십시오.

* 다음 ID를 [대상으로](../../identity-service/namespaces.md) 보낼 수 [!DNL Google Display & Video 360] 있습니다.Google 쿠키 ID, IDFA, GAID, Roku ID, Microsoft ID 및 Amazon Fire TV ID.
* 활성화된 대상은 Google 플랫폼에서 프로그래밍 방식으로 생성됩니다.
* Adobe 실시간 CDP에는 현재 성공적인 활성화를 확인하는 측정 지표가 포함되어 있지 않습니다. 통합을 확인하고 대상 타깃팅 크기를 이해하려면 Google의 대상 수를 참조하십시오.

>[!IMPORTANT]
>
>Google Display &amp; Video 360을 사용하여 첫 번째 대상을 만들고 이전에 Experience Cloud ID 서비스에서 [ID 동기화 기능을](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) 활성화하지 않은 경우(Adobe Audience Manager 또는 기타 애플리케이션 포함), Adobe 컨설팅 또는 고객 지원 센터에 연락하여 ID 동기화를 활성화하십시오. 이전에 Audience Manager에서 Google 통합을 설정한 경우 설정한 ID 동기화가 Adobe 실시간 CDP로 전달됩니다.

### 내보내기 유형 {#export-type}

**세그먼트 내보내기** - 세그먼트(대상)의 모든 멤버를 Google 대상으로 내보냅니다.

## 전제 조건

### 허용 목록

>[!NOTE]
>
>Adobe 실시간 CDP에서 첫 번째 [!DNL Google Display & Video 360] 대상을 설정하기 전에 허용 목록은 필수입니다. 대상을 만들기 전에 아래에 설명된 허용 목록 프로세스가 Google에서 완료되었는지 확인하십시오.

Adobe 실시간 CDP에서 [!DNL Google Display & Video 360] 대상을 생성하기 전에 Google에 Adobe이 허용된 데이터 공급자 목록에 포함될 수 있도록 문의하고 사용자 계정이 허용 목록에 추가될 수 있도록 요청해야 합니다. Google에 연락하여 다음 정보를 제공합니다.

* **계정 ID** :이것은 Google의 Adobe 계정 ID입니다. 이 ID를 얻으려면 Adobe 고객 지원 센터 또는 Adobe 담당자에게 문의하십시오.
* **고객 ID** :Google의 Adobe 고객 계정 ID입니다. 이 ID를 얻으려면 Adobe 고객 지원 센터 또는 Adobe 담당자에게 문의하십시오.
* **계정 유형**:디스플레이 및 비디오 360 계정 **[!DNL Invite advertiser]** 에서 대상을 특정 브랜드에만 공유하거나 디스플레이 및 비디오 360 계정의 모든 브랜드에 대상을 공유할 수 있도록 **[!DNL Invite partner]** 하는 데 사용합니다.

## 대상 구성

1. [ **[!UICONTROL 연결]** ] > **[!UICONTROL 대상]**&#x200B;에서 [!DNL Google Display & Video 360]를 선택하고 구성을 **[!UICONTROL 선택합니다]**.
   ![Connect Google 표시 및 비디오 360 대상](/help/rtcdp/destinations/assets/google-dv360-destination.png)

   >[!NOTE]
   >
   >이 대상과의 연결이 이미 있는 경우 대상 카드에 **[!UICONTROL 활성화]** 단추가 표시됩니다. 활성화 및 구성 [!UICONTROL 의 차이에 대한 자세한][!UICONTROL 내용은 대상 작업 공간 설명서의]카탈로그 [섹션을](/help/rtcdp/destinations/destinations-workspace.md#catalog) 참조하십시오.

2. 대상 **만들기 작업** 과정의 설정 [!UICONTROL 단계에서 대상에 대한] 기본 정보및 이 대상에 적용할 마케팅 사용 사례를 입력합니다. <br>

   ![기본 정보 Google Display &amp; Video 360](/help/rtcdp/destinations/assets/dv360-setup-step.png)
* **[!UICONTROL 이름]**:이 대상에 대한 기본 이름을 입력합니다.
* **[!UICONTROL 설명]**:선택 사항. 예를 들어 이 대상을 사용하는 캠페인을 언급할 수 있습니다.
* **[!UICONTROL 계정 유형]**:Google의 계정에 따라 옵션을 선택합니다.
   * 표시 및 비디오 360 계정 `Invite Advertiser` 에서 대상을 특정 브랜드에만 공유할 수 있도록 허용하는 데 사용합니다.
   * 디스플레이 및 비디오 360 계정 `Invite Partner` 의 모든 브랜드에 대상을 공유할 수 있도록 허용하는 데 사용합니다.
* **[!UICONTROL 계정 ID]**:Google에서 **[!DNL Invite partner]** 또는 **[!DNL Invite advertiser]** 계정 ID를 입력합니다. 일반적으로 6 또는 7자리 ID입니다.
* **[!UICONTROL 마케팅 활용 사례]**:마케팅 사용 사례에서는 데이터를 대상으로 내보내려는 의도를 나타냅니다. Adobe에서 정의한 마케팅 사용 사례에서 선택하거나 고유한 마케팅 사용 사례를 만들 수 있습니다. 마케팅 활용 사례에 대한 자세한 내용은 실시간 CDP의 [데이터 거버넌스](/help/rtcdp/privacy/data-governance-overview.md#destinations) 페이지를 참조하십시오. 개별 Adobe에서 정의한 마케팅 사용 사례에 대한 자세한 내용은 [데이터 사용 정책 개요를 참조하십시오](/help/data-governance/policies/overview.md#core-actions).

>[!NOTE]
>
>대상을 설정할 때 [!DNL Google Display & Video 360] 귀하의 [!DNL Google Account Manager] 또는 Adobe 담당자에게 연락하여 보유하고 있는 계정 유형을 파악하십시오.

## 세그먼트 활성화 [!DNL Google Display & Video 360]

세그먼트를 활성화할 방법에 대한 지침 [!DNL Google Display & Video 360]은 대상에 [데이터 활성화를 참조하십시오](/help/rtcdp/destinations/activate-destinations.md).

## 내보낸 데이터

데이터를 대상으로 성공적으로 내보냈는지 확인하려면 [!DNL Google Display & Video 360] [!DNL Google Display & Video 360] 계정을 확인하십시오. 정품 인증이 성공적으로 완료되면 사용자의 계정에 대상이 채워집니다.