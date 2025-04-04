---
title: UI를 통해 Salesforce Marketing Cloud 계정을 Experience Platform에 연결
description: UI를 통해 Salesforce Marketing Cloud 계정을 Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 2%

---

# UI를 통해 [!DNL Salesforce Marketing Cloud] 계정을 Experience Platform에 연결

>[!WARNING]
>
>[!DNL Salesforce Marketing Cloud] 원본은 2025년 6월 말에 사용되지 않습니다.

이 자습서에서는 UI를 통해 [!DNL Salesforce Marketing Cloud] 계정을 Adobe Experience Platform에 연결하는 방법에 대한 단계를 제공합니다.

## 시작하기

이 자습서에서는 Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): [!DNL Experience Platform]에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 [!DNL Salesforce Marketing Cloud] 계정이 있는 경우 이 문서의 나머지 부분을 건너뛰고 [UI를 사용하여 Experience Platform에 마케팅 자동화 데이터를 가져오는 중](../../dataflow/marketing-automation.md)에 대한 자습서를 진행할 수 있습니다.

### 필요한 자격 증명 수집

Experience Platform에서 [!DNL Salesforce Marketing Cloud] 계정에 액세스하려면 다음 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| Host | 응용 프로그램의 호스트 서버입니다. 이는 종종 하위 도메인입니다. **참고:** `host` 값을 입력할 때 `{subdomain}.rest.marketingcloudapis.com`을(를) 지정해야 합니다. 예를 들어 호스트 URL이 `https://acme-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`인 경우 `acme-ab12c3d4e5fg6hijk7lmnop8qrst.rest.marketingcloudapis.com/`을(를) 호스트 값으로 입력해야 합니다. |
| 클라이언트 ID | [!DNL Salesforce Marketing Cloud] 응용 프로그램과 연결된 클라이언트 ID입니다. |
| 클라이언트 암호 | [!DNL Salesforce Marketing Cloud] 응용 프로그램과 연결된 클라이언트 암호입니다. |

[!DNL Salesforce Marketing Cloud]의 인증에 대한 자세한 내용은 [[!DNL Salesforce] 인증 설명서](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm)를 참조하세요.

## [!DNL Salesforce Marketing Cloud] 계정 연결

>[!IMPORTANT]
>
>사용자 지정 개체 수집은 현재 [!DNL Salesforce Marketing Cloud] 원본 통합에서 지원되지 않습니다.

Experience Platform UI의 왼쪽 탐색에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 [!UICONTROL 소스] 작업 영역에 액세스합니다. [!UICONTROL 카탈로그]에는 Experience Platform에서 지원하는 다양한 소스가 표시됩니다.

범주 목록에서 적절한 범주를 선택할 수 있습니다. 검색 창을 사용하여 특정 소스를 필터링할 수도 있습니다.

[!UICONTROL 마케팅 자동화] 범주에서 **[!UICONTROL Salesforce Marketing Cloud]**&#x200B;을 선택한 다음 **[!UICONTROL 설정]**&#x200B;을 선택합니다.

![Salesforce Marketing Cloud 소스가 있는 소스 카탈로그를 선택했습니다.](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

**[!UICONTROL Salesforce Marketing Cloud에 연결]** 페이지가 나타납니다. 이 페이지에서 새 계정을 만들거나 기존 계정을 사용할 수 있습니다.

### 새 계정

새 계정을 만들려면 **[!UICONTROL 새 계정]**&#x200B;을(를) 선택하고 계정 이름, 선택적 설명 및 [!DNL Salesforce Marketing Cloud] 계정에 해당하는 인증 자격 증명을 제공하세요.

완료되면 **[!UICONTROL 소스에 연결]**&#x200B;을 선택한 다음 새 연결을 설정할 수 있는 시간을 허용하세요.

![Salesforce Marketing Cloud의 새 계정을 인증할 수 있는 새 계정 인터페이스입니다.](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### 기존 계정

기존 계정이 이미 있는 경우 **[!UICONTROL 기존 계정]**&#x200B;을 선택한 다음 표시되는 목록에서 사용할 계정을 선택하십시오.

![기존 Salesforce Marketing Cloud 계정 목록에서 선택할 수 있는 기존 계정 인터페이스입니다.](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## 다음 단계

이 자습서를 따라 [!DNL Salesforce Marketing Cloud] 계정과 Experience Platform 간에 연결을 설정했습니다. 이제 다음 자습서를 계속 진행하고 [데이터 흐름을 만들어 마케팅 자동화 데이터를 Experience Platform으로 가져올 수 있습니다](../../dataflow/marketing-automation.md).
