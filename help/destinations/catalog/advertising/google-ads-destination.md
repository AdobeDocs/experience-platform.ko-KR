---
keywords: Google 광고;google 광고;google 광고;Google 애드워즈;Google 애드워즈;Google Adwords
title: Google 광고 연결
description: 이전에 Google AdWords로 알려졌던 Google Ads는 기업에서 텍스트 기반 검색, 그래픽 디스플레이, YouTube 비디오 및 인앱 모바일 디스플레이에 걸쳐 클릭당 광고를 지불하는 온라인 광고 서비스입니다.
translation-type: tm+mt
source-git-commit: 6e7ecfdc0b2cbf6f07e6b2220ec163289511375e
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---


# [!DNL Google Ads] 연결

[!DNL Google Ads](이전 이름 [!DNL Google AdWords]으로 알려짐)은 기업이 텍스트 기반 검색, 그래픽 디스플레이,  [!DNL YouTube] 비디오 및 인앱 모바일 디스플레이에서 클릭당 광고를 유료 표시할 수 있도록 하는 온라인 광고 서비스입니다.

## 대상 사양

[!DNL Google Ads] 대상에 대한 다음 세부 정보를 참조하십시오.

* 다음 [id](../../../identity-service/namespaces.md)를 [!DNL Google Ads] 대상으로 보낼 수 있습니다.[AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en), Google 쿠키 ID, IDFA, GAID, Roku ID, Microsoft ID 및 Amazon Fire TV ID.
   * Google은 [AAM UUID](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/ids-in-aam.html?lang=en)를 사용하여 캘리포니아에 있는 사용자를 타깃팅하고 다른 모든 사용자에 대해 Google 쿠키 ID를 사용합니다.
* 활성화된 대상은 [!DNL Google] 플랫폼에서 프로그래밍 방식으로 생성됩니다.
* 현재 플랫폼에 성공적인 활성화를 확인할 측정 지표가 포함되어 있지 않습니다. 통합을 확인하고 대상 타깃팅 크기를 이해하려면 Google의 대상 수를 참조하십시오.

>[!IMPORTANT]
>
>[!DNL Google Ads]을(를) 사용하여 첫 번째 대상을 만들고 이전에 Experience Cloud ID 서비스에서 [ID 동기화 기능](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html)을(를) 활성화하지 않은 경우(Audience Manager 또는 다른 응용 프로그램 포함) Adobe 컨설팅 또는 고객 지원 센터에 문의하여 ID 동기화를 활성화하십시오. 이전에 Audience Manager에서 Google 통합을 설정한 경우 설정한 ID 동기화가 플랫폼으로 이월됩니다.

### 내보내기 유형 {#export-type}

**세그먼트 내보내기**  - 세그먼트(대상)의 모든 구성원을 Google 대상으로 내보냅니다.

## 전제 조건

### 기존 [!DNL Google Ads] 계정

>[!IMPORTANT]
>
> [!DNL Google] 에 타사 공급업체와의 새  [!DNL Google Ads] 쿠키 통합이 사용되지 않습니다. 다음 섹션에서 허용 목록 단계를 수행하려면 [!DNL Google Ads]과(와) 기존 통합이 있어야 합니다. 따라서 [!DNL Google Ads]을(를) 사용하기 위한 권장 방법은 [!DNL Google Customer Match] 통합을 설정하는 것입니다. [!DNL Google Customer Match] 통합 만들기에 대한 자세한 내용은 [[!DNL Google Customer Match]](./google-customer-match.md) 연결 만들기에 대한 자습서를 참조하십시오.

### 허용 목록

>[!NOTE]
>
>플랫폼에서 첫 번째 [!DNL Google Ads] 대상을 설정하기 전에 허용 목록은 필수입니다. 대상을 만들기 전에 아래에 설명된 허용 목록 프로세스가 [!DNL Google]에 의해 완료되었는지 확인하십시오.

플랫폼에서 [!DNL Google Ads] 대상을 만들기 전에 허용되는 데이터 공급자 목록에 Adobe을 배치하고 허용 목록에 계정을 추가하려면 [!DNL Google]에 문의해야 합니다. [!DNL Google]에 연락하여 다음 정보를 제공합니다.

* **계정 ID** :Adobe 계정 ID입니다 [!DNL Google]. 이 ID를 얻으려면 Adobe 고객 지원 센터 또는 Adobe 담당자에게 문의하십시오.
* **고객 ID** :Adobe의 고객 계정 ID입니다 [!DNL Google]. 이 ID를 얻으려면 Adobe 고객 지원 센터 또는 Adobe 담당자에게 문의하십시오.
* 계정 유형:**AdWords**
* **Google AdWords ID** :ID입니다 [!DNL Google]. ID 형식은 일반적으로 123-456-7890.

## 대상 구성

**[!UICONTROL 연결]** > **[!UICONTROL 대상]**&#x200B;에서 [!DNL Google Ads]를 선택하고 **[!UICONTROL 구성]**&#x200B;을 선택합니다.

![Google 광고 대상 연결](../../assets/catalog/advertising/google-ads-destination/catalog.png)

>[!NOTE]
>
>이 대상과의 연결이 이미 있는 경우 대상 카드에 **[!UICONTROL 활성화]** 단추가 표시될 수 있습니다. **[!UICONTROL 활성화]**&#x200B;와 **[!UICONTROL 구성]**&#x200B;의 차이에 대한 자세한 내용은 대상 작업 공간 설명서의 [카탈로그](../../ui/destinations-workspace.md#catalog) 섹션을 참조하십시오.

대상 만들기 작업 과정의 **설정** 단계에서 대상에 대한 [!UICONTROL 기본 정보]를 입력합니다.

![기본 정보 Google 광고](../../assets/catalog/advertising/google-ads-destination/setup.png)

* **[!UICONTROL 이름]**:이 대상에 대한 기본 이름을 입력합니다.
* **[!UICONTROL 설명]**:선택 사항. 예를 들어 이 대상을 사용하는 캠페인을 언급할 수 있습니다.
* **[!UICONTROL 계정 유형]**:AdWords만 사용할 수 있습니다.
* **[!UICONTROL 계정 ID]**:계정 ID를 다음으로 입력합니다 [!DNL Google Ads]. ID 형식은 일반적으로 123-456-7890.
* **[!UICONTROL 마케팅 작업]**:마케팅 작업은 데이터를 대상에 내보내려는 의도를 나타냅니다. Adobe 정의 마케팅 작업 중에서 선택하거나 자신의 마케팅 작업을 만들 수 있습니다. 마케팅 작업에 대한 자세한 내용은 [데이터 사용 정책 개요](../../../data-governance/policies/overview.md)를 참조하십시오.

## 세그먼트를 [!DNL Google Ads]에 활성화

세그먼트를 [!DNL Google Ads]에 활성화하는 방법에 대한 지침은 [대상에 데이터 활성화](../../ui/activate-destinations.md)를 참조하십시오.

## 내보낸 데이터

데이터를 [!DNL Google Ads] 대상으로 성공적으로 내보냈는지 확인하려면 [!DNL Google Ads] 계정을 확인하십시오. 활성화가 성공하면 고객이 계정에 채워집니다.