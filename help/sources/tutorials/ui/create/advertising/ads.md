---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: UI에서 Google 광고 소스 커넥터 만들기
topic: overview
translation-type: tm+mt
source-git-commit: 3b5821d641d35e1190ea9fecfd4def5beced6ecc

---


# UI에서 Google 광고 소스 커넥터 만들기

Adobe Experience Platform의 소스 커넥터는 외부 소스 데이터를 일정 단위로 인제스트할 수 있는 기능을 제공합니다. 이 자습서에서는 플랫폼 사용자 인터페이스를 사용하여 Google 광고 소스 커넥터를 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

* [XDM(Experience Data Model) 시스템](../../../../../xdm/home.md):Adobe Experience Platform을 통해 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의](../../../../../xdm/schema/composition.md)기본 사항:스키마 컴포지션의 주요 원칙 및 모범 사례 등 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md):스키마 편집기 UI를 사용하여 사용자 정의 스키마를 만드는 방법을 알아봅니다.
* [실시간 고객 프로필](../../../../../profile/home.md):다양한 소스의 데이터를 집계하여 통합된 실시간 고객 프로파일을 제공합니다.

이미 Google 광고 기본 연결이 있는 경우 이 문서의 나머지 부분을 건너뛰고 데이터 흐름 [구성에 대한 자습서로 진행할 수 있습니다](../../dataflow/payments.md)

### 필요한 자격 증명 수집

Google 광고 계정 플랫폼에 액세스하려면 다음 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `clientCustomerId` | 광고 계정의 클라이언트 고객 ID. |
| `developerToken` | 관리자 계정과 연결된 개발자 토큰입니다. |
| `refreshToken` | 광고에 대한 액세스 권한을 인증하기 위해 Google에서 얻은 새로 고침 토큰입니다. |
| `clientId` | 새로 고침 토큰을 획득하는 데 사용되는 Google 애플리케이션의 클라이언트 ID입니다. |
| `clientSecret` | 새로 고침 토큰을 획득하는 데 사용되는 Google 애플리케이션의 클라이언트 암호입니다. |

시작하는 방법에 대한 자세한 내용은 이 Google 광고 [문서를](https://developers.google.com/adwords/api/docs/guides/authentication)참조하십시오.

## Google 광고 계정 연결

필요한 자격 증명을 수집했으면 아래 절차에 따라 Google 광고 계정을 플랫폼에 연결하는 새 인바운드 기본 연결을 만들 수 있습니다.

Adobe Experience <a href="https://platform.adobe.com" target="_blank">Platform에</a> 로그인한 다음 **왼쪽 탐색** 표시줄에서 Sources를 선택하여 *Sources* 작업 영역에 액세스할 수있습니다. [ *카탈로그* ] 화면에는 인바운드 기본 연결을 만들 수 있는 다양한 소스가 표시되며, 각 소스에는 연결된 기존 기본 연결의 수가 표시됩니다.

광고 *카테고리* 아래에서 **Google 광고를** 선택하여 화면 오른쪽에 정보 막대를 표시합니다. 정보 표시줄은 선택한 소스에 대한 간단한 설명과 소스와 연결하거나 설명서를 보는 옵션을 제공합니다. 새 인바운드 기본 연결을 만들려면 Connect **소스를**&#x200B;선택합니다.

![카탈로그](../../../../images/tutorials/create/ads/catalog.png)

Google *광고에 연결* 페이지가 나타납니다. 이 페이지에서 새 자격 증명이나 기존 자격 증명을 사용할 수 있습니다.

### 새 계정

새 자격 증명을 사용하는 경우 새 계정을 **선택합니다**. 표시되는 입력 양식에서 이름, 선택적 설명 및 Google 광고 자격 증명으로 기본 연결을 제공합니다. 완료되면 Connect **를** 선택한 다음 새 기본 연결이 설정될 시간을 허용합니다.

![connect](../../../../images/tutorials/create/ads/connect.png)

### 기존 계정

기존 계정을 연결하려면 연결할 Google 광고 계정을 선택한 다음 **다음을** 선택하여 진행합니다.

![기존](../../../../images/tutorials/create/ads/existing.png)

## 다음 단계

이 자습서를 따라 Google 광고 계정에 대한 기본 연결을 설정했습니다. 이제 다음 튜토리얼을 계속 진행하고 데이터 흐름을 [구성하여 광고 데이터를 Platform으로 가져올 수 있습니다](../../dataflow/advertising.md).