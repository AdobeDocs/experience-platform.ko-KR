---
keywords: airship attributes;airship destination
title: Airship 속성 대상
seo-title: Airship 속성 대상
description: Airship 내에서 타깃팅하기 위해 Adobe 대상 데이터를 대상 특성으로 Airship에 매끄럽게 전달합니다.
seo-description: Airship 내에서 타깃팅하기 위해 Adobe 대상 데이터를 대상 특성으로 Airship에 매끄럽게 전달합니다.
translation-type: tm+mt
source-git-commit: 0e065bbc0917d5009738b4cae890ffd13c0ab154
workflow-type: tm+mt
source-wordcount: '1245'
ht-degree: 1%

---


# (베타) [!DNL Airship Attributes] 대상 {#airship-attributes-destination}

>[!IMPORTANT]
>
>Adobe Experience Platform의 [!DNL Airship Attributes] 목적지는 현재 베타 버전입니다. 설명서 및 기능은 변경될 수 있습니다.

## 개요 {#overview}

[!DNL Airship] 선도적인 고객 참여 플랫폼으로 고객 라이프사이클의 모든 단계에서 사용자에게 의미 있고 개인화된 옴니채널 메시지를 제공할 수 있습니다.

이 통합은 타깃팅 또는 트리거를 위해 Adobe 프로필 데이터 [!DNL Airship] 를 [속성으로](https://docs.airship.com/guides/audience/attributes/) 전달합니다.

자세한 내용은 Airship Docs [!DNL Airship]를 [참조하십시오](https://docs.airship.com).


>[!TIP]
>
>이 설명서 페이지는 [!DNL Airship] 팀이 만들었습니다. 문의 또는 업데이트 요청이 있는 경우 [support.airship.com으로 직접 문의하십시오](https://support.airship.com/).

## 전제 조건 {#prerequisites}

대상 세그먼트를 다음으로 보내기 전에 다음을 수행해야 [!DNL Airship]합니다.

* 프로젝트에서 속성을 [!DNL Airship] 활성화합니다.
* 인증에 사용할 무기급 토큰을 생성합니다.

>[!TIP]
>
>아직 계정이 없는 경우 [!DNL Airship] 이 등록 링크를 통해 [](https://go.airship.eu/accounts/register/plan/starter/) 계정을 만듭니다.

### 속성 활성화 {#enable-attributes}

Adobe Experience Platform 프로필 속성은 속성과 유사하며, 이 페이지에서 아래에 자세히 설명된 매핑 도구를 사용하여 Platform에서 서로 쉽게 매핑할 수 있습니다. [!DNL Airship]

[!DNL Airship] 프로젝트에는 여러 개의 사전 정의된 기본 속성이 있습니다. 사용자 지정 속성이 있는 경우 [!DNL Airship] 먼저 정의해야 합니다. 자세한 [내용은 속성](https://docs.airship.com/tutorials/audience/attributes/) 설정 및 관리를 참조하십시오.

### 무기명 토큰 {#bearer-token}

1. Airship **[!UICONTROL 대시보드의]** **[!UICONTROL Settings]** [APIs &amp; Integration](https://go.airship.com) 으로 **[!UICONTROL 이동하고]** 왼쪽 메뉴에서 Tokens를 선택합니다.
1. 토큰 **[!UICONTROL 만들기를 클릭합니다]**.
1. 토큰에 대해 사용자에게 친숙한 이름을 입력하고(예: &quot;Adobe 속성 대상&quot;) 역할에 대해 &quot;모든 액세스&quot;를 선택합니다.
1. 토큰 **[!UICONTROL 만들기를]** 클릭하고 세부 사항을 기밀로 저장합니다.


## 사용 사례 {#use-cases}

대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례를 소개합니다. [!DNL Airship Attributes]

### 사용 사례 #1

Adobe Experience Platform에서 수집된 프로필 데이터를 활용하여 모든 채널에서 메시지와 풍부한 컨텐츠를 개인화할 수 [!DNL Airship]있습니다. 예를 들어 프로필 [!DNL Experience Platform] 데이터를 활용하여 내에서 위치 속성을 설정할 수 [!DNL Airship]있습니다. 이를 통해 호텔 브랜드는 각 사용자에 가장 가까운 호텔 위치에 대한 이미지를 표시할 수 있습니다.

### 사용 사례 #2

Adobe Experience Platform의 속성을 활용하여 프로파일을 더욱 강화하고 SDK 또는 예측 데이터와 결합할 수 [!DNL Airship] [!DNL Airship] 있습니다. 예를 들어 소매업체는 충성도 상태 및 위치 데이터(플랫폼의 특성)가 포함된 세그먼트를 만들고 데이터를 이탈하여 Las Vegas, NV)에 거주하는 사용자에게 고도로 타겟팅된 메시지를 전송하고 대량 추월 가능성이 높은 골드 로열티 상태에 있는 사용자를 대상으로 보낼 [!DNL Airship] 것으로 예측합니다.

## 속성에 [!DNL Airship] 연결 {#connect-airship-attributes}

1. [ **[!UICONTROL 대상]** ] > [ **[!UICONTROL 카탈로그]**]에서 **[!UICONTROL 모바일 참여]** 범주로스크롤합니다. 을 **[!DNL Airship Attributes]**&#x200B;선택하고 구성을 **[!UICONTROL 선택합니다]**.

   >[!NOTE]
   >
   >이 대상과의 연결이 이미 있는 경우 대상 카드에 **[!UICONTROL 활성화]** 단추가 표시됩니다. 활성화 및 구성 **[!UICONTROL 의 차이에 대한 자세한]****[!UICONTROL 내용은 대상 작업 공간 설명서의]**&#x200B;카탈로그 [섹션을](/help/rtcdp/destinations/destinations-workspace.md#catalog) 참조하십시오.

   ![항공 특성 연결](/help/rtcdp/destinations/assets/airship-attributes-in-catalog.png)

2. 이전에 대상에 대한 연결을 **설정한** 경우 [!DNL Airship Attributes] 계정 **[!UICONTROL 을 선택하고 기존 연결을]** 선택합니다. 또는 새 계정 **[!UICONTROL 을]** 선택하여 새 연결을 설정할 수 [!DNL Airship Attributes]있습니다. 대시보드에서 **[!UICONTROL 생성한]** 베어러 토큰을 사용하여 Adobe Experience Platform을 프로젝트에 연결하려면 대상에 [!DNL Airship] 연결을 [!DNL Airship] 선택합니다.

   >[!NOTE]
   >
   >Adobe Experience Platform은 인증 프로세스에서 자격 증명 유효성 검사를 지원하고 계정에 잘못된 자격 증명을 입력하는 경우 오류 메시지를 [!DNL Airship] 표시합니다. 따라서 잘못된 자격 증명으로 워크플로우를 완료하지 못합니다.

   ![항공 특성 연결](/help/rtcdp/destinations/assets/airship1-connect-to-airship.png)

3. 자격 증명이 확인되고 Adobe Experience Platform이 [!DNL Airship] 프로젝트에 연결되면 **[!UICONTROL 다음]** 을 선택하여 **[!UICONTROL 설정]** 단계로 진행할 수 있습니다.

4. 인증 **[!UICONTROL 단계]** 에서 **[!UICONTROL 이름]****[!UICONTROL 과]** 정품 인증과정에 대한 설명을입력합니다. <br> 또한 이 단계에서는 이 대상에 적용되는 [!DNL Airship] 데이터 센터에 따라 미국 또는 EU 데이터 센터를 선택할 수 있습니다. 마지막으로 대상으로 데이터를 내보낼 마케팅 사용 사례를 하나 이상 선택합니다. Adobe에서 정의한 마케팅 사용 사례에서 선택하거나 직접 만들 수 있습니다. 마케팅 활용 사례에 대한 자세한 내용은 실시간 CDP의 [데이터 거버넌스](/help/rtcdp/privacy/data-governance-overview.md#destinations) 페이지를 참조하십시오. 개별 Adobe에서 정의한 마케팅 사용 사례에 대한 자세한 내용은 [데이터 사용 정책 개요를 참조하십시오](/help/data-governance/policies/overview.md#core-actions). <br> 위 필드 **[!UICONTROL 를]** 채운 후 대상 만들기를 선택합니다.

   ![항공 특성 연결](/help/rtcdp/destinations/assets/airship2-select-airship-domain.png)

5. 이제 대상이 만들어집니다. 나중에 세그먼트 **[!UICONTROL 를]** 활성화하려면 저장 및 종료를 **[!UICONTROL 선택하거나]** 다음을 선택하여 워크플로우를 계속하고 활성화할 세그먼트를 선택할 수 있습니다. 두 경우 모두 워크플로우의 나머지 [에 대해 다음 섹션, 세그먼트](#activate-segments)활성화를 참조하십시오.

## 세그먼트 활성화 {#activate-segments}

세그먼트를 활성화하려면 [!DNL Airship Attributes]아래 단계를 따르십시오.

1. 대상 **[!UICONTROL > 찾아보기에서]**&#x200B;세그먼트를 활성화할 [!DNL Airship Attributes] 대상을 선택합니다.
   ![정품 인증](/help/rtcdp/destinations/assets/airship-attributes-activate1.png)
1. 대상의 이름을 클릭합니다. 활성화 흐름으로 이동합니다.
대상에 대한 활성화 흐름이 이미 존재하는 경우 대상에 현재 전송되고 있는 세그먼트를 볼 수 있습니다. 오른쪽 레일에서 **[!UICONTROL 활성화]** 편집을 선택하고 아래 단계에 따라 정품 인증 세부 사항을 수정합니다. ![정품 인증](/help/rtcdp/destinations/assets/airship-attributes-activate2.png)
1. 활성화 **[!UICONTROL 를]**&#x200B;선택합니다.
1. 대상 **[!UICONTROL 활성화]** 워크플로의 세그먼트 **[!UICONTROL 선택]** 페이지에서 보낼 세그먼트를 [!DNL Airship Attributes]선택합니다.
   ![세그먼트-대상](/help/rtcdp/destinations/assets/airship3-select-segments-to-export.png)
1. 매핑 **[!UICONTROL 단계]** 에서 대상 스키마에 매핑할 [XDM](https://docs.adobe.com/content/help/ko-KR/experience-platform/xdm/home.html) 스키마에서 속성과 ID를 선택합니다. 새 매핑 **[!UICONTROL 추가를]** 선택하여 스키마를 검색하고 해당 대상 ID에 매핑합니다.
   ![ID 매핑 초기 화면](/help/rtcdp/destinations/assets/gcm-identity-mapping.png)
   [!DNL Airship] 속성은 장치 인스턴스(예: iPhone 또는 지정된 사용자)를 나타내는 채널에서 설정할 수 있습니다. 이 채널은 모든 사용자의 장치를 고객 ID와 같은 일반 식별자에 매핑합니다. 스키마의 기본 ID로 일반 텍스트(해시되지 않은) 이메일 주소가 있는 경우 **[!UICONTROL 소스 속성]** 의 이메일 필드를 선택하고 [!DNL Airship] Target ID **[!UICONTROL 아래 오른쪽 열에 있는 지정된 사용자]**에게 매핑합니다.
   ![명명된 사용자 매핑](/help/rtcdp/destinations/assets/airshiptags7-mappingoption2.png)채널에 매핑되어야 하는 식별자(예: 장치)를 위해 소스를 기반으로 적절한 채널에 매핑합니다. 다음 이미지는 두 가지 매핑이 만들어지는 방식을 보여 줍니다.

   * iOS 채널에 대한 IDFA iOS 광고 [!DNL Airship] ID
   * Adobe 속성 `fullName` 을 &quot; [!DNL Airship] 전체 이름&quot; 속성에 지정

   >[!NOTE]
   >
   >속성 매핑에 대한 대상 필드를 선택할 때 [!DNL Airship] 대시보드에 나타나는 사용자에게 친숙한 이름을 사용합니다.

   **매핑 ID**소스 필드 선택:
   ![Airship 속성에](/help/rtcdp/destinations/assets/airship5-select-source-identity.png)연결 대상 필드 선택:
   ![항공 특성 연결](/help/rtcdp/destinations/assets/airship6-select-target-identity.png)

   **매핑 속성**

   소스 속성 선택:
   ![소스 필드 선택](/help/rtcdp/destinations/assets/airship7-select-source-attributes.png)대상 속성 선택:
   ![대상 필드](/help/rtcdp/destinations/assets/airship8-select-target-attribute.png)매핑 확인:
   ![채널 매핑](/help/rtcdp/destinations/assets/airship9-mapping-final.png)

1. 세그먼트 **[!UICONTROL 예약]** 페이지에서 현재 예약을 사용할 수 없습니다. 다음 **[!UICONTROL 을]** 클릭하여 검토 단계를 계속 진행합니다. ![현재 예약 비활성화](/help/rtcdp/destinations/assets/airship10-scheduling-step-is-disabled-for-now.png)

1. [ **[!UICONTROL 검토]** ] 페이지에서 선택 사항의 요약을 볼 수 있습니다. 흐름을 구분하려면 **[!UICONTROL 취소]** 를, 설정을 **[!UICONTROL 수정하려면]** [뒤로]를, **[!UICONTROL 마침을]** 선택하여 선택을 확인하고 데이터를 대상에 보내기 시작합니다.

>[!IMPORTANT]
>
>이 단계에서는 데이터 사용 정책 위반을 확인합니다. 아래는 정책을 위반한 예입니다. 위반이 해결되기 전에는 세그먼트 활성화 워크플로우를 완료할 수 없습니다. 정책 위반을 해결하는 방법에 대한 자세한 내용은 데이터 거버넌스 문서 섹션에서 [정책](/help/rtcdp/privacy/data-governance-overview.md#enforcement) 적용을 참조하십시오.

![선택 확인](/help/rtcdp/destinations/assets/data-policy-violation.png)

정책 위반이 감지되지 않은 경우 **[!UICONTROL 마침을]** 선택하여 선택을 확인하고 대상으로 데이터 전송을 시작합니다.

![검토](/help/rtcdp/destinations/assets/airship11-review-step.png)

## 데이터 사용 및 관리 {#data-usage-governance}

모든 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 데이터 거버넌스 [!DNL Adobe Experience Platform] 를 적용하는 방법에 대한 자세한 내용은 실시간 CDP의 [데이터 거버넌스를 참조하십시오](/help/rtcdp/privacy/data-governance-overview.md).
