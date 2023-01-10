---
keywords: Experience Platform;홈;인기 항목;일반 REST API
title: UI에서 일반 REST API 소스 연결 만들기
type: Tutorial
description: Adobe Experience Platform UI를 사용하여 일반 REST API 소스 연결을 만드는 방법을 알아봅니다.
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 1%

---

# 만들기 [!DNL Generic REST API] UI의 소스 연결

>[!NOTE]
>
> 다음 [!DNL Generic REST API] 소스가 베타 버전입니다. 자세한 내용은 [소스 개요](../../../../home.md#terms-and-conditions) 베타 레이블이 지정된 커넥터 사용에 대한 자세한 정보.

이 자습서에서는 을(를) 만드는 단계를 제공합니다 [!DNL Generic REST API] Adobe Experience Platform 사용자 인터페이스를 사용한 소스 커넥터.

## 시작하기

이 자습서에서는 Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [소스](../../../../home.md): Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

### 필요한 자격 증명 수집

에 액세스하려면 [!DNL Generic REST API] 플랫폼의 계정에서는 선택한 인증 유형에 유효한 자격 증명을 제공해야 합니다. 일반 REST API는 OAuth 2 새로 고침 코드와 기본 인증을 모두 지원합니다. 지원되는 두 가지 인증 유형에 대한 자격 증명에 대한 자세한 내용은 다음 표를 참조하십시오.

#### OAuth 2 새로 고침 코드

| 자격 증명 | 설명 |
| --- | --- |
| Host | 요청을 하는 소스의 호스트 URL입니다. 이 값은 필수이며 요청 매개 변수 무시를 사용하여 생략할 수 없습니다. |
| 인증 테스트 URL | (선택 사항) 기본 연결을 만들 때 인증 테스트 URL을 사용하여 자격 증명을 확인합니다. 지정하지 않으면 소스 연결 생성 단계 동안 자격 증명이 자동으로 선택됩니다. |
| 클라이언트 ID | (선택 사항) 사용자 계정과 연결된 클라이언트 ID입니다. |
| 클라이언트 암호 | (선택 사항) 사용자 계정과 연결된 클라이언트 암호입니다. |
| 액세스 토큰 | 응용 프로그램에 액세스하는 데 사용되는 기본 인증 자격 증명입니다. 액세스 토큰은 사용자 데이터의 특정 측면에 액세스할 수 있도록 애플리케이션의 인증을 나타냅니다. 이 값은 필수이며 요청 매개 변수 무시를 사용하여 생략할 수 없습니다. |
| 새로 고침 토큰 | (선택 사항) 액세스 토큰이 만료되었을 때 새 액세스 토큰을 생성하는 데 사용되는 토큰입니다. |
| 액세스 토큰 URL | (선택 사항) 액세스 토큰을 가져오는 데 사용되는 URL 끝점입니다. |
| 요청 매개 변수 무시 | (선택 사항) 재정의할 자격 증명 매개 변수를 지정할 수 있는 속성입니다. |


#### 기본 인증

| 자격 증명 | 설명 |
| --- | --- |
| Host | 요청을 하는 소스의 호스트 URL입니다. |
| 사용자 이름 | 사용자 계정에 해당하는 사용자 이름입니다. |
| 암호 | 사용자 계정에 해당하는 암호입니다. |

## 일반 REST API 계정 연결

플랫폼 UI에서 **[!UICONTROL 소스]** 왼쪽 탐색에서 로 이동하여 [!UICONTROL 소스] 작업 공간. 다음 [!UICONTROL 카탈로그] 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 막대를 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래에 [!UICONTROL 프로토콜] 카테고리, 선택 **[!UICONTROL 일반 REST API]** 그런 다음 **[!UICONTROL 데이터 추가]**.

![카탈로그](../../../../images/tutorials/create/generic-rest/catalog.png)

다음 **[!UICONTROL 일반 REST API에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정을 연결하려면 연결하려는 일반 REST API 계정을 선택한 다음 을 선택합니다 **[!UICONTROL 다음]** 계속 진행합니다.

![기존](../../../../images/tutorials/create/generic-rest/existing.png)

### 새 계정

새 계정을 만드는 경우 **[!UICONTROL 새 계정]**, 그런 다음 이름 및 옵션 설명을 새로 추가합니다 [!DNL Generic REST API] 계정이 필요합니다.

![새](../../../../images/tutorials/create/generic-rest/new.png)

#### OAuth 2 새로 고침 코드를 사용하여 인증

[!DNL Generic REST API] 은 OAuth 2 새로 고침 코드 및 기본 인증을 모두 지원합니다. OAuth2 인증을 사용하여 인증하려면 **[!UICONTROL OAuth2RefreshCode]**, OAuth 2 자격 증명을 제공한 다음 을(를) 선택합니다 **[!UICONTROL 소스에 연결]**.

![](../../../../images/tutorials/create/generic-rest/oauth2.png)

#### 기본 인증을 사용하여 인증

기본 인증을 사용하려면 **[!UICONTROL 기본 인증]**&#x200B;호스트, 사용자 이름 및 암호를 제공한 다음 을 선택합니다 **[!UICONTROL 소스에 연결]**.

![](../../../../images/tutorials/create/generic-rest/basic-authentication.png)

## 다음 단계

이 자습서에 따라 일반 REST API 계정에 대한 연결을 설정했습니다. 이제 다음 자습서를 계속 진행하고 [데이터를 플랫폼으로 가져오도록 데이터 흐름 구성](../../dataflow/protocols.md).
