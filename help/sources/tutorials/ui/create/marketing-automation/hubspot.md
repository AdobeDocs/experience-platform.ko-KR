---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: UI에서 HubSpot 소스 커넥터 만들기
topic: overview
translation-type: tm+mt
source-git-commit: 2162c66b1664ecaaf0b609fe3f7ccf58c4a5d31d
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 0%

---


# UI에서 HubSpot 소스 커넥터 만들기

> [!NOTE]
> HubSpot 커넥터가 베타에 있습니다. 기능 및 설명서는 변경될 수 있습니다.

Adobe Experience Platform의 소스 커넥터는 외부에서 소스 데이터를 예약된 기준으로 인제스트하는 기능을 제공합니다. 이 자습서에서는 플랫폼 사용자 인터페이스를 사용하여 HubSpot 소스 커넥터를 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소에 대해 작업해야 합니다.

* [XDM(Experience Data Model) 시스템](../../../../../xdm/home.md): 고객 경험 데이터를 구성하는 표준 프레임워크
   * [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례 등 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 정의 스키마를 생성하는 방법을 알아봅니다.
* [실시간 고객 프로필](../../../../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 HubSpot 베이스 연결이 있는 경우 이 문서의 나머지 부분을 건너뛰고 마케팅 자동화 데이터 흐름 [구성에 대한 자습서로 진행할 수 있습니다](../../dataflow/marketing-automation.md).

### 필요한 자격 증명 수집

플랫폼의 허브 스팟 계정에 액세스하려면 다음 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `clientId` | HubSpot 응용 프로그램과 연결된 클라이언트 ID. |
| `clientSecret` | HubSpot 응용 프로그램과 연결된 클라이언트 암호입니다. |
| `accessToken` | OAuth 통합을 처음 인증할 때 얻은 액세스 토큰입니다. |
| `refreshToken` | OAuth 통합을 처음 인증할 때 얻은 새로 고침 토큰입니다. |

시작하는 방법에 대한 자세한 내용은 이 [HubSpot 문서를 참조하십시오](https://developers.hubspot.com/docs/methods/oauth2/oauth2-overview).

## HubSpot 계정 연결

필요한 자격 증명을 수집했으면 아래 절차에 따라 HubSpot 계정을 플랫폼에 연결하는 새 인바운드 기본 연결을 만들 수 있습니다.

Adobe <a href="https://platform.adobe.com" target="_blank">Experience Platform에</a> 로그인한 다음 왼쪽 탐색 **모음에서** Sources를 *선택하여* Sources 작업 영역에액세스합니다. [ *카탈로그* ] 화면에는 인바운드 기본 연결을 만들 수 있는 다양한 소스가 표시되며, 각 소스에는 연관된 기존 기본 연결의 수가 표시됩니다.

[ *마케팅 자동화* ] 카테고리 아래에서 **HubSpot** 을 선택하여 화면 오른쪽에 정보 막대를 표시합니다. 정보 표시줄에는 선택한 소스에 대한 간단한 설명과 소스와 연결하거나 설명서를 보는 옵션이 제공됩니다. 새 인바운드 기본 연결을 만들려면 **Connect 소스를 선택합니다**.

![카탈로그](../../../../images/tutorials/create/hubspot/catalog.png)

HubSpot *에 연결* 페이지가 나타납니다. 이 페이지에서 새 자격 증명이나 기존 자격 증명을 사용할 수 있습니다.

### 새 계정

새 자격 증명을 사용 중인 경우 **새 계정을 선택합니다**. 표시되는 입력 양식에서 이름, 선택적 설명 및 HubSpot 자격 증명으로 기본 연결을 제공합니다. 완료되면 **Connect를** 선택한 다음 새 기본 연결이 설정될 때까지 잠시 기다려 주십시오.

![connect](../../../../images/tutorials/create/hubspot/connect.png)

### 기존 계정

기존 계정을 연결하려면 연결하려는 HubSpot 계정을 선택한 다음 **다음을** 선택하여 진행하십시오.

![기존](../../../../images/tutorials/create/hubspot/existing.png)

## 다음 단계

이 튜토리얼을 따라 HubSpot 계정에 기본 연결을 설정했습니다. 이제 다음 튜토리얼로 계속 이동하여 마케팅 자동화 시스템 데이터를 [Platform으로 가져오도록 데이터 흐름을 구성할 수 있습니다](../../dataflow/marketing-automation.md).