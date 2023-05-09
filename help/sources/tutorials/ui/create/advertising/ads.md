---
title: UI에서 Google 광고 소스 연결 만들기
description: Adobe Experience Platform UI를 사용하여 Google Ads 소스 연결을 만드는 방법을 알아봅니다.
exl-id: 33dd2857-aed3-4e35-bc48-1c756a8b3638
source-git-commit: ac87434c857a39f4be3714cba57519cbb4fa54a6
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 0%

---

# UI에서 Google Ads 소스 연결 만들기

>[!NOTE]
>
>Google 광고 소스가 베타 버전입니다. 자세한 내용은 [소스 개요](../../../../home.md#terms-and-conditions) 베타 레이블이 지정된 소스 사용에 대한 자세한 정보.

이 자습서에서는 Adobe Experience Platform 사용자 인터페이스를 사용하여 Google 광고 소스 연결을 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 작성 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 빌딩 블록에 대해 알아봅니다.
   * [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아보십시오.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 유효한 Google Ads 연결이 있는 경우 이 문서의 나머지 부분을 건너뛰고 다음의 자습서를 진행할 수 있습니다. [데이터 흐름 구성](../../dataflow/advertising.md)

### 필요한 자격 증명 수집

Google 광고 계정 플랫폼에 액세스하려면 다음 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| 클라이언트 고객 ID | 클라이언트 고객 ID는 Google 광고 API를 사용하여 관리하려는 Google Ads 클라이언트 계정에 해당하는 계정 번호입니다. 이 ID는 `123-456-7890`. |
| 로그인 고객 ID | 로그인 고객 ID는 Google 광고 관리자 계정에 해당하는 계정 번호이며 특정 운영 고객으로부터 보고서 데이터를 가져오는 데 사용됩니다. 로그인 고객 ID에 대한 자세한 내용은 [Google 광고 API 설명서](https://developers.google.com/google-ads/api/docs/migration/login-customer-id). |
| 개발자 토큰 | 개발자 토큰을 사용하면 Google 광고 API에 액세스할 수 있습니다. 동일한 개발자 토큰을 사용하여 모든 Google 광고 계정에 대해 요청을 수행할 수 있습니다. 다음 방법으로 개발자 토큰을 검색합니다. [manager 계정에 로그인](https://ads.google.com/home/tools/manager-accounts/) API 센터 페이지로 이동합니다. |
| 새로 고침 토큰 | 새로 고침 토큰은 [!DNL OAuth2] 인증. 이 토큰을 사용하면 액세스 토큰이 만료된 후 다시 생성할 수 있습니다. |
| 클라이언트 ID | 클라이언트 ID는 의 일부로 클라이언트 암호와 함께 사용됩니다 [!DNL OAuth2] 인증. 클라이언트 ID와 클라이언트 암호를 함께 사용하면 애플리케이션을 Google에 식별하여 계정을 대신하여 애플리케이션이 작동할 수 있습니다. |
| 클라이언트 암호 | 클라이언트 암호는 [!DNL OAuth2] 인증. 클라이언트 ID와 클라이언트 암호를 함께 사용하면 애플리케이션을 Google에 식별하여 계정을 대신하여 애플리케이션이 작동할 수 있습니다. |

에 대한 API 개요 문서를 참조하십시오 [Google 광고 시작에 대한 자세한 정보](https://developers.google.com/google-ads/api/docs/first-call/overview).

## Google 광고 계정 연결

플랫폼 UI에서 **[!UICONTROL 소스]** 왼쪽 탐색 모음에서 를 클릭하여 [!UICONTROL 소스] 작업 공간. 다음 [!UICONTROL 카탈로그] 화면에 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래에 **[!UICONTROL 광고]** 카테고리, 선택 **[!UICONTROL Google 광고]**&#x200B;를 선택한 다음 을 선택합니다. **[!UICONTROL 데이터 추가]**.

![Experience Platform UI의 소스 카탈로그.](../../../../images/tutorials/create/ads/catalog.png).

다음 **[!UICONTROL Google 광고에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정을 연결하려면 연결할 Google 광고 계정을 선택한 다음 을(를) 선택합니다 **[!UICONTROL 다음]** 계속 진행합니다.

![소스 워크플로우의 기존 계정에 대한 선택 페이지입니다.](../../../../images/tutorials/create/ads/existing.png).

### 새 계정

새 자격 증명을 사용하는 경우 **[!UICONTROL 새 계정]**. 표시되는 입력 양식에서 이름, 선택적 설명 및 Google 광고 자격 증명을 제공합니다. 완료되면 을 선택합니다 **[!UICONTROL 소스에 연결]** 그런 다음 새 연결이 설정될 시간을 허용합니다.

![소스 워크플로우의 새 계정 인터페이스입니다.](../../../../images/tutorials/create/ads/new.png).

## 다음 단계

이 자습서에 따라 Google 광고 계정에 대한 연결을 설정했습니다. 이제 다음 자습서를 계속 진행하고 [광고 데이터를 플랫폼으로 가져오도록 데이터 흐름 구성](../../dataflow/advertising.md).
