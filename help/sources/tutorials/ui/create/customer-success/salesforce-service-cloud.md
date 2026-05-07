---
title: Experience Platform 사용자 인터페이스를 사용하여 Salesforce 서비스 클라우드 계정 연결
description: 사용자 인터페이스를 사용하여 Salesforce Service Cloud 계정을 연결하고 고객 성공 데이터를 Experience Platform으로 가져오는 방법을 알아봅니다.
exl-id: 38480a29-7852-46c6-bcea-5dc6bffdbd15
source-git-commit: b9a9b00114b3c1159a14b7e39484d250fa7563ba
workflow-type: tm+mt
source-wordcount: '423'
ht-degree: 2%

---

# UI를 사용하여 [!DNL Salesforce Service Cloud] 계정을 Experience Platform에 연결

이 단계별 안내서에 따라 [!DNL Salesforce Service Cloud] 계정을 원활하게 연결하고 고객 성공 데이터를 Adobe Experience Platform으로 가져옵니다.

## 시작

이 자습서에서는 Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): Experience Platform에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 올바른 [!DNL Salesforce Service Cloud] 연결이 있는 경우 이 문서의 나머지 부분을 건너뛰고 [고객 성공을 위한 데이터 흐름 구성](../../dataflow/customer-success.md)에 대한 자습서로 진행할 수 있습니다.

### 필요한 자격 증명 수집

자격 증명 검색에 대한 자세한 내용은 [인증 가이드](../../../../connectors/customer-success/salesforce-service-cloud.md#credentials)를 참조하십시오.

## [!DNL Salesforce Service Cloud] 계정 연결

Experience Platform UI의 왼쪽 탐색에서 **[!UICONTROL Sources]**&#x200B;을(를) 선택하여 [!UICONTROL Sources] 작업 영역에 액세스합니다. 화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

*[!UICONTROL Customer success]* 범주에서 **[!DNL Salesforce Service Cloud]**&#x200B;을(를) 선택한 다음 **[!UICONTROL Add data]**&#x200B;을(를) 선택합니다.

>[!TIP]
>
>지정된 소스에 아직 인증된 계정이 없는 경우 소스 카탈로그의 소스에 **[!UICONTROL Set up]** 옵션이 표시됩니다. 인증된 계정이 있으면 이 옵션이 **[!UICONTROL Add data]**(으)로 변경됩니다.

![Salesforce Service Cloud 소스 카드가 선택된 Experience Platform UI의 소스 카탈로그입니다.](../../../../images/tutorials/create/salesforce-service-cloud/catalog.png)

**[!UICONTROL Connect to Salesforce Service Cloud]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정 사용

기존 계정을 사용하려면 **[!UICONTROL Existing account]**&#x200B;을(를) 선택한 다음 표시되는 목록에서 원하는 계정을 선택하십시오. 완료되면 계속하려면 **[!UICONTROL Next]**&#x200B;을(를) 선택하십시오.

![이미 조직에 있는 인증된 Salesforce Service Cloud 계정 목록입니다.](../../../../images/tutorials/create/salesforce-service-cloud/existing.png)

### 새 계정 만들기

새 계정을 만들려면 **[!UICONTROL New account]**&#x200B;을(를) 선택하고 새 [!DNL Salesforce Service Cloud] 계정의 이름과 설명을 입력하십시오. **[!UICONTROL OAuth2 Client Credential]**&#x200B;을(를) 선택한 후 다음 자격 증명의 값을 제공합니다.

* 환경 URL
* 클라이언트 ID
* 클라이언트 암호
* API 버전

완료되면 **[!UICONTROL Connect to source]**&#x200B;을(를) 선택합니다.

![Salesforce 계정 생성을 위한 OAuth 인터페이스입니다.](../../../../images/tutorials/create/salesforce-service-cloud/new.png)

## 다음 단계

이 자습서에 따라 [!DNL Salesforce Service Cloud] 계정에 대한 연결을 설정했습니다. 이제 다음 자습서를 계속 진행하고 [고객 성공 데이터를 Experience Platform으로 가져오도록 데이터 흐름을 구성](../../dataflow/customer-success.md)할 수 있습니다.
