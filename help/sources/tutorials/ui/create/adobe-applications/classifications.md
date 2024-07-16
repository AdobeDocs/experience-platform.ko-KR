---
keywords: Experience Platform;홈;인기 항목; 분석;분류
description: UI에서 Adobe Analytics 소스 커넥터를 만들어 분류 데이터를 Adobe Experience Platform으로 가져오는 방법을 알아봅니다.
solution: Experience Platform
title: UI에서 분류 데이터에 대한 Adobe Analytics Source 연결 만들기
type: Tutorial
exl-id: d606720d-f1ca-47cc-919b-643a8fc61e07
source-git-commit: fcebef97ba9cc667f80afd55980c5460912a56fb
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 0%

---

# UI에서 분류 데이터에 대한 Adobe Analytics 소스 연결 만들기

이 자습서에서는 분류 데이터를 Adobe Experience Platform으로 가져오기 위해 UI에서 Adobe Analytics 분류 데이터 소스 연결을 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

Analytics 분류 데이터 커넥터를 사용하려면 데이터를 Adobe Analytics의 새 [!DNL Classifications] 인프라로 마이그레이션해야 합니다. 데이터의 마이그레이션 상태를 확인하려면 Adobe 계정 팀에 문의하십시오.

## 분류 선택

[Adobe Experience Platform](https://platform.adobe.com)에 로그인한 다음 왼쪽 탐색 막대에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 소스 작업 영역에 액세스합니다. **[!UICONTROL 카탈로그]** 화면에 인바운드 연결을 만드는 데 사용할 수 있는 원본이 표시됩니다. 각 소스 카드에는 새 계정을 구성하거나 기존 계정에 데이터를 추가하는 옵션이 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

**[!UICONTROL Adobe 응용 프로그램]** 범주에서 **[!UICONTROL Adobe Analytics]** 카드를 선택한 다음 **[!UICONTROL 데이터 추가]**&#x200B;를 선택하여 Analytics 분류 데이터 작업을 시작합니다.

![](../../../../images/tutorials/create/classifications/catalog.png)

**[!UICONTROL Analytics 원본 데이터 추가]** 단계가 나타납니다. 차원 ID, 보고서 세트 이름 및 보고서 세트 ID에 대한 정보가 포함된 [!DNL Classifications] 데이터 세트 목록을 보려면 상단 헤더에서 **[!UICONTROL 분류]**&#x200B;을(를) 선택하십시오.

각 페이지에는 선택할 수 있는 최대 10개의 서로 다른 [!DNL Classifications] 데이터 세트가 표시됩니다. 더 많은 옵션을 찾아보려면 페이지 하단에서 **[!UICONTROL 다음]**&#x200B;을(를) 선택하십시오. 오른쪽 패널에는 선택한 총 [!DNL Classifications]개 데이터 세트 수와 해당 이름이 표시됩니다. 또한 이 패널을 사용하면 실수로 선택한 [!DNL Classifications] 데이터 세트를 제거하거나 한 번의 작업으로 모든 선택 항목을 지울 수 있습니다.

최대 30개의 서로 다른 [!DNL Classifications] 데이터 세트를 선택하여 [!DNL Platform]에 가져올 수 있습니다.

[!DNL Classifications] 데이터 세트를 선택한 후에는 페이지의 오른쪽 상단에서 **[!UICONTROL 다음]**&#x200B;을(를) 선택하십시오.

![](../../../../images/tutorials/create/classifications/add-data.png)

## 분류 검토

**[!UICONTROL 검토]** 단계가 표시되어 선택한 [!DNL Classifications] 데이터 세트를 만들기 전에 검토할 수 있습니다. 세부 사항은 다음 범주 내에서 그룹화됩니다.

* **[!UICONTROL 연결]**: 원본 플랫폼과 연결 상태를 표시합니다.
* **[!UICONTROL 데이터 형식]**: 선택한 [!DNL Classifications]의 수를 표시합니다.
* **[!UICONTROL 예약]**: [!DNL Classifications] 데이터의 동기화 빈도를 표시합니다.

데이터 흐름을 검토한 후 **[!UICONTROL 완료]**&#x200B;를 클릭하고 데이터 흐름이 만들어지도록 잠시 기다립니다.

![](../../../../images/tutorials/create/classifications/review.png)

## 분류 데이터 흐름 모니터링

데이터 흐름이 만들어지면 데이터 흐름을 통해 수집되는 데이터를 모니터링할 수 있습니다. **[!UICONTROL 카탈로그]** 화면에서 **[!UICONTROL 데이터 흐름]**&#x200B;을 선택하여 [!DNL Classifications] 계정과 연결된 설정된 흐름 목록을 봅니다.

![](../../../../images/tutorials/create/classifications/dataflows.png)

**[!UICONTROL 데이터 흐름]** 화면이 나타납니다. 이 페이지에는 이름, 소스 데이터 및 데이터 흐름 실행 상태에 대한 정보를 포함한 데이터 흐름 목록이 있습니다. 오른쪽에는 [!DNL Classifications] 데이터 흐름과 관련된 메타데이터가 포함된 **[!UICONTROL 속성]** 패널이 있습니다.

액세스하려는 **[!UICONTROL 대상 데이터 세트]**&#x200B;를 선택하십시오.

![](../../../../images/tutorials/create/classifications/list-of-dataflows.png)

**[!UICONTROL 데이터 집합 활동]** 페이지에는 일괄 처리 상태, 데이터 집합 ID 및 스키마에 대한 세부 정보를 포함하여 선택한 대상 데이터 집합에 대한 정보가 표시됩니다.

![](../../../../images/tutorials/create/classifications/dataset.png)

## 다음 단계

이 자습서를 따라 [!DNL Classifications] 데이터를 [!DNL Platform](으)로 가져오는 Analytics 분류 데이터 커넥터를 만들었습니다. [!DNL Analytics] 및 [!DNL Classifications] 데이터에 대한 자세한 내용은 다음 문서를 참조하십시오.

* [Analytics 데이터 커넥터 개요](../../../../connectors/adobe-applications/analytics.md)
* [UI에서 Analytics 데이터 연결 만들기](./analytics.md)
* [분류 정보](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html)
