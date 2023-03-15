---
keywords: Experience Platform;홈;인기 항목;Google Big Query;google Big Query;GBQ;gbq
solution: Experience Platform
title: UI에서 Google Big Query 소스 연결 만들기
type: Tutorial
description: Adobe Experience Platform UI를 사용하여 Google Big Query 소스 연결을 만드는 방법을 알아봅니다.
exl-id: 3c0902de-48b9-42d8-a4bd-0213ca85fc7f
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 1%

---

# 만들기 [!DNL Google Big Query] UI의 소스 연결

Adobe Experience Platform의 소스 커넥터는 일정에 따라 외부 소스 데이터를 수집하는 기능을 제공합니다. 이 자습서에서는 다음을 만드는 단계를 제공합니다 [!DNL Google Big Query] 플랫폼 사용자 인터페이스를 사용한 소스 연결.

## 시작하기

이 자습서에서는 다음 Experience Platform 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 정의 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 소스의 집계 데이터를 기반으로 통합 실시간 소비자 프로필을 제공합니다.

이미 유효한 을(를) 가지고 있는 경우 [!DNL Google BigQuery] 연결을 통해 이 문서의 나머지 부분을 건너뛰고 다음 튜토리얼을 진행할 수 있습니다. [데이터 흐름 구성](../../dataflow/databases.md).

### 필요한 자격 증명 수집

에 액세스하려면 [!DNL Google BigQuery] 플랫폼의 계정에서 다음 OAuth 2.0 인증 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `project` | 기본값의 프로젝트 ID [!DNL Google BigQuery] 쿼리할 프로젝트입니다. |
| `clientID` | 새로 고침 토큰을 생성하는 데 사용되는 ID 값입니다. |
| `clientSecret` | 새로 고침 토큰을 생성하는 데 사용되는 비밀 값. |
| `refreshToken` | 다음에서 얻은 새로 고침 토큰: [!DNL Google] 에 대한 액세스 권한을 부여하는 데 사용됨 [!DNL Google BigQuery]. |

이러한 값에 대한 자세한 내용은 [이 [!DNL Google BigQuery] 문서](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing).

## Google BigQuery 계정 연결

Platform UI에서 를 선택합니다. **[!UICONTROL 소스]** 을(를) 왼쪽 탐색에서 [!UICONTROL 소스] 작업 영역. 다음 [!UICONTROL 카탈로그] 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 창을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래 [!UICONTROL 데이터베이스] 범주, 선택 **[!UICONTROL Google Bigquery]** 다음을 선택합니다. **[!UICONTROL 데이터 추가]**.

![](../../../../images/tutorials/create/google-big-query/catalog.png)

다음 **[!UICONTROL Google Big Query에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정을 연결하려면 [!DNL Google BigQuery] 연결할 계정을 선택한 다음 **[!UICONTROL 다음]** 계속합니다.

![](../../../../images/tutorials/create/google-big-query/existing.png)

### 새 계정

새 자격 증명을 사용하는 경우 다음을 선택합니다 **[!UICONTROL 새 계정]**. 표시되는 입력 양식에서 이름, 설명(선택 사항) 및 [!DNL Google BigQuery] 자격 증명. 완료되면 다음을 선택합니다. **[!UICONTROL 소스에 연결]** 그런 다음 새 연결을 설정하는 데 시간이 걸릴 수 있습니다.

![](../../../../images/tutorials/create/google-big-query/new.png)

## 다음 단계

이 자습서를 따라 [!DNL Google BigQuery] 계정입니다. 이제 다음 튜토리얼을 계속 진행하여 [데이터를 Platform으로 가져오는 데이터 흐름 구성](../../dataflow/databases.md).
