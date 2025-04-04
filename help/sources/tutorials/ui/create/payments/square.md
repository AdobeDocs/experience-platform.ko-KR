---
keywords: Experience Platform;홈;인기 항목;사각형;사각형
title: UI에서 정사각형 Source 연결 만들기
description: Adobe Experience Platform UI를 사용하여 Square 소스 연결을 만드는 방법을 알아봅니다.
exl-id: 7cdfeb36-c989-4875-bb94-e6594ddf30da
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 3%

---

# UI에서 [!DNL Square] 소스 연결 만들기

이 자습서에서는 Experience Platform 사용자 인터페이스를 사용하여 [!DNL Square] 소스 커넥터를 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): [!DNL Experience Platform]에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

### 필요한 자격 증명 수집

[!DNL Square] 계정 Experience Platform에 액세스하려면 다음 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| --- | --- |
| Host | [!DNL Square] 인스턴스의 URL. |
| 클라이언트 ID | [!DNL Square] 계정과 연결된 클라이언트 ID입니다. |
| 클라이언트 암호 | [!DNL Square] 계정과 연결된 클라이언트 암호입니다. |
| 액세스 토큰 | 액세스 토큰은 OAuth 2.0 인증을 통해 [!DNL Square] 계정을 인증하는 데 사용됩니다. [!DNL Square]에서 액세스 토큰을 가져올 수 있습니다. |
| 토큰 새로 고침 | 새로 고침 토큰은 현재 액세스 토큰이 만료되면 새 액세스 토큰을 생성하는 데 사용됩니다. [!DNL Square]에서 새로 고침 토큰을 가져올 수 있습니다. |

이러한 자격 증명과 자격 증명을 얻는 방법에 대한 자세한 내용은 [[!DNL Square] OAuth에 대한 설명서](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens)를 참조하십시오.

필요한 자격 증명을 수집했으면 아래 단계에 따라 [!DNL Square] 계정을 Experience Platform에 연결할 수 있습니다.

## [!DNL Square] 계정 연결

Experience Platform UI의 왼쪽 탐색에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 [!UICONTROL 소스] 작업 영역에 액세스합니다. [!UICONTROL 카탈로그] 화면에 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

[!UICONTROL 결제] 범주에서 **[!UICONTROL 제곱]**&#x200B;을 선택한 다음 **[!UICONTROL 데이터 추가]**&#x200B;를 선택합니다.

![카탈로그](../../../../images/tutorials/create/square/catalog.png)

**[!UICONTROL 사각형에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정을 사용하려면 새 데이터 흐름을 만들 [!DNL Square] 계정을 선택한 다음 **[!UICONTROL 다음]**&#x200B;을 선택하여 계속합니다.

![기존](../../../../images/tutorials/create/square/existing.png)

### 새 계정

새 계정을 만드는 경우 **[!UICONTROL 새 계정]**&#x200B;을(를) 선택한 다음 이름, 선택적 설명 및 [!DNL Square] 자격 증명에 대한 적절한 값을 제공합니다. 완료되면 **[!UICONTROL 소스에 연결]**&#x200B;을 선택한 다음 새 연결을 설정할 수 있는 시간을 허용하세요.

![새로 만들기](../../../../images/tutorials/create/square/new.png)

## 다음 단계

이 자습서를 따라 [!DNL Square] 계정과 Experience Platform 간의 소스 연결을 인증하고 만들었습니다. 이제 다음 자습서를 계속 진행하고 [데이터 흐름을 만들어 결제 데이터를 Experience Platform으로 가져올 수 있습니다](../../dataflow/payments.md).
