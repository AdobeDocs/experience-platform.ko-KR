---
title: Facebook 대상
seo-title: Facebook 대상
description: 해시된 이메일을 기반으로 고객 타깃팅, 개인화 및 억제를 위해 Facebook 캠페인에 대한 프로필을 활성화합니다.
seo-description: 해시된 이메일을 기반으로 고객 타깃팅, 개인화 및 억제를 위해 Facebook 캠페인에 대한 프로필을 활성화합니다.
translation-type: tm+mt
source-git-commit: bfcbc56f05fa1c3b5fafd57b1166e50130b6007d

---


# (베타) Facebook 대상

>[!IMPORTANT]
>
>Adobe Real-time CDP의 Facebook 대상은 현재 베타 버전이며 일부 사용자는 사용할 수 없습니다. 설명서 및 기능은 변경될 수 있습니다.

## 개요

해시된 이메일을 기반으로 고객 타깃팅, 개인화 및 억제를 위해 Facebook 캠페인에 대한 프로필을 활성화합니다.

## 대상 사양

### 활성화 유형

세그먼트 내보내기 - 세그먼트(대상)의 모든 멤버를 식별자(이름, 전화 번호 등)로 내보냅니다. Facebook 대상에 사용됨

## 전제 조건

대상 세그먼트를 다음으로 보내려면 먼저 다음 요구 사항을 [!DNL Facebook]충족해야 합니다.

1. 사용자 [!DNL Facebook] 계정에는 사용할 **광고 계정에 대해 캠페인** 관리 권한이 활성화되어 있어야 합니다.
2. Adobe Experience **Cloud** 비즈니스 계정을 광고 파트너에 [!DNL Facebook Ad Account]추가합니다.  `business ID=206617933627973`. 자세한 [내용은 비즈니스 관리자에 파트너](https://www.facebook.com/business/help/1717412048538897) 추가를 참조하십시오.
   >[!IMPORTANT]
   > Adobe Experience Cloud에 대한 권한을 구성할 때 캠페인 **관리** 권한을 활성화해야 합니다. 이 작업은 [!DNL Adobe Real-time CDP] 통합에 필요합니다.
3. 서비스 약관을 읽고 [!DNL Facebook Custom Audiences] 서명합니다. 이렇게 하려면, `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`어디로 `accountID` 가십시오 [!DNL Facebook Ad Account ID].


## 연결 대상

Facebook 대상을 연결하려면 소셜 [네트워크 대상 인증 워크플로우를](/help/rtcdp/destinations/social-network-destinations-workflow.md)참조하십시오.


## Facebook에 세그먼트 활성화

Facebook에 세그먼트를 활성화하는 방법에 대한 지침은 대상에 [데이터 활성화를 참조하십시오](/help/rtcdp/destinations/activate-destinations.md).