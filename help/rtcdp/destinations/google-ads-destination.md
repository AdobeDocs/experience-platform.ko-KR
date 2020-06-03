---
title: Google 광고 대상
seo-title: Google 광고 대상
description: 이전에 Google AdWords로 알려졌던 Google Ads는 기업에서 텍스트 기반 검색, 그래픽 디스플레이, YouTube 비디오 및 인앱 모바일 디스플레이에서 클릭당 광고를 지불하는 온라인 광고 서비스입니다.
seo-description: 이전에 Google AdWords로 알려졌던 Google Ads는 기업에서 텍스트 기반 검색, 그래픽 디스플레이, YouTube 비디오 및 인앱 모바일 디스플레이에서 클릭당 광고를 지불하는 온라인 광고 서비스입니다.
translation-type: tm+mt
source-git-commit: 121ae74e9c352b1f6fc12093d815e711ebd817b8
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---


# Google 광고 대상

## 개요

이전에 Google AdWords로 알려졌던 Google Ads는 기업에서 텍스트 기반 검색, 그래픽 디스플레이, YouTube 비디오 및 인앱 모바일 디스플레이에서 클릭당 광고를 지불하는 온라인 광고 서비스입니다.

## 대상 사양

Google 광고 대상에만 해당되는 다음 세부 사항을 참고하십시오.

* Google 광고 대상으로 다음 [ID를](../../identity-service/namespaces.md) 전송할 수 있습니다. **Google 쿠키 ID, IDFA, GAID, Roku ID, Microsoft ID, Amazon Fire TV ID**.
* 활성화된 대상은 Google 플랫폼에서 프로그래밍 방식으로 생성됩니다.
* Adobe 실시간 CDP에는 현재 성공적인 활성화를 검증하는 측정 지표가 포함되어 있지 않습니다. 통합을 확인하고 대상 타깃팅 크기를 이해하려면 Google의 대상 수를 참조하십시오.

>[!IMPORTANT]
>
>Google Ads를 사용하여 첫 번째 대상을 만들려는 경우 이전에 Experience Cloud ID Service에서 [ID 동기화 기능을](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) 활성화하지 않은 경우(Audience Manager 또는 다른 응용 프로그램 사용) Adobe Consulting 또는 고객 지원 센터에 연락하여 ID 동기화를 활성화하십시오. 이전에 Audience Manager에서 Google 통합을 설정한 경우 설정한 ID 동기화가 Adobe Real-time CDP로 전달됩니다.

## 전제 조건

### 기존 Google 광고 계정

Google은 타사 공급업체와의 새로운 Google 광고 통합을 일시 중지했습니다. 다음 섹션의 화이트 리스트 단계를 수행하고 Adobe 실시간 CDP에서 Google 광고 대상을 만들려면 Google 광고와 기존 통합이 있어야 합니다.

### 화이트 리스트

>[!NOTE]
>
>Adobe 실시간 CDP에서 첫 번째 Google 광고 대상을 설정하기 전에 허용 목록은 필수 사항입니다. 대상을 만들기 전에 Google에서 아래 설명된 허용 목록 프로세스가 완료되었는지 확인하십시오.

Adobe 실시간 CDP에서 Google 광고 대상을 만들기 전에 Google에 데이터 제공자로 허용 목록에 추가되고 계정을 허용 목록에 추가하도록 요청해야 합니다. Google에 연락하여 다음 정보를 제공합니다.

* **계정 ID** : Google의 Adobe 계정 ID입니다. 이 ID를 얻으려면 Adobe 고객 지원 센터 또는 Adobe 담당자에게 문의하십시오.
* **고객 ID** : Google의 Adobe 고객 계정 ID입니다. 이 ID를 얻으려면 Adobe 고객 지원 센터 또는 Adobe 담당자에게 문의하십시오.
* 계정 유형: **AdWords**
* **Google AdWords ID** : Google의 ID입니다. ID 형식은 일반적으로 123-456-7890입니다.

## 대상 만들기

1. 연결 **[!UICONTROL > 대상에서]** Google 광고를 선택하고 대상 **[!UICONTROL 만들기를 선택합니다]**.
   ![Google 광고 대상 연결](/help/rtcdp/destinations/assets/google-2-destination.png)

2. 대상 만들기 워크플로우에서 대상에 대한 [!UICONTROL 기본 정보를] 입력합니다. <br>
   ![기본 정보 Google 광고](/help/rtcdp/destinations/assets/google-2-basic-information.png)
* **[!UICONTROL 이름]**: 이 대상에 대한 기본 이름을 입력합니다.
* **[!UICONTROL 설명]**: 선택 사항. 예를 들어 이 대상을 사용하는 캠페인을 언급할 수 있습니다.
* **[!UICONTROL 계정 유형]**: AdWords만 사용할 수 있습니다.
* **[!UICONTROL 계정 ID]**: Google 광고로 계정 ID를 입력합니다. ID 형식은 일반적으로 123-456-7890입니다.

## Google 광고에 세그먼트 활성화

Google 광고에 세그먼트를 활성화하는 방법에 대한 지침은 대상에 [데이터 활성화를 참조하십시오](/help/rtcdp/destinations/activate-destinations.md).

