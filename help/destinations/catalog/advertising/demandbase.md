---
title: Demandbase 연결
description: 이 대상을 사용하여 Account-Based Marketing(ABM) 사용 사례에 대한 계정 대상을 활성화하십시오. DemandBase의 DSP(B2B Demand Side Platform)를 통해 대상 계정의 관련 담당자 및 역할에 광고를 게재합니다. 마케팅 및 판매의 다른 다운스트림 사용 사례에 대해 Demandbase 타사 데이터를 사용하여 대상 계정을 보강할 수도 있습니다.
badgeB2B: label="B2B 버전" type="Informative" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
badgeB2P: label="B2P 버전" type="Positive" url=" https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=en#rtcdp-editions newtab=true"
last-substantial-update: 2024-09-30T00:00:00Z
source-git-commit: 92abae6bc63c13f1103364ae82cc9c04459ce00f
workflow-type: tm+mt
source-wordcount: '696'
ht-degree: 3%

---


# Demandbase 연결 {#demandbase}

>[!AVAILABILITY]
>
>>Real-time Customer Data Platform의 [Business-to-Business](/help/rtcdp/overview.md#rtcdp-b2b) 및 [Business-to-Person](/help/rtcdp/overview.md#rtcdp-b2p) 에디션을 구매하는 회사는 Demandbase 대상에 대한 계정 대상을 활성화할 수 있습니다.

[계정 대상자](/help/segmentation/ui/account-audiences.md)를 기반으로 대상자 타깃팅, 개인화 및 제외를 위한 Demandbase 캠페인에 대한 프로필을 활성화합니다.

## 활용 사례 {#use-case}

이 대상을 사용하여 Account-Based Marketing(ABM) 사용 사례에 대한 계정 대상을 활성화하십시오. DemandBase의 DSP(B2B Demand Side Platform)를 통해 대상 계정의 관련 담당자 및 역할에 광고를 게재합니다. 마케팅 및 판매의 다른 다운스트림 사용 사례에 대해 Demandbase 타사 데이터를 사용하여 대상 계정을 보강할 수도 있습니다.

예를 들어, Demandbase의 애드테크 DSP을 활용하여 주요 계정 내에서 특정 담당자 또는 역할을 타겟팅하거나 구매 그룹을 생성하고 늘릴 수 있습니다. Demandbase 대상을 사용하여 계정을 효과적으로 타기팅하는 다른 사용 사례를 살펴보십시오.

또한 이 통합을 통해 실시간 계정 정보 조회를 사용하여 웹 사이트 경험을 개인화하여 참여를 최적화할 수 있습니다.

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ 덧신 | Experience Platform [세그먼테이션 서비스](../../../segmentation/home.md)를 통해 생성된 대상입니다. |
| 사용자 정의 업로드 | X | CSV 파일에서 Experience Platform으로 대상 [가져옴](../../../segmentation/ui/overview.md#import-audience). |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-and-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
|--------------|-----------|---------------------------|
| 내보내기 유형 | 대상자 내보내기 | 모든 대상 멤버는 이름, 전화번호 등과 같은 키 식별자와 함께 내보내집니다. |
| 빈도 | 스트리밍 | &quot;상시 설정&quot; API 기반 연결. 업데이트는 프로필 변경 후 즉시 다운스트림으로 전송됩니다. |

{style="table-layout:auto"}

## 전제 조건 {#prerequisites}

계정 대상을 Demandbase로 내보내려면 다음이 필요합니다.

1. Demandbase 계정입니다.
2. Demandbase API 토큰. Demandbase에서 사용자와 함께 API 토큰을 생성할 수 있습니다. 토큰을 생성하려면 Demandbase 계정에 로그인한 후 [내 프로필 > API 토큰](https://web.demandbase.com/o/ad/at)(으)로 이동합니다.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

대상에 인증하려면 필수 필드를 입력한 다음 **[!UICONTROL 대상에 연결]**&#x200B;을(를) 선택하십시오.

![전달자 토큰 추가](/help/destinations/assets/catalog/advertising/demandbase/add-bearer-token.png)

* **[!UICONTROL 전달자 토큰]**: 대상에 인증하려면 전달자 토큰을 입력하십시오. 토큰을 얻는 방법에 대한 자세한 내용은 [필수 구성 요소](#prerequisites)를 참조하십시오.

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

![대상 연결에 대한 정보 추가](/help/destinations/assets/catalog/advertising/demandbase/name-and-description.png)

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 엔터티 형식]**: 엔터티 형식으로 **[!UICONTROL 계정]**&#x200B;을(를) 선택하십시오.

이제 Demandbase 내에서 대상을 활성화할 준비가 되었습니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

이 대상에 대한 계정 대상을 활성화하는 방법에 대한 지침은 [계정 대상 활성화](/help/destinations/ui/activate-account-audiences.md)를 참조하십시오.

## 추가 참고 사항 및 중요한 설명선 {#additional-notes}

* 같은 이름의 계정 대상이 이전에 Demandbase에 활성화되었을 경우 Demandbase 대상에 대한 다른 데이터 흐름을 통해 다시 활성화할 수 없습니다.
* 대상을 Demandbase로 내보냈는데 Experience Platform에서 내보내기가 성공했지만 모든 데이터가 Demandbase에 도달하지 않은 경우 Demandbase 측에서 API 제한이 발생할 수 있습니다. 자세한 내용은 해당 담당자에게 문의하십시오.
