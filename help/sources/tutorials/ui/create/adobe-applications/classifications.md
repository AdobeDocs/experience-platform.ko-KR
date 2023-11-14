---
keywords: Experience Platform;홈;인기 항목; 분석;분류
description: UI에서 Adobe Analytics 소스 커넥터를 만들어 분류 데이터를 Adobe Experience Platform으로 가져오는 방법을 알아봅니다.
solution: Experience Platform
title: UI에서 분류 데이터에 대한 Adobe Analytics 소스 연결 만들기
type: Tutorial
exl-id: d606720d-f1ca-47cc-919b-643a8fc61e07
source-git-commit: fcebef97ba9cc667f80afd55980c5460912a56fb
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 2%

---

# UI에서 분류 데이터에 대한 Adobe Analytics 소스 연결 만들기

이 자습서에서는 분류 데이터를 Adobe Experience Platform으로 가져오기 위해 UI에서 Adobe Analytics 분류 데이터 소스 연결을 만드는 단계를 제공합니다.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 소스의 집계 데이터를 기반으로 통합 실시간 소비자 프로필을 제공합니다.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

Analytics 분류 데이터 커넥터 를 사용하려면 데이터를 새 로 마이그레이션해야 합니다 [!DNL Classifications] 사용 전 Adobe Analytics 인프라. 데이터의 마이그레이션 상태를 확인하려면 Adobe 계정 팀에 문의하십시오.

## 분류 선택

에 로그인 [Adobe Experience Platform](https://platform.adobe.com) 다음을 선택합니다. **[!UICONTROL 소스]** 소스 작업 공간에 액세스하려면 왼쪽 탐색 모음에서 를 사용하십시오. 다음 **[!UICONTROL 카탈로그]** 화면에는 인바운드 연결을 만들 수 있는 사용 가능한 소스가 표시됩니다. 각 소스 카드에는 새 계정을 구성하거나 기존 계정에 데이터를 추가하는 옵션이 표시됩니다.

화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

아래 **[!UICONTROL Adobe 애플리케이션]** 범주를 선택한 다음 **[!UICONTROL Adobe Analytics]** 카드를 선택한 다음 선택 **[!UICONTROL 데이터 추가]** analytics 분류 데이터 작업을 시작합니다.

![](../../../../images/tutorials/create/classifications/catalog.png)

다음 **[!UICONTROL Analytics 소스 데이터 추가]** 단계가 나타납니다. 선택 **[!UICONTROL 분류]** 을 클릭하여 목록을 확인합니다. [!DNL Classifications] 차원 ID, 보고서 세트 이름 및 보고서 세트 ID에 대한 정보가 포함된 데이터 세트입니다.

각 페이지에는 최대 10개의 다른 페이지가 표시됩니다 [!DNL Classifications] 데이터 세트 중에서 선택할 수 있습니다. 선택 **[!UICONTROL 다음]** 페이지 하단에서 추가 옵션을 찾아봅니다. 오른쪽 패널에 의 총 수가 표시됩니다. [!DNL Classifications] 선택한 데이터 세트 및 해당 이름. 이 패널을 통해 다음을 제거할 수도 있습니다. [!DNL Classifications] 실수로 선택했거나 한 번의 작업으로 모든 선택 항목을 지웠을 수 있는 데이터 세트입니다.

최대 30개까지 선택할 수 있습니다 [!DNL Classifications] 가져올 데이터 세트 [!DNL Platform].

을(를) 선택하면 [!DNL Classifications] 데이터 세트, 선택 **[!UICONTROL 다음]** 페이지의 오른쪽 상단에 있습니다.

![](../../../../images/tutorials/create/classifications/add-data.png)

## 분류 검토

다음 **[!UICONTROL 리뷰]** 선택한 항목을 검토할 수 있는 단계가 나타납니다. [!DNL Classifications] 데이터 세트를 만들기 전에 선택합니다. 세부 사항은 다음 범주 내에서 그룹화됩니다.

* **[!UICONTROL 연결]**: 소스 플랫폼과 연결 상태를 표시합니다.
* **[!UICONTROL 데이터 유형]**: 선택한 항목 수를 표시합니다. [!DNL Classifications].
* **[!UICONTROL 예약]**: 동기화 빈도를 표시합니다. [!DNL Classifications] 데이터.

데이터 흐름을 검토하고 나면 **[!UICONTROL 완료]** 데이터 흐름이 만들어지는 데 시간이 걸릴 수 있습니다.

![](../../../../images/tutorials/create/classifications/review.png)

## 분류 데이터 흐름 모니터링

데이터 흐름이 만들어지면 데이터 흐름을 통해 수집되는 데이터를 모니터링할 수 있습니다. 다음에서 **[!UICONTROL 카탈로그]** 화면, 선택 **[!UICONTROL 데이터 흐름]** 와(과) 연결된 설정된 플로우 목록을 보려면 다음과 같이 하십시오. [!DNL Classifications] 계정입니다.

![](../../../../images/tutorials/create/classifications/dataflows.png)

다음 **[!UICONTROL 데이터 흐름]** 화면이 나타납니다. 이 페이지에는 이름, 소스 데이터 및 데이터 흐름 실행 상태에 대한 정보를 포함한 데이터 흐름 목록이 있습니다. 오른쪽에는 **[!UICONTROL 속성]** 패널 - 과 관련된 메타데이터가 포함되어 있습니다. [!DNL Classifications] 데이터 흐름.

다음 항목 선택 **[!UICONTROL 타겟 데이터 세트]** 에 액세스하려고 합니다.

![](../../../../images/tutorials/create/classifications/list-of-dataflows.png)

다음 **[!UICONTROL 데이터 세트 활동]** 이 페이지에는 일괄 처리 상태, 데이터 세트 ID 및 스키마에 대한 세부 정보를 포함하여 선택한 대상 데이터 세트에 대한 정보가 표시됩니다.

![](../../../../images/tutorials/create/classifications/dataset.png)

## 다음 단계

이 자습서에 따라 를 가져오는 Analytics 분류 데이터 커넥터를 만들었습니다 [!DNL Classifications] 데이터 입력 [!DNL Platform]. 자세한 내용은 다음 문서를 참조하십시오 [!DNL Analytics] 및 [!DNL Classifications] 데이터:

* [Analytics 데이터 커넥터 개요](../../../../connectors/adobe-applications/analytics.md)
* [UI에서 Analytics 데이터 연결 만들기](./analytics.md)
* [분류 정보](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html)
