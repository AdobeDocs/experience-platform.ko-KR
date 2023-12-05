---
title: UI에서 Google 광고 소스 연결 만들기
description: Adobe Experience Platform UI를 사용하여 Google Ads 소스 연결을 만드는 방법을 알아봅니다.
exl-id: 33dd2857-aed3-4e35-bc48-1c756a8b3638
source-git-commit: 12ddf87d594b7e25a0356cd419e990b262c1734e
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 0%

---

# UI에서 Google Ads 소스 연결 만들기

>[!NOTE]
>
>Google Ads 소스는 Beta 버전입니다. 다음을 참조하십시오. [소스 개요](../../../../home.md#terms-and-conditions) beta 레이블 소스를 사용하는 방법에 대한 자세한 내용.

이 자습서에서는 Adobe Experience Platform 사용자 인터페이스를 사용하여 Google Ads 소스 연결을 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 다음 Experience Platform 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 정의 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 소스의 집계 데이터를 기반으로 통합 실시간 소비자 프로필을 제공합니다.

이미 유효한 Google Ads 연결이 있는 경우 이 문서의 나머지 부분을 건너뛰고 다음에 대한 자습서로 진행할 수 있습니다. [데이터 흐름 구성](../../dataflow/advertising.md)

### 필요한 자격 증명 수집

Google Ads 계정 플랫폼에 액세스하려면 다음 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| 클라이언트 고객 ID | 클라이언트 고객 ID는 Google Ads API로 관리하려는 Google Ads 클라이언트 계정에 해당하는 계정 번호입니다. 이 ID는 의 템플릿을 따릅니다. `123-456-7890`. |
| 로그인 고객 ID | 로그인 고객 ID는 Google Ads Manager 계정에 해당하는 계정 번호이며 특정 운영 고객으로부터 보고서 데이터를 가져오는 데 사용됩니다. 로그인 고객 ID에 대한 자세한 내용은 [Google Ads API 설명서](https://developers.google.com/search-ads/reporting/concepts/login-customer-id). |
| 개발자 토큰 | 개발자 토큰을 사용하면 Google Ads API에 액세스할 수 있습니다. 동일한 개발자 토큰을 사용하여 모든 Google Ads 계정에 대해 요청할 수 있습니다. 다음 방법으로 개발자 토큰 검색 [manager 계정에 로그인](https://ads.google.com/home/tools/manager-accounts/) 그런 다음 API 센터 페이지로 이동합니다. |
| 토큰 새로 고침 | 새로 고침 토큰은 [!DNL OAuth2] 인증. 이 토큰을 사용하면 액세스 토큰이 만료된 후 다시 생성할 수 있습니다. |
| 클라이언트 ID | 클라이언트 ID는 클라이언트 암호와 함께 의 일부로 사용됩니다 [!DNL OAuth2] 인증. 클라이언트 ID와 클라이언트 암호를 사용하면 Google에 대한 애플리케이션을 식별하여 애플리케이션이 계정을 대신하여 작동할 수 있습니다. |
| 클라이언트 암호 | 클라이언트 암호는 클라이언트 ID와 함께 의 일부로 사용됩니다 [!DNL OAuth2] 인증. 클라이언트 ID와 클라이언트 암호를 사용하면 Google에 대한 애플리케이션을 식별하여 애플리케이션이 계정을 대신하여 작동할 수 있습니다. |

다음에 대한 API 개요 문서 읽기 [Google 광고 시작하기에 대한 자세한 정보](https://developers.google.com/google-ads/api/docs/first-call/overview).

## Google 광고 계정 연결

Platform UI에서 를 선택합니다. **[!UICONTROL 소스]** 왼쪽 탐색 모음에서 다음 위치에 액세스: [!UICONTROL 소스] 작업 영역. 다음 [!UICONTROL 카탈로그] 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래 **[!UICONTROL 광고]** 범주, 선택 **[!UICONTROL Google 광고]**&#x200B;을 선택한 다음 을 선택합니다 **[!UICONTROL 데이터 추가]**.

![Experience Platform UI의 소스 카탈로그.](../../../../images/tutorials/create/ads/catalog.png).

다음 **[!UICONTROL Google 광고에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정을 연결하려면 연결할 Google Ads 계정을 선택한 다음 을 선택합니다. **[!UICONTROL 다음]** 계속합니다.

![소스 워크플로우의 기존 계정에 대한 선택 페이지입니다.](../../../../images/tutorials/create/ads/existing.png).

### 새 계정

새 자격 증명을 사용하는 경우 다음을 선택합니다 **[!UICONTROL 새 계정]**. 표시되는 입력 양식에서 이름, 선택적 설명 및 Google Ads 자격 증명을 제공합니다. 완료되면 다음을 선택합니다. **[!UICONTROL 소스에 연결]** 그런 다음 새 연결을 설정하는 데 시간이 걸릴 수 있습니다.

![소스 워크플로우의 새 계정 인터페이스입니다.](../../../../images/tutorials/create/ads/new.png).

## 다음 단계

이 자습서에 따라 Google Ads 계정에 대한 연결을 설정했습니다. 이제 다음 튜토리얼을 계속 진행하여 [advertising 데이터를 Platform으로 가져오는 데이터 흐름 구성](../../dataflow/advertising.md).
