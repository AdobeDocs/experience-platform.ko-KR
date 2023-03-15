---
keywords: Experience Platform;홈;인기 항목;소스;커넥터;소스 커넥터;소스 sdk;sdk;SDK
solution: Experience Platform
title: Platform UI를 사용하여 MailChimp 멤버 소스 연결 만들기
description: Platform UI를 사용하여 Adobe Experience Platform을 MailChimp 구성원에 연결하는 방법을 알아봅니다.
exl-id: dc620ef9-624d-4fc9-8475-bb475ea86eb7
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '682'
ht-degree: 1%

---

# 만들기 [!DNL Mailchimp Members] 플랫폼 UI를 사용한 소스 연결

이 자습서에서는 다음을 만드는 단계를 제공합니다 [!DNL Mailchimp] 수집할 소스 커넥터 [!DNL Mailchimp Members] 사용자 인터페이스를 사용하여 Adobe Experience Platform에 데이터를 전송합니다.

## 시작하기

이 안내서를 사용하려면 Adobe Experience Platform의 다음 구성 요소에 대해 이해하고 있어야 합니다.

* [소스](../../../../home.md): 플랫폼을 사용하면 다양한 소스에서 데이터를 수집할 수 있으며 을 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다 [!DNL Platform] 서비스.
* [샌드박스](../../../../../sandboxes/home.md): Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

## 필요한 자격 증명 수집

다음을 가져오려면 [!DNL Mailchimp Members] 데이터를 플랫폼으로 전송하려면 먼저 다음에 해당하는 적절한 인증 자격 증명을 제공해야 합니다. [!DNL Mailchimp] 계정입니다.

다음 [!DNL Mailchimp Members] 소스는 OAuth 2 새로 고침 코드와 기본 인증을 모두 지원합니다. 이러한 인증 유형에 대한 자세한 내용은 아래 표를 참조하십시오.

### OAuth 2 새로 고침 코드

| 자격 증명 | 설명 |
| --- | --- |
| 도메인 | MailChimp API에 연결하는 데 사용되는 루트 URL. 루트 URL 형식은 다음과 같습니다. `https://{DC}.api.mailchimp.com`, 여기서 `{DC}` 는 계정에 해당하는 데이터 센터를 나타냅니다. |
| 인증 테스트 URL | 연결 시 자격 증명의 유효성을 검사하는 데 인증 테스트 URL이 사용됩니다 [!DNL Mailchimp] 플랫폼으로 이동합니다. 제공되지 않으면 소스 연결 생성 단계에서 자격 증명을 자동으로 확인합니다. |
| 액세스 토큰 | 소스 인증에 사용되는 해당 액세스 토큰입니다. OAuth 기반 인증에 필요합니다. |

OAuth 2를 사용하여 을 인증하는 방법에 대한 자세한 내용은 [!DNL Mailchimp] 계정을 플랫폼에 추가합니다. 다음을 참조하십시오. [[!DNL Mailchimp] oauth 2 사용에 대한 문서](https://mailchimp.com/developer/marketing/guides/access-user-data-oauth-2/).

### 기본 인증

| 자격 증명 | 설명 |
| --- | --- |
| 도메인 | MailChimp API에 연결하는 데 사용되는 루트 URL. 루트 URL 형식은 다음과 같습니다. `https://{DC}.api.mailchimp.com`, 여기서 `{DC}` 는 계정에 해당하는 데이터 센터를 나타냅니다. |
| 사용자 이름 | MailChimp 계정에 해당하는 사용자 이름입니다. 기본 인증에 필요합니다. |
| 암호 | MailChimp 계정에 해당하는 암호입니다. 기본 인증에 필요합니다. |

## 연결 [!DNL Mailchimp Members] 플랫폼으로 계정

Platform UI에서 를 선택합니다. **[!UICONTROL 소스]** 왼쪽 탐색 모음에서 다음 위치에 액세스: [!UICONTROL 소스] 작업 영역. 다음 [!UICONTROL 카탈로그] 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래 [!UICONTROL 마케팅 자동화] 범주, 선택 **[!UICONTROL Mailchimp 캠페인]**&#x200B;을 선택한 다음 을 선택합니다 **[!UICONTROL 데이터 추가]**.

![카탈로그](../../../../images/tutorials/create/mailchimp-members/catalog.png)

다음 **[!UICONTROL Mailchimp 캠페인 계정 연결]** 페이지가 나타납니다. 이 페이지에서 기존 계정에 액세스할지 또는 새 계정을 만들지 여부를 선택할 수 있습니다.

### 기존 계정

기존 계정을 사용하려면 [!DNL Mailchimp Members] 새 데이터 흐름을 만들 계정 을 선택합니다. **[!UICONTROL 다음]** 계속합니다.

![기존](../../../../images/tutorials/create/mailchimp-members/existing.png)

### 새 계정

새 계정을 만드는 경우 다음을 선택합니다 **[!UICONTROL 새 계정]**&#x200B;을 클릭하고 의 이름과 설명을 입력합니다. [!DNL Mailchimp Members] 소스 연결 세부 정보.

![신규](../../../../images/tutorials/create/mailchimp-members/new.png)


#### OAuth 2를 사용하여 인증

OAuth 2를 사용하려면 다음을 선택합니다. [!UICONTROL OAuth 2 새로 고침 코드], 도메인, 인증 테스트 URL 및 액세스 토큰에 대한 값을 입력한 다음 을 선택합니다 **[!UICONTROL 소스에 연결]**. 자격 증명의 유효성을 검사하기 위해 잠시 기다린 후 을(를) 선택합니다. **[!UICONTROL 다음]** 계속합니다.

![사용합니다](../../../../images/tutorials/create/mailchimp-members/oauth.png)

#### 기본 인증을 사용하여 인증

기본 인증을 사용하려면 다음을 선택합니다 [!UICONTROL 기본 인증], 도메인, 사용자 이름 및 암호 값을 입력한 다음 을 선택합니다 **[!UICONTROL 소스에 연결]**. 자격 증명의 유효성을 검사하기 위해 잠시 기다린 후 을(를) 선택합니다. **[!UICONTROL 다음]** 계속합니다.

![기본](../../../../images/tutorials/create/mailchimp-members/basic.png)

### 선택 [!DNL Mailchimp Members] 데이터

소스가 인증되면 다음을 제공해야 합니다. `listId` 에 해당하는 [!DNL Mailchimp Members] 계정입니다.

다음에서 [!UICONTROL 데이터 선택] 페이지, 입력 `listId` 다음을 선택합니다. **[!UICONTROL 탐색]**.

![탐색](../../../../images/tutorials/create/mailchimp-members/explore.png)

페이지가 데이터의 계층 구조를 탐색하고 검사할 수 있는 대화형 스키마 트리로 업데이트됩니다. 선택 **[!UICONTROL 다음]** 계속합니다.

![select-data](../../../../images/tutorials/create/mailchimp-members/select-data.png)

## 다음 단계

(으)로 [!DNL Mailchimp] 계정 인증됨 및 [!DNL Mailchimp Members] 데이터를 선택했습니다. 이제 데이터 흐름을 만들어 데이터를 플랫폼으로 가져올 수 있습니다. 데이터 흐름을 만드는 방법에 대한 자세한 단계는 의 설명서를 참조하십시오. [마케팅 자동화 데이터를 Platform으로 가져오기 위한 데이터 흐름 만들기](../../dataflow/marketing-automation.md).
