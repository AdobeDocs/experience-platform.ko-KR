---
title: UI에서 Google Ads Source 연결 만들기
description: Adobe Experience Platform UI를 사용하여 Google Ads 소스 연결을 만드는 방법을 알아봅니다.
exl-id: 33dd2857-aed3-4e35-bc48-1c756a8b3638
source-git-commit: ce3dabe4ab08a41e581b97b74b3abad352e3267c
workflow-type: tm+mt
source-wordcount: '680'
ht-degree: 2%

---

# UI에서 Google Ads 소스 연결 만들기

>[!WARNING]
>
>[!DNL Google Ads] 원본을 일시적으로 사용할 수 없습니다. Adobe이 이 소스의 문제를 해결하기 위해 노력하고 있습니다.

>[!NOTE]
>
>Google Ads 소스는 Beta 버전입니다. 베타 레이블 소스를 사용하는 방법에 대한 자세한 내용은 [소스 개요](../../../../home.md#terms-and-conditions)를 참조하십시오.

이 자습서에서는 Adobe Experience Platform 사용자 인터페이스를 사용하여 Google Ads 소스 연결을 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 다음 Experience Platform 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 유효한 Google 광고 연결이 있는 경우 이 문서의 나머지 부분을 건너뛰고 [데이터 흐름 구성](../../dataflow/advertising.md)에 대한 자습서로 진행할 수 있습니다.

### 필요한 자격 증명 수집

Google Ads 계정 플랫폼에 액세스하려면 다음 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| 클라이언트 고객 ID | 클라이언트 고객 ID는 Google Ads API로 관리하려는 Google Ads 클라이언트 계정에 해당하는 계정 번호입니다. 이 ID는 `123-456-7890`의 템플릿을 따릅니다. |
| 로그인 고객 ID | 로그인 고객 ID는 Google Ads Manager 계정에 해당하는 계정 번호이며 특정 운영 고객으로부터 보고서 데이터를 가져오는 데 사용됩니다. 로그인 고객 ID에 대한 자세한 내용은 [Google Ads API 설명서](https://developers.google.com/search-ads/reporting/concepts/login-customer-id)를 참조하세요. |
| 개발자 토큰 | 개발자 토큰을 사용하면 Google Ads API에 액세스할 수 있습니다. 동일한 개발자 토큰을 사용하여 모든 Google Ads 계정에 대해 요청할 수 있습니다. [관리자 계정에 로그인](https://ads.google.com/home/tools/manager-accounts/)한 다음 API 센터 페이지로 이동하여 개발자 토큰을 검색하십시오. |
| 토큰 새로 고침 | 새로 고침 토큰은 [!DNL OAuth2] 인증의 일부입니다. 이 토큰을 사용하면 액세스 토큰이 만료된 후 다시 생성할 수 있습니다. |
| 클라이언트 ID | 클라이언트 ID는 [!DNL OAuth2] 인증의 일부로 클라이언트 암호와 함께 사용됩니다. 클라이언트 ID와 클라이언트 암호를 사용하면 Google에 대한 애플리케이션을 식별하여 애플리케이션이 계정을 대신하여 작동할 수 있습니다. |
| 클라이언트 암호 | 클라이언트 암호는 [!DNL OAuth2] 인증의 일부로 클라이언트 ID와 함께 사용됩니다. 클라이언트 ID와 클라이언트 암호를 사용하면 Google에 대한 애플리케이션을 식별하여 애플리케이션이 계정을 대신하여 작동할 수 있습니다. |

[Google 광고 시작에 대한 자세한 내용](https://developers.google.com/google-ads/api/docs/first-call/overview)은 API 개요 문서를 참조하십시오.

## Google 광고 계정 연결

Platform UI의 왼쪽 탐색 막대에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 [!UICONTROL 소스] 작업 영역에 액세스합니다. [!UICONTROL 카탈로그] 화면에 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

**[!UICONTROL Advertising]** 범주에서 **[!UICONTROL Google 광고]**&#x200B;를 선택한 다음 **[!UICONTROL 데이터 추가]**&#x200B;를 선택합니다.

![Experience Platform UI의 소스 카탈로그.](../../../../images/tutorials/create/ads/catalog.png).

**[!UICONTROL Google 광고에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정에 연결하려면 연결할 Google Ads 계정을 선택한 후 **[!UICONTROL 다음]**&#x200B;을(를) 선택하여 계속합니다.

![원본 워크플로의 기존 계정에 대한 선택 페이지입니다.](../../../../images/tutorials/create/ads/existing.png).

### 새 계정

새 자격 증명을 사용하는 경우 **[!UICONTROL 새 계정]**&#x200B;을(를) 선택하십시오. 표시되는 입력 양식에서 이름, 선택적 설명 및 Google Ads 자격 증명을 제공합니다. 완료되면 **[!UICONTROL 소스에 연결]**&#x200B;을 선택한 다음 새 연결을 설정할 수 있는 시간을 허용하세요.

![원본 워크플로의 새 계정 인터페이스.](../../../../images/tutorials/create/ads/new.png).

## 다음 단계

이 자습서에 따라 Google Ads 계정에 대한 연결을 설정했습니다. 이제 다음 자습서를 계속 진행하고 [광고 데이터를 플랫폼으로 가져오도록 데이터 흐름을 구성](../../dataflow/advertising.md)할 수 있습니다.
