---
keywords: Experience Platform;홈;인기 항목;onetrust;OneTrust
solution: Experience Platform
title: (베타) UI에서 OneTrust 소스 연결 만들기
topic-legacy: overview
type: Tutorial
description: Adobe Experience Platform UI를 사용하여 OneTrust 소스 연결을 만드는 방법을 알아봅니다.
source-git-commit: adefaeb895c91d45727f791b73b73a17a2b1ccf9
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 1%

---

# (베타) 만들기 [!DNL OneTrust Integration] UI의 소스 연결

>[!NOTE]
>
>다음 [!DNL OneTrust Integration] 소스가 베타 버전입니다. 해당 기능과 설명서는 변경될 수 있습니다. 베타 레이블이 지정된 소스 사용에 대한 자세한 내용은 [소스 개요](../../../../home.md#terms-and-conditions).

이 자습서에서는 을(를) 만드는 단계를 제공합니다 [[!DNL OneTrust Integration]](https://my.onetrust.com/s/contactsupport?language=en_US) 플랫폼 사용자 인터페이스를 사용하여 내역 및 예약된 동의 데이터를 모두 Adobe Experience Platform에 수집하기 위한 소스 연결입니다.

## 전제 조건

>[!IMPORTANT]
>
>다음 [!DNL OneTrust Integration] 소스 커넥터 및 설명서가 [!DNL OneTrust Integration] 팀 문의 사항이나 업데이트 요청에 대해서는 [[!DNL OneTrust] 팀](https://my.onetrust.com/s/contactsupport?language=en_US) 직접 액세스할 수 있습니다.

연결하기 전에 [!DNL OneTrust Integration] 플랫폼에서는 먼저 액세스 토큰을 검색해야 합니다. 액세스 토큰 찾기에 대한 자세한 지침은 [[!DNL OneTrust Integration] OAuth 2 안내서](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

시스템 간 새로 고침 토큰은 [!DNL OneTrust]. 따라서 액세스 토큰이 만료되기 전에 연결에서 업데이트되는지 확인해야 합니다. 액세스 토큰에 대한 구성 가능한 최대 수명은 1년입니다. 액세스 토큰 업데이트에 대한 자세한 내용은 [[!DNL OneTrust] OAuth 2.0 클라이언트 자격 증명 관리에 대한 문서](https://developer.onetrust.com/docs/documentation/ZG9jOjIyODk1MTUw-managing-o-auth-2-0-client-credentials).

### 필요한 자격 증명 수집

연결하려면 [!DNL OneTrust Integration] 플랫폼에 다음 인증 자격 증명에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 | 예 |
| --- | --- | --- |
| Host | Adobe Analytics Mobile Apps 또는 Analytics Premium이 [!DNL OneTrust Integration] 데이터를 가져와야 합니다. | `https://uat.onetrust.com/` |
| 인증 테스트 URL | (선택 사항) 기본 연결을 만들 때 인증 테스트 URL을 사용하여 자격 증명을 확인합니다. 지정하지 않으면 소스 연결 생성 단계 동안 자격 증명이 자동으로 선택됩니다. |  |
| 액세스 토큰 | 사용자의 [!DNL OneTrust Integration] 계정이 필요합니다. | `ZGFkZDMyMjFhMmEyNDQ2ZGFhNTdkZjNkZjFmM2IyOWE6QjlUSERVUTNjOFVsRmpEZTJ6Vk9oRnF3Sk8xNlNtcm4=` |

이러한 자격 증명에 대한 자세한 내용은 [[!DNL OneTrust Integration] 인증 설명서](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

## 연결 [!DNL OneTrust Integration] account

>[!NOTE]
>
>다음 [!DNL OneTrust Integration] API 사양은 데이터 수집을 위해 Adobe과 공유되고 있습니다.

플랫폼 UI에서 **[!UICONTROL 소스]** 왼쪽 탐색에서 로 이동하여 [!UICONTROL 소스] 작업 공간. 다음 [!UICONTROL 카탈로그] 화면에 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래에 *[!UICONTROL 동의 및 기본 설정]* 카테고리, 선택 [!DNL OneTrust Integration]를 선택한 다음 을 선택합니다. **[!UICONTROL 데이터 추가]**.

![카탈로그](../../../../images/tutorials/create/onetrust/catalog.png)

다음 **[!UICONTROL OneTrust 통합 계정 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정을 사용하려면 [!DNL OneTrust Integration] 새 데이터 흐름을 만들 계정을 선택한 다음 **[!UICONTROL 다음]** 계속 진행합니다.

![기존](../../../../images/tutorials/create/onetrust/existing.png)

### 새 계정

새 계정을 만드는 경우 **[!UICONTROL 새 계정]**, 그런 다음 이름, 선택적 설명 및 자격 증명을 제공합니다. 완료되면 을 선택합니다 **[!UICONTROL 소스에 연결]** 그런 다음 새 연결이 설정될 시간을 허용합니다.

![새](../../../../images/tutorials/create/onetrust/new.png)

## 다음 단계

이 자습서에 따라 [!DNL OneTrust Integration] 계정이 필요합니다. 이제 다음 자습서를 계속 진행하고 [동의 데이터를 플랫폼으로 가져오도록 데이터 흐름 구성](../../dataflow/consent-and-preferences.md).