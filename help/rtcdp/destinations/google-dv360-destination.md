---
title: Google Display & Video 360 대상
seo-title: Google Display & Video 360 대상
description: Display & Video 360(이전 DoubleClick Bid Manager)은 디스플레이, 비디오 및 모바일 인벤토리 소스에서 타겟팅된 디지털 캠페인 및 대상 리타겟팅을 실행하는 데 사용되는 도구입니다.
seo-description: 'Display & Video 360(이전 DoubleClick Bid Manager)은 디스플레이, 비디오 및 모바일 인벤토리 소스에서 타겟팅된 디지털 캠페인 및 대상 리타겟팅을 실행하는 데 사용되는 도구입니다. '
translation-type: tm+mt
source-git-commit: 810028edc662a7f52484e37cf0fbdfafe5db650f

---


# Google Display &amp; Video 360 대상

## 개요

디스플레이 및 비디오 360(이전 DoubleClick 입찰 관리자)은 디스플레이, 비디오 및 모바일 인벤토리 소스에서 리타겟팅된 디지털 캠페인 및 대상 타깃팅을 실행하는 데 사용되는 도구입니다.

## 대상 사양

Google Display &amp; Video 360 대상에만 해당되는 다음 세부 사항을 참고하십시오.

* Google Display &amp; Video 360 대상으로 다음 [ID를](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md) 전송할 수 있습니다.Google **쿠키 ID, IDFA, GAID, Roku ID, Microsoft ID, Amazon Fire TV ID**.
* 활성화된 대상은 Google 플랫폼에서 프로그래밍 방식으로 생성됩니다.
* Adobe Real-time CDP에는 현재 성공적인 활성화를 확인하는 측정 지표가 포함되어 있지 않습니다. 통합을 확인하고 대상 타깃팅 크기를 이해하려면 Google의 대상 수를 참조하십시오.

>[!IMPORTANT]
>
>Google Display &amp; Video 360을 사용하여 첫 번째 대상을 만들고 이전 Experience Cloud ID Service에서 [ID 동기화 기능을](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) 활성화하지 않은 경우(Adobe Audience Manager 또는 기타 애플리케이션 포함) Adobe Consulting 또는 고객 지원 센터에 문의하여 ID 동기화를 활성화하십시오. 이전에 Audience Manager에서 Google 통합을 설정한 경우 설정한 ID 동기화를 Adobe Real-time CDP로 이월합니다.

## 전제 조건

### 화이트리스트

>[!NOTE]
>
>Adobe Real-time CDP에서 첫 번째 Google Display &amp; Video 360 대상을 설정하기 전에 화이트리스트 기능이 필요합니다. 대상을 만들기 전에 아래에 설명된 화이트 리스트 프로세스가 Google에서 완료되었는지 확인하십시오.

Adobe Real-time CDP에서 Google Display &amp; Video 360 대상을 만들기 전에 Google에 데이터 제공자로 허용 목록에 추가되고 허용 목록에 추가되도록 요청해야 합니다. Google에 연락하여 다음 정보를 제공합니다.

* **계정 ID** :이것은 Google의 Adobe 계정 ID입니다. 이 ID를 얻으려면 Adobe 고객 지원 센터 또는 Adobe 담당자에게 문의하십시오.
* **고객 ID** :이것은 Google의 Adobe 고객 계정 ID입니다. 이 ID를 얻으려면 Adobe 고객 지원 센터 또는 Adobe 담당자에게 문의하십시오.
* **계정 유형**:디스플레이 및 비디오 360 계정의 특정 브랜드에만 대상을 공유할 수 **[!DNL Invite advertiser]** 있도록 하거나 디스플레이 및 비디오 360 계정의 모든 브랜드에 대상을 공유할 **[!DNL Invite partner]** 수 있도록 하는 데 사용합니다.

## 대상 만들기

1. 에서 Google **[!UICONTROL Connections > Destinations]** Display &amp; Video 360을 선택하고 **[!UICONTROL Create destination]**선택합니다.
   ![Google Display &amp; Video 360 대상 연결](/help/rtcdp/destinations/assets/google-dv360-destination.png)

2. 대상 만들기 마법사에서 대상에 대한 기본 정보를 입력합니다.
   ![기본 정보 Google Display &amp; Video 360](/help/rtcdp/destinations/assets/google-dv360-basic-information.png)
* **이름**:이 대상에 대한 기본 이름을 입력합니다.
* **설명**:선택 사항입니다. 예를 들어 이 대상을 사용하는 캠페인을 언급할 수 있습니다.
* **계정 유형**:Google의 계정에 따라 옵션을 선택합니다.
   * 디스플레이 및 비디오 360 계정에서 특정 브랜드에만 대상을 공유할 수 `Invite Advertiser` 있도록 하는 데 사용합니다.
   * 디스플레이 및 비디오 360 계정의 모든 브랜드에 대상을 공유할 수 `Invite Partner` 있도록 허용하는 데 사용합니다.
* **계정 ID**:Google로 **[!DNL Invite partner]** 또는 **[!DNL Invite advertiser]** 계정 ID를 입력합니다. 일반적으로 이것은 6 또는 7자리 ID입니다.

>[!NOTE]
>
>Google Display &amp; Video 360 대상을 설정할 때는 Google 계정 관리자 또는 Adobe 담당자에게 문의하여 보유하고 있는 계정 유형을 파악하십시오.

## Google 디스플레이 및 비디오 360으로 세그먼트 활성화

Google 디스플레이 및 비디오 360에 세그먼트를 활성화하는 방법에 대한 지침은 대상에 데이터 [활성화를 참조하십시오](/help/rtcdp/destinations/activate-destinations.md).