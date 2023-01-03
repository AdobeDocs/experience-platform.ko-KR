---
keywords: Experience Platform;홈;인기 항목;Google Big Query;google big 쿼리;GBQ;gbq
solution: Experience Platform
title: UI에서 Google 대용량 쿼리 소스 연결 만들기
topic-legacy: overview
type: Tutorial
description: Adobe Experience Platform UI를 사용하여 Google Big Query 소스 연결을 만드는 방법을 알아봅니다.
exl-id: 3c0902de-48b9-42d8-a4bd-0213ca85fc7f
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 1%

---

# 만들기 [!DNL Google Big Query] UI의 소스 연결

Adobe Experience Platform의 소스 커넥터는 예약된 방식으로 외부 소스 데이터를 수집할 수 있습니다. 이 자습서에서는 을(를) 만드는 단계를 제공합니다 [!DNL Google Big Query] 플랫폼 사용자 인터페이스를 사용한 소스 연결.

## 시작하기

이 자습서에서는 Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 작성 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 빌딩 블록에 대해 알아봅니다.
   * [스키마 편집기 자습서](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아보십시오.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 유효한 [!DNL Google BigQuery] 연결을 통해 이 문서의 나머지 부분을 건너뛰고 다음 자습서를 진행할 수 있습니다. [데이터 흐름 구성](../../dataflow/databases.md).

### 필요한 자격 증명 수집

에 액세스하려면 [!DNL Google BigQuery] 플랫폼의 계정은 다음 OAuth 2.0 인증 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `project` | 기본값은 프로젝트 ID입니다 [!DNL Google BigQuery] 쿼리할 프로젝트입니다. |
| `clientID` | 새로 고침 토큰을 생성하는 데 사용되는 ID 값입니다. |
| `clientSecret` | 새로 고침 토큰을 생성하는 데 사용되는 암호 값입니다. |
| `refreshToken` | 에서 가져온 새로 고침 토큰 [!DNL Google] 액세스 권한을 인증하는 데 사용됩니다. [!DNL Google BigQuery]. |

이러한 값에 대한 자세한 내용은 [이 [!DNL Google BigQuery] 문서](https://cloud.google.com/storage/docs/json_api/v1/how-tos/authorizing).

## Google BigQuery 계정 연결

플랫폼 UI에서 **[!UICONTROL 소스]** 왼쪽 탐색에서 로 이동하여 [!UICONTROL 소스] 작업 공간. 다음 [!UICONTROL 카탈로그] 화면에는 계정을 만들 수 있는 다양한 소스가 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 막대를 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래에 [!UICONTROL 데이터베이스] 카테고리, 선택 **[!UICONTROL Google BigQuery]** 그런 다음 **[!UICONTROL 데이터 추가]**.

![](../../../../images/tutorials/create/google-big-query/catalog.png)

다음 **[!UICONTROL Google Big Query에 연결]** 페이지가 나타납니다. 이 페이지에서 새 자격 증명 또는 기존 자격 증명을 사용할 수 있습니다.

### 기존 계정

기존 계정을 연결하려면 [!DNL Google BigQuery] 연결할 계정을 선택한 다음 **[!UICONTROL 다음]** 계속 진행합니다.

![](../../../../images/tutorials/create/google-big-query/existing.png)

### 새 계정

새 자격 증명을 사용하는 경우 **[!UICONTROL 새 계정]**. 표시되는 입력 양식에서 이름, 선택적 설명 및 [!DNL Google BigQuery] 자격 증명. 완료되면 을 선택합니다 **[!UICONTROL 소스에 연결]** 그런 다음 새 연결이 설정될 시간을 허용합니다.

![](../../../../images/tutorials/create/google-big-query/new.png)

## 다음 단계

이 자습서에 따라 [!DNL Google BigQuery] 계정이 필요합니다. 이제 다음 자습서를 계속 진행하고 [데이터를 플랫폼으로 가져오도록 데이터 흐름 구성](../../dataflow/databases.md).
