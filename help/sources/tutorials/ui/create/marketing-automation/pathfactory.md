---
title: UI를 통해 PathFactory 계정을 Experience Platform에 연결
description: UI를 통해 PathFactory 계정을 Experience Platform에 연결하는 방법을 알아봅니다.
badge: Beta
exl-id: 859dd0c1-8c4b-43e3-a87b-84c879460bc0
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 2%

---

# UI를 통해 [!DNL PathFactory] 계정을 Experience Platform에 연결

이 자습서에서는 UI를 통해 [!DNL PathFactory] 방문자, 세션 및 페이지 보기 수를 Adobe Experience Platform에 연결하는 방법에 대한 단계를 제공합니다.

## 시작하기

이 자습서에서는 Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): [!DNL Experience Platform]에서 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
   * [스키마 컴포지션의 기본 사항](../../../../../xdm/schema/composition.md): 스키마 컴포지션의 주요 원칙 및 모범 사례를 포함하여 XDM 스키마의 기본 구성 요소에 대해 알아봅니다.
   * [스키마 편집기 튜토리얼](../../../../../xdm/tutorials/create-schema-ui.md): 스키마 편집기 UI를 사용하여 사용자 지정 스키마를 만드는 방법을 알아봅니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.

이미 [!DNL PathFactory] 계정이 있는 경우 이 문서의 나머지 부분을 건너뛰고 [UI를 사용하여 Experience Platform에 마케팅 자동화 데이터를 가져오는 중](../../dataflow/marketing-automation.md)에 대한 자습서를 진행할 수 있습니다.

### 필요한 자격 증명 수집 {#gather-credentials}

Experience Platform에서 PathFactory 계정에 액세스하려면 다음 값을 제공해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| 사용자 이름 | PathFactory 계정 사용자 이름입니다. 시스템에서 계정을 식별하는 데 필수적입니다. |
| 암호 | PathFactory 계정과 연결된 암호입니다. 무단 액세스를 방지하기 위해 보안을 유지해야 합니다. |
| 도메인 | PathFactory 계정과 연결된 도메인입니다. 일반적으로 PathFactory URL 내의 고유 식별자를 참조합니다. |
| 액세스 토큰 | 시스템과 PathFactory 간의 보안 통신을 보장하기 위해 API 인증에 사용되는 고유한 토큰입니다. |
| API 엔드포인트 | 데이터 액세스를 위한 특정 API 엔드포인트: 방문자, 세션 및 페이지 보기. 각 끝점은 검색할 수 있는 서로 다른 데이터 세트에 해당합니다. **참고:** 이는 [!DNL PathFactory]에 의해 미리 정의되며 액세스하려는 데이터에만 해당됩니다. <ul><li>**방문자 끝점**: `/api/public/v3/data_lake_apis/visitors.json`</li><li>**세션 끝점**: `/api/public/v3/data_lake_apis/sessions.json`</li><li>**페이지 보기 끝점**: `/api/public/v3/data_lake_apis/page_views.json`</li></ul> |

자격 증명 보안 및 사용 방법에 대한 자세한 지침과 액세스 토큰 획득 및 새로 고침에 대한 자세한 내용은 [PathFactory 지원 센터](https://support.pathfactory.com/categories/adobe/)를 참조하세요. 이 리소스는 자격 증명 관리와 효과적이고 안전한 API 통합에 대한 포괄적인 안내서를 제공합니다.


## [!DNL PathFactory] 계정 연결

Experience Platform UI의 왼쪽 탐색에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 [!UICONTROL 소스] 작업 영역에 액세스합니다. [!UICONTROL 카탈로그]에는 Experience Platform에서 지원하는 다양한 소스가 표시됩니다.

범주 목록에서 적절한 범주를 선택할 수 있습니다. 검색 창을 사용하여 특정 소스를 필터링할 수도 있습니다.

[!UICONTROL 마케팅 자동화] 범주에서 **[!UICONTROL PathFactory]**&#x200B;를 선택한 다음 **[!UICONTROL 설정]**&#x200B;을 선택합니다.

![PathFactory 원본이 있는 원본 카탈로그를 선택했습니다.](../../../../images/tutorials/create/pathfactory/catalog.png)

**[!UICONTROL PathFactory에 연결]** 페이지가 나타납니다. 이 페이지에서 새 계정을 만들거나 기존 계정을 사용할 수 있습니다.

### 새 계정

새 계정을 만들려면 **[!UICONTROL 새 계정]**&#x200B;을(를) 선택하고 계정 이름, 선택적 설명 및 [!DNL PathFactory] 계정에 해당하는 인증 자격 증명을 제공하세요.

완료되면 **[!UICONTROL 소스에 연결]**&#x200B;을 선택한 다음 새 연결을 설정할 수 있는 시간을 허용하세요.

![PathFactory의 새 계정을 인증할 수 있는 새 계정 인터페이스입니다.](../../../../images/tutorials/create/pathfactory/new.png)

### 기존 계정

기존 계정이 이미 있는 경우 **[!UICONTROL 기존 계정]**&#x200B;을 선택한 다음 표시되는 목록에서 사용할 계정을 선택하십시오.

![기존 PathFactory 계정 목록에서 선택할 수 있는 기존 계정 인터페이스](../../../../images/tutorials/create/pathfactory/existing.png)

## 다음 단계

이 자습서를 따라 [!DNL PathFactory] 계정과 Experience Platform 간에 연결을 설정했습니다. 이제 다음 자습서를 계속 진행하고 [데이터 흐름을 만들어 마케팅 자동화 데이터를 Experience Platform으로 가져올 수 있습니다](../../dataflow/marketing-automation.md).
