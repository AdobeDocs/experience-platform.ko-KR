---
title: Salesforce Marketing Cloud 계정을 UI를 통해 Experience Platform에 연결
description: UI를 통해 Salesforce Marketing Cloud 계정을 Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: 635ab266fac9d3dc232307d7cb49f83904197782
workflow-type: tm+mt
source-wordcount: '500'
ht-degree: 1%

---

# 연결 [!DNL Salesforce Marketing Cloud] UI를 통해 Experience Platform 할 계정

>[!IMPORTANT]
>
>사용자 지정 개체 수집은 현재 [!DNL Salesforce Marketing Cloud] 소스 통합.

이 튜토리얼에서는 을(를) 연결하는 방법에 대한 단계를 제공합니다. [!DNL Salesforce Marketing Cloud] UI를 통해 Adobe Experience Platform에 연결합니다.

## 시작하기

이 자습서에서는 다음 Experience Platform 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): 표준화된 프레임워크 [!DNL Experience Platform] 고객 경험 데이터를 구성합니다.
   * [스키마 컴포지션 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 정의 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 소스의 집계 데이터를 기반으로 통합 실시간 소비자 프로필을 제공합니다.

이미 다음 항목이 있는 경우: [!DNL Salesforce Marketing Cloud] 계정, 이 문서의 나머지 부분을 건너뛰고 다음에 대한 자습서로 진행할 수 있습니다. [ui를 사용하여 마케팅 자동화 데이터를 Experience Platform으로 가져오기](../../dataflow/marketing-automation.md).

### 필요한 자격 증명 수집

에 액세스하려면 [!DNL Salesforce Marketing Cloud] 플랫폼의 계정에서 다음 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| Host | 응용 프로그램의 호스트 서버입니다. 이는 종종 하위 도메인입니다. **참고:** 을(를) 입력할 때 `host` 값, 다음을 지정해야 합니다. `{subdomain}.rest.marketingcloudapis.com`. 예를 들어 호스트 URL이 `https://acme-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`를 선택한 다음 입력하기만 하면 됩니다. `acme-ab12c3d4e5fg6hijk7lmnop8qrstauth.marketingcloudapis.com/` 을 호스트 값으로 사용하십시오. |
| 클라이언트 ID | 와 연결된 클라이언트 ID [!DNL Salesforce Marketing Cloud] 응용 프로그램. |
| 클라이언트 암호 | 와(과) 연결된 클라이언트 암호 [!DNL Salesforce Marketing Cloud] 응용 프로그램. |

인증에 대한 자세한 내용 [!DNL Salesforce Marketing Cloud], 다음 방문: [[!DNL Salesforce] 인증 설명서](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## 연결 [!DNL Salesforce Marketing Cloud] account

Platform UI에서 를 선택합니다. **[!UICONTROL 소스]** 을(를) 왼쪽 탐색에서 [!UICONTROL 소스] 작업 영역. 다음 [!UICONTROL 카탈로그] Experience Platform에서 지원하는 다양한 소스를 표시합니다.

범주 목록에서 적절한 범주를 선택할 수 있습니다. 검색 창을 사용하여 특정 소스를 필터링할 수도 있습니다.

아래 [!UICONTROL 마케팅 자동화] 범주, 선택 **[!UICONTROL Salesforce Marketing Cloud]** 다음을 선택합니다. **[!UICONTROL 설정]**.

![Salesforce Marketing Cloud 소스가 선택된 소스 카탈로그.](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

다음 **[!UICONTROL Salesforce Marketing Cloud에 연결]** 페이지가 나타납니다. 이 페이지에서 새 계정을 만들거나 기존 계정을 사용할 수 있습니다.

### 새 계정

새 계정을 만들려면 다음을 선택합니다. **[!UICONTROL 새 계정]** 계정의 이름, 설명(선택 사항) 및 [!DNL Salesforce Marketing Cloud] 계정입니다.

완료되면 다음을 선택합니다. **[!UICONTROL 소스에 연결]** 그런 다음 새 연결을 설정하는 데 시간이 걸릴 수 있습니다.

![Salesforce Marketing Cloud에 대한 새 계정을 인증할 수 있는 새 계정 인터페이스입니다.](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### 기존 계정

기존 계정이 이미 있는 경우 다음을 선택합니다. **[!UICONTROL 기존 계정]** 그런 다음 표시되는 목록에서 사용할 계정을 선택합니다.

![기존 Salesforce Marketing Cloud 계정 목록에서 선택할 수 있는 기존 계정 인터페이스입니다.](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## 다음 단계

이 자습서를 따라 [!DNL Salesforce Marketing Cloud] 계정과 Experience Platform. 이제 다음 튜토리얼을 계속 진행하여 [마케팅 자동화 데이터를 Experience Platform 상태로 가져오는 데이터 흐름 만들기](../../dataflow/marketing-automation.md).
