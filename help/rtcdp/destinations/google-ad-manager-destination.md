---
title: Google 광고 관리자 대상
seo-title: Google 광고 관리자 대상
description: '이전에 발행자를 위한 DoubleClick 또는 DoubleClick AdX로 알려진 Google Ad Manager는 발행자가 비디오 및 모바일 앱을 통해 자사 웹 사이트에서 광고 표시를 관리할 수 있는 수단을 제공하는 Google의 광고 서비스 플랫폼입니다. '
seo-description: '이전에 발행자를 위한 DoubleClick 또는 DoubleClick AdX로 알려진 Google Ad Manager는 발행자가 비디오 및 모바일 앱을 통해 자사 웹 사이트에서 광고 표시를 관리할 수 있는 수단을 제공하는 Google의 광고 서비스 플랫폼입니다. '
translation-type: tm+mt
source-git-commit: dc5ee796ca390d06fc8e08bd6c30e88a0d96dd53
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 0%

---


# Google 광고 관리자 대상

## 개요

이전에 발행자를 위한 DoubleClick 또는 DoubleClick AdX로 알려진 Google Ad Manager는 발행자가 비디오 및 모바일 앱을 통해 자사 웹 사이트에서 광고 표시를 관리할 수 있는 수단을 제공하는 Google의 광고 서비스 플랫폼입니다.

## 대상 사양

Google Ad Manager 대상에만 해당되는 다음 세부 사항을 참고하십시오.

* 다음 ID를 Google 광고 관리자 [대상으로](../../identity-service/namespaces.md) 전송할 수 있습니다. **Google 쿠키 ID, IDFA, GAID, Roku ID, Microsoft ID, Amazon Fire TV ID**.
* 활성화된 대상은 Google 플랫폼에서 프로그래밍 방식으로 생성됩니다.
* Adobe 실시간 CDP에는 현재 성공적인 활성화를 검증하는 측정 지표가 포함되어 있지 않습니다. 통합을 확인하고 대상 타깃팅 크기를 이해하려면 Google의 대상 수를 참조하십시오.

>[!IMPORTANT]
>
>Google Ad Manager를 사용하여 첫 번째 대상을 만들고 이전에 Experience Cloud ID Service에서 [ID 동기화 기능을](https://docs.adobe.com/content/help/en/id-service/using/id-service-api/methods/idsync.html) 활성화하지 않은 경우(Audience Manager 또는 다른 응용 프로그램 사용) Adobe Consulting 또는 고객 지원 센터에 연락하여 ID 동기화를 활성화하십시오. 이전에 Audience Manager에서 Google 통합을 설정한 경우 설정한 ID 동기화가 Adobe Real-time CDP로 전달됩니다.

## 전제 조건

### 허용 목록

>[!NOTE]
>
>Adobe 실시간 CDP에서 첫 번째 Google Ad Manager 대상을 설정하기 전에 허용 목록이 필수입니다. 대상을 만들기 전에 아래에 설명된 목록 허용 프로세스가 Google에서 완료되었는지 확인하십시오.

Adobe 실시간 CDP에서 Google Ad Manager 대상을 만들려면 Google에 연락하여 Adobe가 허용된 데이터 공급자 목록에 포함되고, 계정이 허용 목록에 추가되도록 해야 합니다. Google에 연락하여 다음 정보를 제공합니다.

* **계정 ID** : Google의 Adobe 계정 ID입니다. 이 ID를 얻으려면 Adobe 고객 지원 센터 또는 Adobe 담당자에게 문의하십시오.
* **고객 ID** : Google의 Adobe 고객 계정 ID입니다. 이 ID를 얻으려면 Adobe 고객 지원 센터 또는 Adobe 담당자에게 문의하십시오.
* **네트워크 ID** : Google 광고 관리자의 계정입니다.
* **대상 링크 ID** : Google 광고 관리자의 계정입니다.
* 계정 유형. **Google** 또는 **AdX 구매자별 DFP**.

## 대상 만들기

1. 연결 **[!UICONTROL > 대상에서]** Google 광고 관리자를 선택하고 대상 **[!UICONTROL 만들기를 선택합니다]**.
   ![Google 광고 관리자 대상 연결](/help/rtcdp/destinations/assets/google-1-destination.png)

2. 대상 만들기 워크플로우에서 대상에 대한 [!UICONTROL 기본 정보를] 입력합니다. <br>

   ![기본 정보 Google 광고 관리자](/help/rtcdp/destinations/assets/google-1-basic-information.png)
* **[!UICONTROL 이름]**: 이 대상에 대한 기본 이름을 입력합니다.
* **[!UICONTROL 설명]**: 선택 사항. 예를 들어 이 대상을 사용하는 캠페인을 언급할 수 있습니다.
* **[!UICONTROL 계정 유형]**: Google의 계정에 따라 옵션을 선택합니다.
   * 게시자 `DFP by Google` 에 대해 DoubleClick 사용
   * Google AdX `AdX buyer` 에 사용
* **[!UICONTROL 계정 ID]**: Google로 계정 ID를 입력합니다. 네트워크 ID 또는 대상 링크 ID일 수 있습니다. 일반적으로 8자리 ID입니다.

>[!NOTE]
>
>Google Ad Manager 대상을 설정할 때는 Google 계정 관리자 또는 Adobe 담당자에게 문의하여 보유하고 있는 계정 유형을 파악하십시오.

## Google 광고 관리자에 세그먼트 활성화

Google 광고 관리자에 세그먼트를 활성화하는 방법에 대한 지침은 대상에 [데이터 활성화를 참조하십시오](/help/rtcdp/destinations/activate-destinations.md).