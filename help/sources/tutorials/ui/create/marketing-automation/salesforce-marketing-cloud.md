---
keywords: Experience Platform;홈;인기 항목;salesforce marketing cloud;Salesforce Marketing Cloud
solution: Experience Platform
title: UI에서 Salesforce Marketing Cloud 소스 연결 만들기
topic-legacy: overview
type: Tutorial
description: Adobe Experience Platform UI를 사용하여 Salesforce Marketing Cloud 소스 연결을 만드는 방법을 알아봅니다.
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---

# 만들기 [!DNL Salesforce Marketing Cloud] UI의 소스 연결

>[!NOTE]
>
> 다음 [!DNL Salesforce Marketing Cloud] 소스가 베타 버전입니다. 자세한 내용은 [소스 개요](../../../../home.md#terms-and-conditions) 베타 레이블이 지정된 소스 사용에 대한 자세한 정보.

Adobe Experience Platform의 소스 커넥터는 예약된 방식으로 외부 소스 데이터를 수집할 수 있습니다. 이 자습서에서는 을(를) 만드는 단계를 제공합니다 [!DNL Salesforce Marketing Cloud] 플랫폼 사용자 인터페이스를 사용하는 소스 커넥터.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): 표준화된 프레임워크 [!DNL Experience Platform] 고객 경험 데이터를 구성합니다.
   * [스키마 작성 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 빌딩 블록에 대해 알아봅니다.
   * [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아보십시오.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 [!DNL Salesforce Marketing Cloud] 연결을 통해 이 문서의 나머지 부분을 건너뛰고 다음 자습서를 진행할 수 있습니다. [데이터 흐름 구성](../../dataflow/marketing-automation.md).

### 필요한 자격 증명 수집

에 액세스하려면 [!DNL Salesforce Marketing Cloud] 플랫폼의 계정은 다음 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `host` | 애플리케이션의 호스트 서버입니다. 종종 하위 도메인입니다. **참고:** 을 입력할 때 `host` 값은 전체 URL이 아니라 하위 도메인만 지정해야 합니다. 예를 들어 호스트 URL이 `https://abcd-ab12c3d4e5fg6hijk7lmnop8qrst.auth.marketingcloudapis.com/`를 입력한 다음 을(를) 입력하기만 하면 됩니다 `abcd-ab12c3d4e5fg6hijk7lmnop8qrst` 를 호스트 값으로 사용할 수 있습니다. |
| `clientId` | 와 연결된 클라이언트 ID [!DNL Salesforce Marketing Cloud] 응용 프로그램. |
| `clientSecret` | 와 연결된 클라이언트 암호입니다. [!DNL Salesforce Marketing Cloud] 응용 프로그램. |

시작하는 방법에 대한 자세한 내용은 다음을 참조하십시오 [[!DNL Salesforce Marketing Cloud] 문서](https://developer.salesforce.com/docs/atlas.en-us.mc-apis.meta/mc-apis/authentication.htm).

## 연결 [!DNL Salesforce Marketing Cloud] account

필요한 자격 증명을 수집하면 아래 단계에 따라 를 연결할 수 있습니다 [!DNL Salesforce Marketing Cloud] Platform에 계정을 설정합니다.

플랫폼 UI에서 **[!UICONTROL 소스]** 왼쪽 탐색에서 로 이동하여 [!UICONTROL 소스] 작업 공간. 다음 [!UICONTROL 카탈로그] 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 검색 창을 사용하여 표시된 커넥터 범위를 좁힐 수도 있습니다.

아래에 [!UICONTROL 마케팅 자동화] 카테고리, 선택 **[!UICONTROL Salesforce Marketing Cloud]** 그런 다음 **[!UICONTROL 설정]**.

![카탈로그](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

다음 **[!UICONTROL Salesforce Marketing Cloud에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 새 계정

새 자격 증명을 사용하는 경우 **[!UICONTROL 새 계정]**. 표시되는 입력 양식에서 이름, 선택적 설명 및 [!DNL Salesforce Marketing Cloud] 자격 증명. 완료되면 을 선택합니다 **[!UICONTROL Connect]** 그런 다음 새 연결이 설정될 시간을 허용합니다.

![새](../../../../images/tutorials/create/salesforce-marketing-cloud/new.png)

### 기존 계정

기존 계정을 연결하려면 [!DNL Salesforce Marketing Cloud] 연결할 계정을 선택한 다음 **[!UICONTROL 다음]** 계속 진행합니다.

![기존](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## 다음 단계

이 자습서에 따라 [!DNL Salesforce Marketing Cloud] 계정이 필요합니다. 이제 다음 자습서를 계속 진행하고 [마케팅 자동화 시스템 데이터를 플랫폼으로 가져오기 위해 데이터 흐름 구성](../../dataflow/marketing-automation.md).
