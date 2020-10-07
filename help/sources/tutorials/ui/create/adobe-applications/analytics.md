---
keywords: Experience Platform;home;popular topics;Analytics source connector;Analytics connector;Analytics source;analytics
solution: Experience Platform
title: UI에서 Adobe Analytics 소스 커넥터 만들기
topic: overview
type: Tutorial
description: 이 자습서에서는 소비자 데이터를 Adobe Experience Platform으로 가져오기 위해 UI에서 Adobe Analytics 소스 커넥터를 만드는 단계를 제공합니다.
translation-type: tm+mt
source-git-commit: 8c94d3631296c1c3cc97501ccf1a3ed995ec3cab
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 1%

---


# UI에서 Adobe Analytics 소스 커넥터 만들기

이 자습서에서는 소비자 데이터를 Adobe Experience Platform으로 가져오기 위해 UI에서 Adobe Analytics 소스 커넥터를 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 다음 Adobe Experience Platform 구성 요소에 대해 작업해야 합니다.

* [XDM(Experience Data Model) 시스템](../../../../../xdm/home.md):Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
* [실시간 고객 프로필](../../../../../profile/home.md):여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
* [샌드박스](../../../../../sandboxes/home.md):Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되도록 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

## Adobe Analytics과 소스 연결 만들기

소스 작업 영역에 액세스하려면 [Adobe Experience Platform](https://platform.adobe.com) 에 로그인한 다음 **** 왼쪽 탐색 막대에서 소스를 선택합니다. [ **카탈로그** ] 화면에는 인바운드 연결을 만들 수 있는 사용 가능한 소스가 표시되고 각 소스에는 연관된 기존 계정 및 데이터 세트 흐름 수가 표시됩니다.

화면의 왼쪽에 있는 카탈로그에서 해당 범주를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

Adobe 애플리케이션 **[!UICONTROL 카테고리 아래에서]** Adobe Analytics **** 을 선택하여 화면 오른쪽에 정보 막대를 표시합니다. 정보 표시줄에는 선택한 소스에 대한 간단한 설명과 소스와 연결하거나 설명서를 보는 옵션이 제공됩니다. 기존 계정을 보려면 계정 **[!UICONTROL 을 선택합니다]**.

![](../../../../images/tutorials/create/analytics/catalog.png)

### 데이터 선택

Adobe Analytics **[!UICONTROL 단계가]** 나타납니다. 이전에 설정한 Analytics 데이터 세트 흐름이 이 화면에 나열됩니다. 데이터 선택을 클릭하여 새 데이터 세트 흐름 **[!UICONTROL 을 만들 수 있습니다]**.

>[!NOTE]
>
>서로 다른 데이터를 가져오기 위해 소스에 여러 연결 기능을 사용할 수 있습니다.

![](../../../../images/tutorials/create/analytics/dataset-flows.png)

<!---Analytics report suites can be configured for one sandbox at a time. To import the same report suite into a different sandbox, the dataset flow will have to be deleted and instantiated again via configuration for a different sandbox.--->

사용 가능한 보고서 세트 목록에서 플랫폼으로 가져올 보고서 세트를 선택하고 **[!UICONTROL 다음을 클릭합니다]**.

![](../../../../images/tutorials/create/analytics/select-data.png)

### 데이터 세트 흐름 이름 지정

데이터 세트 **[!UICONTROL 흐름 세부]** 단계가 나타나며, 여기에서 데이터 세트 흐름에 대한 이름과 선택적 설명을 제공해야 합니다. 완료되면 **[!UICONTROL 다음]** 을 선택합니다.

![](../../../../images/tutorials/create/analytics/dataset-flow-detail.png)

### 데이터 세트 흐름 검토

검토 **** 단계가 나타나므로 새로 생성된 Analytics 데이터 세트 흐름을 검토할 수 있습니다. 연결 세부 사항은 다음을 포함하여 범주별로 그룹화됩니다.

* **[!UICONTROL 연결]**:소스 연결 유형과 선택한 보고서 세트를 표시합니다.
* **[!UICONTROL 데이터 세트 및 매핑 필드 할당]**:다른 소스 커넥터를 만들 때 이 컨테이너는 데이터 세트가 준수하는 스키마를 포함하여 소스 데이터가 수집 중인 데이터 세트를 표시합니다. 출력 스키마 및 데이터 세트는 Analytics 데이터 세트 흐름에 대해 자동으로 구성됩니다.

![](../../../../images/tutorials/create/analytics/review.png)

### 데이터 세트 흐름 모니터링

데이터 세트 흐름이 만들어지면 데이터 세트를 통해 수집되는 데이터를 모니터링할 수 있습니다. [ **[!UICONTROL 카탈로그]** ] 화면에서 **[!UICONTROL 데이터 세트 흐름]** 을 선택하여 Analytics 계정과 연결된 설정된 흐름 목록을 봅니다.

![](../../../../images/tutorials/create/analytics/catalog-dataset-flows.png)

데이터 **집합 흐름** 화면이 나타납니다. 이 페이지에는 이름, 소스 데이터, 생성 시간 및 상태에 대한 정보를 포함한 데이터 세트 흐름 쌍이 있습니다.

커넥터가 두 개의 데이터 세트 흐름을 인스턴스화합니다. 한 흐름은 채우기 데이터를, 다른 흐름은 라이브 데이터를 나타냅니다. 채우기 데이터는 프로필에 대해 구성되지 않지만 분석 및 데이터 과학 사용 사례를 위해 데이터 호수로 전송됩니다.

채우기, 라이브 데이터 및 해당 대기 시간에 대한 자세한 내용은 [Analytics 데이터 커넥터 개요를 참조하십시오](../../../../connectors/adobe-applications/analytics.md).

목록에서 보려는 데이터 집합 흐름을 선택합니다.

![](../../../../images/tutorials/create/analytics/backfill.png)

데이터 **집합 활동** 페이지가 나타납니다. 이 페이지는 그래프 형식으로 소비되는 메시지 비율을 표시합니다. 상단 헤더에서 *데이터 거버넌스를* 선택하여 레이블 지정 필드에 액세스합니다.

![](../../../../images/tutorials/create/analytics/batches.png)

데이터 집합 흐름의 상속된 레이블을 *데이터 거버넌스* 화면에서 볼 수 있습니다. 특정 레이블에 액세스하려면 오른쪽 상단에 있는 편집 버튼을 선택합니다.

![](../../../../images/tutorials/create/analytics/data-gov.png)

관리 **레이블 편집** 패널이 나타납니다. 이 화면에서는 데이터 세트 흐름의 계약, ID 및 중요한 레이블에 액세스하고 편집할 수 있습니다.

Analytics에서 오는 데이터에 레이블을 지정하는 방법에 대한 자세한 내용은 [데이터 사용 레이블 안내서를 참조하십시오](../../../../../data-governance/labels/user-guide.md).

![](../../../../images/tutorials/create/analytics/labels.png)

## 다음 단계 및 추가 리소스

연결이 만들어지면 들어오는 데이터를 포함하도록 대상 스키마 및 데이터 세트 흐름이 자동으로 생성됩니다. 또한 데이터 다시 채우기가 발생하고 최대 13개월 동안의 이전 데이터가 수집됩니다. 초기 수집이 완료되면 Analytics 데이터가 수집되고 실시간 고객 프로필 및 세그멘테이션 서비스와 같은 다운스트림 플랫폼 서비스에서 사용됩니다. 자세한 내용은 다음 문서를 참조하십시오.

* [실시간 고객 프로필 개요](../../../../../profile/home.md)
* [세그멘테이션 서비스 개요](../../../../../segmentation/home.md)
* [데이터 과학 작업 공간 개요](../../../../../data-science-workspace/home.md)
* [쿼리 서비스 개요](../../../../../query-service/home.md)

다음 비디오는 Adobe Analytics 소스 커넥터를 사용하는 인제스트 데이터에 대한 이해를 지원하기 위한 것입니다.

>[!WARNING]
>
> 다음 비디오에 표시된 [!DNL Platform] UI가 오래되었습니다. 최신 UI 스크린샷 및 기능은 위의 설명서를 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/29687?quality=12&learn=on)

