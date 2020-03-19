---
title: Google 대상
seo-title: Google 대상
description: Adobe 실시간 CDP는 Google과 통합되어 있으므로 DV360, Google Ad Manager, Google AdWords 및 Google AdX에서 데이터를 실행하고 활성화할 수 있습니다.
seo-description: Adobe 실시간 CDP는 Google과 통합되어 있으므로 DV360, Google Ad Manager, Google AdWords 및 Google AdX에서 데이터를 실행하고 활성화할 수 있습니다.
translation-type: tm+mt
source-git-commit: 5396bee00044e5046bd768a863fceca0aec1d24e

---


# Google 대상

## 개요

Adobe 실시간 CDP는 Google과 통합되어 있으므로 DV360, Google Ad Manager, Google AdWords Display 및 Google AdX에서 데이터를 실행하고 활성화할 수 있습니다.

## 대상 사양

Google 대상에 대한 다음 세부 사항을 참고하십시오.

* 다음 ID를 Google [대상으로](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md) 보낼 수 있습니다.Google **쿠키 ID, IDFA, GAID**.
* 활성화된 대상은 Google 플랫폼에서 프로그래밍 방식으로 생성됩니다.
* Adobe Real-time CDP에는 현재 성공적인 활성화를 확인하는 측정 지표가 포함되어 있지 않습니다. 통합을 확인하고 데이터 드롭다운을 이해하려면 Google의 대상 수를 참조하십시오.

## 전제 조건

### 화이트리스트

Adobe Real-time CDP에서 Google 대상을 연결하려면 Google에 계정을 허용 목록에 추가하도록 요청해야 합니다. Google에 연락하여 다음 정보를 제공합니다.

* **계정 ID** :이것은 Google의 Adobe 계정 ID입니다. 이 ID를 얻으려면 Adobe 지원에 문의하십시오.
* **고객 ID** :이것은 Google의 Adobe 고객 계정 ID입니다. 이 ID를 얻으려면 Adobe 지원에 문의하십시오.
* **파트너 ID** :Google의 세 자리 파트너 ID입니다.
* **네트워크 ID** :이것은 귀하의 Google 계정입니다.
* **대상 링크 ID** :이것은 귀하의 Google 계정입니다.
* 계정 유형. 이것은 광고주 초대, **초대장 파트너**, **DFP**, **Ad** AdWords, ******** Covering AdX일 수 있습니다.


## 연결 대상

1. 연결 **[!UICONTROL > 대상에서]** Google을 선택하고 대상 **[!UICONTROL 만들기를 선택합니다]**.
   ![Google 대상 연결](/help/rtcdp/destinations/assets/google-destination.png)

2. Connect 대상 마법사에서 대상의 기본 정보를 입력합니다.
   ![기본 정보 Google](/help/rtcdp/destinations/assets/google-basic-information.png)
* **이름**:이 대상에 대한 기본 이름을 입력합니다.
* **설명**:선택 사항입니다. 예를 들어 이 대상을 사용하는 캠페인을 언급할 수 있습니다.
* **계정 유형**:Google의 계정에 따라 옵션을 선택합니다.
   * Google DV360 `Invite advertiser` 에 사용
   * Google DV360 `Invite partner` 에 사용
   * Google 광고 관리자에 `DFP by Google` 사용
   * Google AdWords `AdWords` 표시에 사용
   * Google AdX `AdX buyer` 에 사용
* **계정 ID**:Google로 계정 ID를 입력합니다.

>[!NOTE]
>
>Google 대상을 설정할 때는 Google 계정 관리자 또는 Adobe 담당자에게 연락하여 귀하의 계정이 속하는 제품 유형을 파악하십시오. Google DV360의 경우 Google 계정 관리자에게 계정이 속하는 제품 유형을 문의하십시오. 

## Google에 세그먼트 활성화

Google에 세그먼트를 활성화하는 방법에 대한 지침은 대상에 데이터 [활성화를 참조하십시오](/help/rtcdp/destinations/activate-destinations.md).