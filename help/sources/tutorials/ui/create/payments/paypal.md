---
keywords: Experience Platform;홈;인기 항목;paypal;Paypal
solution: Experience Platform
title: UI에서 PayPal 소스 연결 만들기
type: Tutorial
description: Adobe Experience Platform UI를 사용하여 PayPal 소스 연결을 만드는 방법을 알아봅니다.
exl-id: bbd3f634-cb28-45d8-9b7b-ed3873101882
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 1%

---

# 만들기 [!DNL PayPal] UI의 소스 연결

Adobe Experience Platform의 소스 커넥터는 일정에 따라 외부 소스 데이터를 수집하는 기능을 제공합니다. 이 자습서에서는 다음을 만드는 단계를 제공합니다 [!DNL PayPal] platform 사용자 인터페이스를 사용하는 소스 커넥터

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): 표준화된 프레임워크 [!DNL Experience Platform] 고객 경험 데이터를 구성합니다.
   * [스키마 컴포지션 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 정의 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 소스의 집계 데이터를 기반으로 통합 실시간 소비자 프로필을 제공합니다.

이미 유효한 을(를) 가지고 있는 경우 [!DNL PayPal] 연결을 통해 이 문서의 나머지 부분을 건너뛰고 다음 튜토리얼을 진행할 수 있습니다. [데이터 흐름 구성](../../dataflow/payments.md)

### 필요한 자격 증명 수집

에 액세스하려면 [!DNL PayPal] 계정 플랫폼에서는 다음 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `host` | 의 URL [!DNL PayPal] 인스턴스. |
| `clientID` | 와 연결된 클라이언트 ID [!DNL PayPal] 응용 프로그램. |
| `clientSecret` | 와(과) 연결된 클라이언트 암호 [!DNL PayPal] 응용 프로그램. |

시작에 대한 자세한 내용은 다음을 참조하십시오. [[!DNL PayPal] 문서](https://developer.paypal.com/docs/api/overview/#get-credentials)

## 연결 [!DNL PayPal] account

필요한 자격 증명을 수집했으면 아래 단계에 따라 를 연결할 수 있습니다. [!DNL PayPal] 계정을 플랫폼에 추가합니다.

에 로그인 [Adobe Experience Platform](https://platform.adobe.com) 다음을 선택합니다. **[!UICONTROL 소스]** 왼쪽 탐색 모음에서 다음 위치에 액세스: **[!UICONTROL 소스]** 작업 영역. 다음 **[!UICONTROL 카탈로그]** 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래 **[!UICONTROL 결제]** 범주, 선택 **[!UICONTROL PayPal]**. 이 커넥터를 처음 사용하는 경우 다음을 선택합니다. **[!UICONTROL 구성]**. 그렇지 않으면 를 선택합니다. **[!UICONTROL 데이터 추가]** 새로 만들려면 [!DNL PayPal] 커넥터.

![카탈로그](../../../../images/tutorials/create/paypal/catalog.png)

다음 **[!UICONTROL Paypal에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 새 계정

새 자격 증명을 사용하는 경우 다음을 선택합니다 **[!UICONTROL 새 계정]**. 표시되는 입력 양식에서 이름, 설명(선택 사항) 및 [!DNL PayPal] 자격 증명. 완료되면 다음을 선택합니다. **[!UICONTROL 연결]** 그런 다음 새 연결을 설정하는 데 시간이 걸릴 수 있습니다.

![연결](../../../../images/tutorials/create/paypal/connect.png)

### 기존 계정

기존 계정을 연결하려면 [!DNL PayPal] 연결할 계정을 선택한 다음 **[!UICONTROL 다음]** 계속합니다.

![기존](../../../../images/tutorials/create/paypal/existing.png)

## 다음 단계

이 자습서를 따라 [!DNL PayPal] 계정입니다. 이제 다음 튜토리얼을 계속 진행하여 [데이터 흐름을 구성하여 결제 데이터를 Platform으로 가져오기](../../dataflow/payments.md).
