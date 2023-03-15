---
keywords: Experience Platform;홈;인기 항목;salesforce marketing cloud;Salesforce Marketing Cloud
solution: Experience Platform
title: UI에서 Salesforce Marketing Cloud 소스 연결 만들기
type: Tutorial
description: Adobe Experience Platform UI를 사용하여 Salesforce Marketing Cloud 소스 연결을 만드는 방법을 알아봅니다.
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---

# 만들기 [!DNL Salesforce Marketing Cloud] UI의 소스 연결

>[!NOTE]
>
> 다음 [!DNL Salesforce Marketing Cloud] 소스는 베타 버전입니다. 다음을 참조하십시오. [소스 개요](../../../../home.md#terms-and-conditions) beta 레이블 소스를 사용하는 방법에 대한 자세한 내용.

Adobe Experience Platform의 소스 커넥터는 일정에 따라 외부 소스 데이터를 수집하는 기능을 제공합니다. 이 자습서에서는 다음을 만드는 단계를 제공합니다 [!DNL Salesforce Marketing Cloud] platform 사용자 인터페이스를 사용하는 소스 커넥터

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): 표준화된 프레임워크 [!DNL Experience Platform] 고객 경험 데이터를 구성합니다.
   * [스키마 컴포지션 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 정의 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 소스의 집계 데이터를 기반으로 통합 실시간 소비자 프로필을 제공합니다.

이미 다음 항목이 있는 경우: [!DNL Salesforce Marketing Cloud] 연결을 통해 이 문서의 나머지 부분을 건너뛰고 다음 튜토리얼을 진행할 수 있습니다. [데이터 흐름 구성](../../dataflow/marketing-automation.md).

### 필요한 자격 증명 수집

에 액세스하려면 [!DNL Salesforce Marketing Cloud] 플랫폼의 계정에서 다음 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `host` | 응용 프로그램의 호스트 서버입니다. 이는 종종 하위 도메인입니다. **참고:** 을(를) 입력할 때 `host` 값을 지정하면 전체 URL이 아닌 하위 도메인만 지정해야 합니다. 예를 들어 호스트 URL이 `https://abcd-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`를 선택한 다음 입력하기만 하면 됩니다. `abcd-ab12c3d4e5fg6hijk7lmnop8qrst` 을 호스트 값으로 사용하십시오. |
| `clientId` | 와 연결된 클라이언트 ID [!DNL Salesforce Marketing Cloud] 응용 프로그램. |
| `clientSecret` | 와(과) 연결된 클라이언트 암호 [!DNL Salesforce Marketing Cloud] 응용 프로그램. |

시작에 대한 자세한 내용은 다음을 참조하십시오. [[!DNL Salesforce Marketing Cloud] 문서](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## 연결 [!DNL Salesforce Marketing Cloud] account

필요한 자격 증명을 수집했으면 아래 단계에 따라 를 연결할 수 있습니다. [!DNL Salesforce Marketing Cloud] 계정을 플랫폼에 추가합니다.

Platform UI에서 를 선택합니다. **[!UICONTROL 소스]** 을(를) 왼쪽 탐색에서 [!UICONTROL 소스] 작업 영역. 다음 [!UICONTROL 카탈로그] 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 검색 창을 사용하여 표시된 커넥터 범위를 좁힐 수도 있습니다.

아래 [!UICONTROL 마케팅 자동화] 범주, 선택 **[!UICONTROL Salesforce Marketing Cloud]** 다음을 선택합니다. **[!UICONTROL 설정]**.

![카탈로그](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

다음 **[!UICONTROL Salesforce Marketing Cloud에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 새 계정

새 자격 증명을 사용하는 경우 다음을 선택합니다 **[!UICONTROL 새 계정]**. 표시되는 입력 양식에서 이름, 설명(선택 사항) 및 [!DNL Salesforce Marketing Cloud] 자격 증명. 완료되면 다음을 선택합니다. **[!UICONTROL 연결]** 그런 다음 새 연결을 설정하는 데 시간이 걸릴 수 있습니다.

![신규](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### 기존 계정

기존 계정을 연결하려면 [!DNL Salesforce Marketing Cloud] 연결할 계정을 선택한 다음 **[!UICONTROL 다음]** 계속합니다.

![기존](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## 다음 단계

이 자습서를 따라 [!DNL Salesforce Marketing Cloud] 계정입니다. 이제 다음 튜토리얼을 계속 진행하여 [마케팅 자동화 시스템 데이터를 플랫폼으로 가져오기 위한 데이터 흐름 구성](../../dataflow/marketing-automation.md).
