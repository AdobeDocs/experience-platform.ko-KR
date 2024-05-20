---
title: Experience Platform 사용자 인터페이스를 사용하여 Salesforce 계정을 연결합니다.
description: 사용자 인터페이스를 사용하여 Salesforce 계정을 연결하고 CRM 데이터를 Experience Platform 상태로 만드는 방법을 알아봅니다.
exl-id: b67fa4c4-d8ff-4d2d-aa76-5d9d32aa22d6
source-git-commit: 8d62cf4ca0071e84baa9399e0a25f7ebfb096c1a
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 1%

---

# 연결 [!DNL Salesforce] UI를 사용하여 Experience Platform 할 계정

이 튜토리얼에서는 을(를) 연결하는 방법에 대한 단계를 제공합니다. [!DNL Salesforce] Experience Platform 사용자 인터페이스를 사용하여 CRM 데이터를 Adobe Experience Platform으로 가져오고 계정을 만듭니다.

## 시작하기

이 자습서에서는 다음 Experience Platform 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 정의 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 소스의 집계 데이터를 기반으로 통합 실시간 소비자 프로필을 제공합니다.

이미 인증된 사용자가 있는 경우 [!DNL Salesforce] 계정, 이 문서의 나머지 부분을 건너뛰고 다음에 대한 자습서로 진행할 수 있습니다. [crm 데이터에 대한 데이터 흐름 구성](../../dataflow/crm.md).

### 필요한 자격 증명 수집 {#gather-required-credentials}

다음 [!DNL Salesforce] 소스는 기본 인증 및 OAuth2 클라이언트 자격 증명을 지원합니다.

>[!BEGINTABS]

>[!TAB 기본 인증]

연결하려면 다음 자격 증명에 대한 값을 제공해야 합니다. [!DNL Salesforce] 기본 인증을 사용하는 계정입니다.

| 자격 증명 | 설명 |
| --- | --- |
| 환경 URL | 의 URL [!DNL Salesforce] 소스 인스턴스. |
| 사용자 이름 | 의 사용자 이름 [!DNL Salesforce] 사용자 계정입니다. |
| 암호 | 에 대한 암호 [!DNL Salesforce] 사용자 계정입니다. |
| 보안 토큰 | 에 대한 보안 토큰 [!DNL Salesforce] 사용자 계정입니다. |
| API 버전 | (선택 사항) 의 REST API 버전 [!DNL Salesforce] 사용 중인 인스턴스. API 버전의 값은 십진수로 형식을 지정해야 합니다. 예를 들어 API 버전을 사용하는 경우 `52`을 누르고 값을 다음으로 입력해야 합니다. `52.0`. 이 필드를 비워 두면 Experience Platform은 자동으로 사용 가능한 최신 버전을 사용합니다. |

인증에 대한 자세한 내용은 [이 [!DNL Salesforce] 인증 안내서](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart_oauth.htm).

>[!TAB OAuth2 클라이언트 자격 증명]

연결하려면 다음 자격 증명에 대한 값을 제공해야 합니다. [!DNL Salesforce] oauth2 클라이언트 자격 증명을 사용하는 계정입니다.

| 자격 증명 | 설명 |
| --- | --- |
| 환경 URL | 의 URL [!DNL Salesforce] 소스 인스턴스. |
| 클라이언트 ID | 클라이언트 ID는 OAuth2 인증의 일부로 클라이언트 암호와 함께 사용됩니다. 클라이언트 ID와 클라이언트 암호를 사용하면 애플리케이션을 식별하여 계정을 대신하여 애플리케이션이 작동할 수 있습니다. [!DNL Salesforce]. |
| 클라이언트 암호 | 클라이언트 암호는 OAuth2 인증의 일부로 클라이언트 ID와 함께 사용됩니다. 클라이언트 ID와 클라이언트 암호를 사용하면 애플리케이션을 식별하여 계정을 대신하여 애플리케이션이 작동할 수 있습니다. [!DNL Salesforce]. |
| API 버전 | 의 REST API 버전 [!DNL Salesforce] 사용 중인 인스턴스. API 버전의 값은 십진수로 형식을 지정해야 합니다. 예를 들어 API 버전을 사용하는 경우 `52`을 누르고 값을 다음으로 입력해야 합니다. `52.0`. 이 필드를 비워 두면 Experience Platform은 자동으로 사용 가능한 최신 버전을 사용합니다. |

에 OAuth 사용에 대한 자세한 정보 [!DNL Salesforce], 다음을 읽습니다 [[!DNL Salesforce] OAuth 인증 흐름에 대한 안내서](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&amp;type=5).

>[!ENDTABS]

필요한 자격 증명을 수집했으면 아래 단계에 따라 연결할 수 있습니다. [!DNL Salesforce] Experience Platform 계정.

## 연결 [!DNL Salesforce] account

Platform UI에서 를 선택합니다. **[!UICONTROL 소스]** 을(를) 왼쪽 탐색에서 [!UICONTROL 소스] 작업 영역. 화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래 *CRM* 범주, 선택 **[!DNL Salesforce]**&#x200B;을 선택한 다음 을 선택합니다 **[!UICONTROL 데이터 추가]**.

>[!TIP]
>
>소스 카탈로그의 소스는 **[!UICONTROL 설정]** 지정된 소스에 인증된 계정이 아직 없는 경우 옵션입니다. 인증된 계정이 존재하면 이 옵션은 다음으로 변경됩니다. **[!UICONTROL 데이터 추가]**.

![Salesforce 소스 카드가 선택된 Experience Platform UI의 소스 카탈로그입니다.](../../../../images/tutorials/create/salesforce/catalog.png)

다음 **[!UICONTROL Salesforce에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정 사용

기존 계정을 사용하려면 **[!UICONTROL 기존 계정]** 그런 다음 나타나는 목록에서 사용할 계정을 선택합니다. 완료되면 다음을 선택합니다. **[!UICONTROL 다음]** 계속합니다.

![조직에 이미 존재하는 인증된 Salesforce 계정 목록입니다.](../../../../images/tutorials/create/salesforce/existing.png)

### 새 계정 만들기

새 계정을 만들려면 다음을 선택합니다. **[!UICONTROL 새 계정]** 및 의 새 이름과 설명을 입력합니다. [!DNL Salesforce] 계정입니다.

![적절한 인증 자격 증명을 제공하여 새 Salesforce 계정을 만들 수 있는 인터페이스입니다.](../../../../images/tutorials/create/salesforce/new.png)

그런 다음 새 계정에 사용할 인증 유형을 선택합니다.

>[!BEGINTABS]

>[!TAB 기본 인증]

기본 인증의 경우 **[!UICONTROL 기본 인증]** 그런 다음 다음 다음 자격 증명의 값을 제공합니다.

* 환경 URL
* 사용자 이름
* 암호
* API 버전(선택 사항)

완료되면 다음을 선택합니다. **[!UICONTROL 소스에 연결]**.

![Salesforce 계정 생성을 위한 기본 인증 인터페이스입니다.](../../../../images/tutorials/create/salesforce/basic.png)

>[!TAB OAuth2 클라이언트 자격 증명]

OAuth 2 클라이언트 자격 증명의 경우 **[!UICONTROL OAuth2 클라이언트 자격 증명]** 그런 다음 다음 다음 자격 증명의 값을 제공합니다.

* 환경 URL
* 클라이언트 ID
* 클라이언트 암호
* API 버전

완료되면 다음을 선택합니다. **[!UICONTROL 소스에 연결]**.

![Salesforce 계정 생성을 위한 OAuth 인터페이스입니다.](../../../../images/tutorials/create/salesforce/oauth2.png)

>[!ENDTABS]

## 다음 단계

이 자습서를 따라 [!DNL Salesforce] 계정입니다. 이제 다음 튜토리얼을 계속 진행하여 [데이터 흐름을 구성하여 데이터 가져오기 [!DNL Platform]](../../dataflow/crm.md).
