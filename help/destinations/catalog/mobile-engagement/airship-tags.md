---
keywords: 비행선 태그;비행선 목적지
title: 비행선 태그 연결
description: Airship 내에서 타깃팅할 대상 태그로 Adobe 대상 데이터를 Airship에 원활하게 전달합니다.
exl-id: 84cf5504-f0b5-48d8-8da1-ff91ee1dc171
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 2%

---

# [!DNL Airship Tags] 연결 {#airship-tags-destination}

## 개요

[!DNL Airship] 는 고객 라이프사이클의 모든 단계에서 사용자에게 의미 있고 개인화된 옴니채널 메시지를 제공하는 데 도움이 되는 최고의 고객 참여 플랫폼입니다.

이 통합은 Adobe Experience Platform 대상 데이터를 [!DNL Airship] 다음으로: [태그](https://docs.airship.com/guides/audience/tags/) 타겟팅 또는 트리거용.

에 대해 자세히 알아보기 [!DNL Airship], 다음을 참조하십시오. [비행선 문서](https://docs.airship.com).


>[!TIP]
>
>이 대상 커넥터 및 설명서 페이지는 [!DNL Airship] 팀. 문의 사항이나 업데이트 요청은 다음 주소로 직접 문의하십시오. [support.airship.com](https://support.airship.com/).

## 전제 조건

Adobe Experience Platform 대상자를 다음으로 보내기 전에 [!DNL Airship], 다음을 수행해야 합니다.

* 에서 태그 그룹 만들기 [!DNL Airship] 프로젝트.
* 인증을 위한 전달자 토큰을 생성합니다.

>[!TIP]
> 
>만들기 [!DNL Airship] 계정 [이 등록 링크](https://go.airship.eu/accounts/register/plan/starter/) 아직 하지 않았다면.

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ 덧신 | Experience Platform을 통해 생성된 대상자 [세분화 서비스](../../../segmentation/home.md). |
| 사용자 정의 업로드 | ✓ 덧신 | 대상 [가져옴](../../../segmentation/ui/audience-portal.md#import-audience) csv 파일에서 Experience Platform으로 변환했습니다. |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 대상자 내보내기]** | Airship Tags 대상에 사용된 식별자를 사용하여 대상자의 모든 구성원을 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 태그 그룹

Adobe Experience Platform의 대상자 개념은 와 유사합니다 [태그](https://docs.airship.com/guides/audience/tags/) Airship에서, 구현에 약간의 차이가 있음. 이 통합은 사용자의 상태를 매핑합니다. [Experience Platform 세그먼트의 멤버십](../../../xdm/field-groups/profile/segmentation.md) 의 존재 여부를 불문한다 [!DNL Airship] 태그에 가깝게 배치하십시오. (예: Platform 대상자) `xdm:status` 변경 사항 `realized`에 태그가 추가됩니다 [!DNL Airship] 이 프로필이 매핑된 채널 또는 명명된 사용자. 다음과 같은 경우 `xdm:status` 변경 사항 `exited`, 태그가 제거됩니다.

이 통합을 사용하려면 *태그 그룹* 위치: [!DNL Airship] 명명된 `adobe-segments`.

>[!IMPORTANT]
>
>새 태그 그룹을 만들 때 **확인 안 함** &quot;&quot;라는 라디오 버튼[!DNL Allow these tags to be set only from your server]&quot;. 이렇게 하면 Adobe 태그 통합에 실패합니다.

다음을 참조하십시오 [태그 그룹 관리](https://docs.airship.com/tutorials/manage-project/messaging/tag-groups) 태그 그룹 만들기에 대한 지침입니다.

## 전달자 토큰 생성

다음으로 이동 **[!UICONTROL 설정]** &quot; **[!UICONTROL API 및 통합]** 다음에서 [비행선 계기판](https://go.airship.com) 및 선택 **[!UICONTROL 토큰]** 왼쪽 메뉴에서 을 클릭합니다.

클릭 **[!UICONTROL 토큰 만들기]**.

토큰에 대해 사용자에게 친숙한 이름(예: &quot;Adobe 태그 대상&quot;)을 제공하고 역할에 대해 &quot;모든 액세스&quot;를 선택합니다.

클릭 **[!UICONTROL 토큰 만들기]** 세부 정보를 기밀로 저장합니다.

## 사용 사례

을(를) 사용하는 방법과 시기를 더 잘 이해할 수 있도록 [!DNL Airship Tags] 대상: 다음은 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례입니다.

### 사용 사례 #1

판매업체 또는 엔터테인먼트 플랫폼은 충성도 고객을 기반으로 사용자 프로필을 생성하고 이러한 대상자를 로 전달할 수 있습니다. [!DNL Airship] 모바일 캠페인에서 메시지 타겟팅용.

### 사용 사례 #2

사용자가 Adobe Experience Platform 내의 특정 대상에 속하거나 속하지 않을 때 실시간으로 일대일 메시지를 트리거합니다.

예를 들어, 소매업체는 Platform에서 청바지 브랜드별 고객을 설정합니다. 해당 소매업체는 이제 청바지 선호도를 특정 브랜드로 설정하는 즉시 모바일 메시지를 트리거할 수 있습니다.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

이 대상에 연결하려면 다음과같이 하십시오. [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

대상에 인증하려면 필수 필드를 입력한 다음 을(를) 선택합니다. **[!UICONTROL 대상에 연결]**.

* **[!UICONTROL 전달자 토큰]**: 다음에서 생성한 전달자 토큰 [!DNL Airship] 대시보드입니다.

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 이 대상을 식별하는 데 도움이 되는 이름을 입력합니다.
* **[!UICONTROL 설명]**: 이 대상에 대한 설명을 입력합니다.
* **[!UICONTROL 도메인]**: 다음 항목에 따라 미국 또는 유럽 연합 데이터 센터 선택 [!DNL Airship] 데이터 센터는 이 대상에 적용됩니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 다음 안내서를 참조하십시오. [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보를 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

다음을 참조하십시오 [대상 데이터를 스트리밍 대상 내보내기 대상으로 활성화](../../ui/activate-segment-streaming-destinations.md) 이 대상에 대한 대상자 활성화에 대한 지침을 참조하십시오.

## 매핑 고려 사항 {#mapping-considerations}

[!DNL Airship] 태그는 장치 인스턴스를 나타내는 채널(예: iPhone) 또는 사용자의 모든 장치를 고객 ID와 같은 공통 식별자에 매핑하는 명명된 사용자에 설정할 수 있습니다. 스키마에 기본 ID로 일반 텍스트(해시되지 않은) 이메일 주소가 있는 경우 **[!UICONTROL Source 속성]** 및 을(를) 다음에 매핑 [!DNL Airship] 아래의 오른쪽 열에 이름이 지정된 사용자 **[!UICONTROL 타겟 ID]**&#x200B;아래에 표시된 대로 를 클릭합니다.

![명명된 사용자 매핑](../../assets/catalog/mobile-engagement/airship-tags/mapping-option-2.png)

채널, 즉 디바이스에 매핑해야 하는 식별자의 경우 소스를 기반으로 적절한 채널에 매핑합니다. 다음 이미지는 Google Advertising ID를 [!DNL Airship] Android 채널.

![비행선에 연결 태그](../../assets/catalog/mobile-engagement/airship-tags/select-source-identity.png)
![비행선에 연결 태그](../../assets/catalog/mobile-engagement/airship-tags/select-target-identity.png)
![채널 매핑](../../assets/catalog/mobile-engagement/airship-tags/mapping-option.png)

## 데이터 사용 및 관리 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스 시행, 참조: [데이터 거버넌스 개요](../../../data-governance/home.md).
