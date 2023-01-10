---
keywords: Experience Platform;홈;인기 항목;Zoho CRM;Zoho crm;Zoho;zoho
solution: Experience Platform
title: UI에서 Zoho CRM 소스 연결 만들기
type: Tutorial
description: Adobe Experience Platform UI를 사용하여 Zoho CRM 소스 연결을 만드는 방법을 알아봅니다.
exl-id: c648fc3e-beea-4030-8d36-dd8a7e2c281e
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# 만들기 [!DNL Zoho CRM] UI의 소스 연결

Adobe Experience Platform의 소스 커넥터는 예약된 대로 외부에서 가져온 CRM 데이터를 수집하는 기능을 제공합니다. 이 자습서에서는 을(를) 만드는 단계를 제공합니다 [!DNL Zoho CRM] 소스 커넥터 [!DNL Platform] 사용자 인터페이스.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): 표준화된 프레임워크 [!DNL Experience Platform] 고객 경험 데이터를 구성합니다.
   * [스키마 작성 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 빌딩 블록에 대해 알아봅니다.
   * [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아보십시오.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 유효한 [!DNL Zoho CRM] account, 이 문서의 나머지 부분을 건너뛰고 다음 자습서를 진행할 수 있습니다. [데이터 흐름 구성](../../dataflow/crm.md).

### 필요한 자격 증명 수집

연결하려면 [!DNL Zoho CRM] 플랫폼에 다음 연결 속성에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| --- | --- |
| 끝점 | 의 끝점입니다 [!DNL Zoho CRM] 요청을 수행하는 서버입니다. |
| 계정 URL | 계정 URL은 액세스 및 토큰 새로 고침에 사용됩니다. URL은 도메인별로 지정해야 합니다. |
| 클라이언트 ID | 와 일치하는 클라이언트 ID입니다 [!DNL Zoho CRM] 사용자 계정. |
| 클라이언트 암호 | 사용자의 [!DNL Zoho CRM] 사용자 계정. |
| 액세스 토큰 | 액세스 토큰은 사용자의 보안 및 임시 액세스를 허용합니다 [!DNL Zoho CRM] 계정이 필요합니다. |
| 토큰 새로 고침 | 새로 고침 토큰은 액세스 토큰이 만료되면 새 액세스 토큰을 생성하는 데 사용되는 토큰입니다. |

이러한 자격 증명에 대한 자세한 내용은 [[!DNL Zoho CRM] 인증](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## 연결 [!DNL Zoho CRM] account

필요한 자격 증명을 수집하면 아래 단계에 따라 를 연결할 수 있습니다 [!DNL Zoho CRM] 계정 대상 [!DNL Platform].

플랫폼 UI에서 **[!UICONTROL 소스]** 왼쪽 탐색 모음에서 를 클릭하여 [!UICONTROL 소스] 작업 공간. 다음 [!UICONTROL 카탈로그] 화면에 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래에 [!UICONTROL CRM] 카테고리, 선택 **[!UICONTROL Zoho CRM]**&#x200B;를 선택한 다음 을 선택합니다. **[!UICONTROL 데이터 추가]**.

![카탈로그](../../../../images/tutorials/create/zoho/catalog.png)

다음 **[!UICONTROL Zoho CRM 계정 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정을 사용하려면 [!DNL Zoho CRM] 새 데이터 흐름을 만들 계정을 선택한 다음 **[!UICONTROL 다음]** 계속 진행합니다.

![기존](../../../../images/tutorials/create/zoho/existing.png)

### 새 계정

새 계정을 만드는 경우 **[!UICONTROL 새 계정]**, 그런 다음 이름, 선택적 설명 및 을 입력합니다. [!DNL Zoho CRM] 자격 증명. 완료되면 을 선택합니다 **[!UICONTROL 소스에 연결]** 그런 다음 새 연결이 설정될 시간을 허용합니다.

>[!TIP]
>
>계정 URL 도메인은 해당 도메인 위치에 해당해야 합니다. 다음은 다양한 도메인 및 해당 계정 URL입니다.<ul><li>미국: https://accounts.zoho.com</li><li>오스트레일리아: https://accounts.zoho.com.au</li><li>유럽: https://accounts.zoho.eu</li><li>인도: https://accounts.zoho.in</li><li>중국: https://accounts.zoho.com.cn</li></ul>

![새](../../../../images/tutorials/create/zoho/new.png)

## 다음 단계

이 자습서에 따라 [!DNL Zoho CRM] 계정이 필요합니다. 이제 다음 자습서를 계속 진행하고 [데이터를 플랫폼으로 가져오도록 데이터 흐름 구성](../../dataflow/crm.md).
