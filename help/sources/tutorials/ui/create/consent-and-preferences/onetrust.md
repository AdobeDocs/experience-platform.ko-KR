---
keywords: Experience Platform;홈;인기 항목;onetrust;OneTrust
solution: Experience Platform
title: UI에서 OneTrust 원본 연결 만들기
type: Tutorial
description: Adobe Experience Platform UI를 사용하여 OneTrust 소스 연결을 만드는 방법을 알아봅니다.
exl-id: 6af0604d-cbb6-4c8e-b017-3eb82ec6ee1c
source-git-commit: 35095ec8c22106ba0a8f11e0a970ed7989a7f06c
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 0%

---

# 만들기 [!DNL OneTrust Integration] UI의 소스 연결

>[!NOTE]
>
>다음 [!DNL OneTrust Integration] 소스는 쿠키가 아닌 동의 및 환경 설정 데이터 섭취만 지원합니다.

이 자습서에서는 을(를) 만드는 단계를 제공합니다 [[!DNL OneTrust Integration]](https://my.onetrust.com/s/contactsupport?language=en_US) 플랫폼 사용자 인터페이스를 사용하여 내역 및 예약된 동의 데이터를 모두 Adobe Experience Platform에 수집하기 위한 소스 연결입니다.

## 사전 요구 사항

>[!IMPORTANT]
>
>다음 [!DNL OneTrust Integration] 소스 커넥터 및 설명서가 [!DNL OneTrust Integration] 팀 문의 사항이나 업데이트 요청에 대해서는 [[!DNL OneTrust] 팀](https://my.onetrust.com/s/contactsupport?language=en_US) 직접 액세스할 수 있습니다.

연결하기 전에 [!DNL OneTrust Integration] 플랫폼에서는 먼저 액세스 토큰을 검색해야 합니다. 액세스 토큰 찾기에 대한 자세한 지침은 [[!DNL OneTrust Integration] OAuth 2 안내서](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

시스템 간 새로 고침 토큰은 [!DNL OneTrust]. 따라서 액세스 토큰이 만료되기 전에 연결에서 업데이트되는지 확인해야 합니다. 액세스 토큰에 대한 구성 가능한 최대 수명은 1년입니다. 액세스 토큰 업데이트에 대한 자세한 내용은 [[!DNL OneTrust] OAuth 2.0 클라이언트 자격 증명 관리에 대한 문서](https://developer.onetrust.com/docs/documentation/ZG9jOjIyODk1MTUw-managing-o-auth-2-0-client-credentials).

### 필요한 자격 증명 수집

연결하려면 [!DNL OneTrust Integration] 플랫폼에 다음 인증 자격 증명에 대한 값을 제공해야 합니다.

| 자격 증명 | 설명 | 예 |
| --- | --- | --- |
| 호스트 이름 | Adobe Analytics Mobile Apps 또는 Analytics Premium이 [!DNL OneTrust Integration] 데이터를 가져와야 합니다. | `app.onetrust.com` |
| 인증 테스트 URL | (선택 사항) 기본 연결을 만들 때 인증 테스트 URL을 사용하여 자격 증명을 확인합니다. 지정하지 않으면 소스 연결 생성 단계 동안 자격 증명이 자동으로 선택됩니다. |  |
| 액세스 토큰 | 사용자의 [!DNL OneTrust Integration] 계정이 필요합니다. | `ZGFkZDMyMjFhMmEyNDQ2ZGFhNTdkZjNkZjFmM2IyOWE6QjlUSERVUTNjOFVsRmpEZTJ6Vk9oRnF3Sk8xNlNtcm4=` |

이러한 자격 증명에 대한 자세한 내용은 [[!DNL OneTrust Integration] 인증 설명서](https://developer.onetrust.com/docs/api-docs-v3/b3A6MjI4OTUyOTc-generate-access-token).

## 연결 [!DNL OneTrust Integration] account

>[!NOTE]
>
>다음 [!DNL OneTrust Integration] API 사양은 데이터 수집을 위해 Adobe과 공유되고 있습니다.

플랫폼 UI에서 **[!UICONTROL 소스]** 왼쪽 탐색에서 로 이동하여 [!UICONTROL 소스] Experience Platform에서 사용할 수 있는 소스 카탈로그를 위한 작업 공간입니다.

를 사용하십시오 *[!UICONTROL 카테고리]* 메뉴를 사용하여 범주별로 소스를 필터링합니다. 또는 검색 막대에 소스 이름을 입력하여 카탈로그에서 특정 소스를 찾습니다.

로 이동합니다. [!UICONTROL 동의 및 기본 설정] 카테고리 [!DNL OneTrust Integration] 소스 카드. 시작하려면 다음을 선택합니다 **[!UICONTROL 데이터 추가]**.

![Experience Platform UI 소스 카탈로그.](../../../../images/tutorials/create/onetrust/catalog.png)

다음 **[!UICONTROL OneTrust 통합 계정 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정을 사용하려면 [!DNL OneTrust Integration] 새 데이터 흐름을 만들 계정을 선택한 다음 **[!UICONTROL 다음]** 계속 진행합니다.

![소스 워크플로우의 기존 계정 인증 단계입니다.](../../../../images/tutorials/create/onetrust/existing.png)

### 새 계정

새 계정을 만드는 경우 **[!UICONTROL 새 계정]**, 그런 다음 이름, 선택적 설명 및 자격 증명을 제공합니다. 완료되면 을 선택합니다 **[!UICONTROL 소스에 연결]** 그런 다음 새 연결이 설정될 시간을 허용합니다.

![소스 워크플로우의 새 계정 인증 단계입니다.](../../../../images/tutorials/create/onetrust/new.png)

## 다음 단계

이 자습서에 따라 [!DNL OneTrust Integration] 계정이 필요합니다. 이제 다음 자습서를 계속 진행하고 [동의 데이터를 플랫폼으로 가져오도록 데이터 흐름 구성](../../dataflow/consent-and-preferences.md).
