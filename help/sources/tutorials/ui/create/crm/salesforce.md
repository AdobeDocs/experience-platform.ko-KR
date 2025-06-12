---
title: Experience Platform 사용자 인터페이스를 사용하여 Salesforce 계정 연결
description: 사용자 인터페이스를 사용하여 Salesforce 계정을 연결하고 CRM 데이터를 Experience Platform으로 가져오는 방법을 알아봅니다.
exl-id: b67fa4c4-d8ff-4d2d-aa76-5d9d32aa22d6
source-git-commit: eab6303a3b420d4622185316922d242a4ce8a12d
workflow-type: tm+mt
source-wordcount: '972'
ht-degree: 2%

---

# UI를 사용하여 [!DNL Salesforce] 계정을 Experience Platform에 연결

이 자습서에서는 Experience Platform 사용자 인터페이스를 사용하여 [!DNL Salesforce] 계정을 연결하고 CRM 데이터를 Adobe Experience Platform으로 가져오는 방법에 대한 단계를 제공합니다.

## 시작

이 자습서에서는 Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): Experience Platform에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

인증된 [!DNL Salesforce] 계정이 이미 있는 경우 이 문서의 나머지 부분을 건너뛰고 [CRM 데이터에 대한 데이터 흐름 구성](../../dataflow/crm.md)에 대한 자습서로 진행할 수 있습니다.

### 필요한 자격 증명 수집 {#gather-required-credentials}

>[!WARNING]
>
>[!DNL Salesforce] 원본에 대한 기본 인증은 2026년 1월에 더 이상 사용되지 않습니다. 소스를 계속 사용하고 [!DNL Salesforce] 계정의 데이터를 Experience Platform으로 수집하려면 OAuth 2 클라이언트 자격 증명 인증으로 이동해야 합니다.

[!DNL Salesforce] 원본은 기본 인증과 OAuth2 클라이언트 자격 증명을 지원합니다.

>[!BEGINTABS]

>[!TAB 기본 인증]

기본 인증을 사용하여 [!DNL Salesforce] 계정에 연결하려면 다음 자격 증명에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| --- | --- |
| 환경 URL | [!DNL Salesforce] 원본 인스턴스의 URL입니다. 환경 URL의 형식은 `https://[domain].my.salesforce.com`입니다. |
| 사용자 이름 | [!DNL Salesforce] 사용자 계정의 사용자 이름입니다. |
| 암호 | [!DNL Salesforce] 사용자 계정의 암호입니다. |
| 보안 토큰 | [!DNL Salesforce] 사용자 계정의 보안 토큰입니다. |
| API 버전 | (선택 사항) 사용 중인 [!DNL Salesforce] 인스턴스의 REST API 버전입니다. API 버전의 값은 십진수로 형식을 지정해야 합니다. 예를 들어 API 버전 `52`을(를) 사용하는 경우 값을 `52.0`(으)로 입력해야 합니다. 이 필드를 비워 두면 Experience Platform은 자동으로 사용 가능한 최신 버전을 사용합니다. |

인증에 대한 자세한 내용은 [이 [!DNL Salesforce] 인증 가이드](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/quickstart_oauth.htm)를 참조하세요.

>[!TAB OAuth2 클라이언트 자격 증명]

OAuth2 클라이언트 자격 증명을 사용하여 [!DNL Salesforce] 계정에 연결하려면 다음 자격 증명에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| --- | --- |
| 환경 URL | [!DNL Salesforce] 원본 인스턴스의 URL입니다. 환경 URL의 형식은 `https://[domain].my.salesforce.com`입니다. |
| 클라이언트 ID | 클라이언트 ID는 OAuth2 인증의 일부로 클라이언트 암호와 함께 사용됩니다. 클라이언트 ID와 클라이언트 암호를 사용하면 응용 프로그램을 [!DNL Salesforce]에 식별하여 응용 프로그램이 계정을 대신하여 작동할 수 있습니다. |
| 클라이언트 암호 | 클라이언트 암호는 OAuth2 인증의 일부로 클라이언트 ID와 함께 사용됩니다. 클라이언트 ID와 클라이언트 암호를 사용하면 응용 프로그램을 [!DNL Salesforce]에 식별하여 응용 프로그램이 계정을 대신하여 작동할 수 있습니다. |
| API 버전 | 사용 중인 [!DNL Salesforce] 인스턴스의 REST API 버전입니다. API 버전의 값은 십진수로 형식을 지정해야 합니다. 예를 들어 API 버전 `52`을(를) 사용하는 경우 값을 `52.0`(으)로 입력해야 합니다. 이 필드를 비워 두면 Experience Platform은 자동으로 사용 가능한 최신 버전을 사용합니다. |

[!DNL Salesforce]에 대한 OAuth 사용에 대한 자세한 내용은 OAuth 인증 흐름에 대한 [[!DNL Salesforce] 안내서](https://help.salesforce.com/s/articleView?id=sf.remoteaccess_oauth_flows.htm&type=5)를 참조하십시오.

>[!ENDTABS]

필요한 자격 증명을 수집했으면 아래 단계에 따라 [!DNL Salesforce] 계정을 Experience Platform에 연결할 수 있습니다.

## [!DNL Salesforce] 계정 연결

Experience Platform UI의 왼쪽 탐색에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 [!UICONTROL 소스] 작업 영역에 액세스합니다. 화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

*[!UICONTROL CRM]* 범주에서 **[!DNL Salesforce]**&#x200B;을(를) 선택한 다음 **[!UICONTROL 데이터 추가]**&#x200B;를 선택합니다.

>[!TIP]
>
>지정된 소스에 아직 인증된 계정이 없는 경우 소스 카탈로그의 소스에 **[!UICONTROL 설정]** 옵션이 표시됩니다. 인증된 계정이 있으면 이 옵션이 **[!UICONTROL 데이터 추가]**(으)로 변경됩니다.

![Salesforce 소스 카드가 선택된 Experience Platform UI의 소스 카탈로그입니다.](../../../../images/tutorials/create/salesforce/catalog.png)

**[!UICONTROL Salesforce에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정 사용

기존 계정을 사용하려면 **[!UICONTROL 기존 계정]**&#x200B;을 선택한 다음 표시되는 목록에서 사용할 계정을 선택하십시오. 완료되면 **[!UICONTROL 다음]**&#x200B;을(를) 선택하여 계속하십시오.

![이미 조직에 있는 인증된 Salesforce 계정 목록입니다.](../../../../images/tutorials/create/salesforce/existing.png)

### 새 계정 만들기

새 계정을 만들려면 **[!UICONTROL 새 계정]**&#x200B;을(를) 선택하고 새 [!DNL Salesforce] 계정의 이름과 설명을 입력하십시오.

![적절한 인증 자격 증명을 제공하여 새 Salesforce 계정을 만들 수 있는 인터페이스입니다.](../../../../images/tutorials/create/salesforce/new.png)

그런 다음 새 계정에 사용할 인증 유형을 선택합니다.

>[!BEGINTABS]

>[!TAB 기본 인증]

기본 인증의 경우 **[!UICONTROL 기본 인증]**&#x200B;을 선택한 후 다음 자격 증명의 값을 제공하십시오.

* 환경 URL
* 사용자 이름
* 암호
* API 버전(선택 사항)

완료되면 **[!UICONTROL 소스에 연결]**&#x200B;을 선택합니다.

![Salesforce 계정 생성을 위한 기본 인증 인터페이스입니다.](../../../../images/tutorials/create/salesforce/basic.png)

>[!TAB OAuth2 클라이언트 자격 증명]

OAuth2 클라이언트 자격 증명의 경우 **[!UICONTROL OAuth2 클라이언트 자격 증명]**&#x200B;을(를) 선택한 다음 다음 자격 증명의 값을 제공합니다.

* 환경 URL
* 클라이언트 ID
* 클라이언트 암호
* API 버전

완료되면 **[!UICONTROL 소스에 연결]**&#x200B;을 선택합니다.

![Salesforce 계정 생성을 위한 OAuth 인터페이스입니다.](../../../../images/tutorials/create/salesforce/oauth2.png)

>[!ENDTABS]

### 샘플 데이터의 미리 보기 건너뛰기 {#skip-preview-of-sample-data}

데이터 선택 단계에서 큰 테이블 또는 데이터 파일을 수집할 때 시간 초과가 발생할 수 있습니다. 샘플 데이터가 없어도 데이터 미리 보기를 건너뛰어 시간 초과를 우회하고 스키마를 볼 수 있습니다. 데이터 미리 보기를 건너뛰려면 **[!UICONTROL 샘플 데이터 미리 보기 건너뛰기]** 전환을 사용하도록 설정하십시오.

워크플로우의 나머지 부분은 그대로 유지됩니다. 유일한 주의 사항은 데이터 미리보기를 건너뛰면 매핑 단계에서 계산된 필드 및 필수 필드의 자동 유효성 검사를 방지할 수 있으므로 매핑 중에 이러한 필드의 유효성을 수동으로 검사해야 한다는 것입니다.

## 다음 단계

이 자습서에 따라 [!DNL Salesforce] 계정에 대한 연결을 설정했습니다. 이제 다음 자습서를 계속 진행하고 [데이터를 가져올 데이터 흐름을 구성 [!DNL Experience Platform]](../../dataflow/crm.md)할 수 있습니다.
