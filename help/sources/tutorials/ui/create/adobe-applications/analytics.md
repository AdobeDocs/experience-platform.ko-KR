---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: UI에서 Adobe Analytics 소스 커넥터 만들기
topic: overview
translation-type: tm+mt
source-git-commit: ac1e5dbe435d9e85e8ce3ad90c60dd31ba9248ff

---


# UI에서 Adobe Analytics 소스 커넥터 만들기

이 자습서에서는 소비자 데이터를 Adobe Experience Platform으로 가져오기 위해 UI에서 Adobe Analytics 소스 커넥터를 만드는 단계를 제공합니다.

## Adobe Analytics를 사용하여 소스 연결 만들기

Adobe Experience <a href="https://platform.adobe.com" target="_blank">Platform에</a> 로그인한 다음 **왼쪽 탐색** 막대에서 소스를 선택하여 소스 작업 영역에 액세스합니다. [ *카탈로그* ] 화면에는 바인딩 연결을 만들 수 있는 사용 가능한 소스가 표시되며, 각 소스에는 연결된 기존 연결 수가 표시됩니다. Adobe Analytics에 대한 **옵션을** 선택한 다음 소스 **** 보기를 클릭하여 설정된 모든 내부 연결을 확인합니다.

![](../../../../images/tutorials/create/analytics/AA-sources_catalog.png)

소스 *활동* 화면에는 이전에 설정한 Adobe Analytics에 대한 모든 연결이 나열되며 데이터 **선택을 클릭하여 새 연결을 만들 수**&#x200B;있습니다.

>[!NOTE] 서로 다른 데이터를 가져오기 위해 소스에 대한 여러 연결 기능을 사용할 수 있습니다.

![](/help/sources/images/tutorials/create/analytics/AA-source_activity.png)

사용 가능한 보고서 세트 목록에서 플랫폼으로 가져올 보고서 세트를 선택하고 다음을 **클릭합니다**.

>[!NOTE] Analytics 소스 연결당 하나의 보고서 세트만 선택할 수 있습니다. 또한 하나의 보고서 세트만 하나의 샌드박스에만 존재할 수 있습니다.

![](../../../../images/tutorials/create/analytics/AA-select_data.png)

검토 *단계가* 표시되어 새 Analytics가 생성되기 전에 바인딩 연결을 검토할 수 있습니다. 연결 세부 사항은 다음을 포함하여 범주별로 그룹화됩니다.

* *소스 세부 정보*:소스 연결 유형과 선택한 보고서 세트를 표시합니다.
* *타겟 세부 사항*:다른 소스 커넥터를 만들 때 이 컨테이너는 데이터 집합이 준수하는 스키마를 포함하여 소스 데이터가 인제스트하는 데이터 집합을 표시합니다. 분석 데이터는 자동으로 매핑되고 실시간 고객 프로파일에 수집됩니다.

![](../../../../images/tutorials/create/analytics/AA-review.png)

## 다음 단계

연결이 만들어지면 들어오는 데이터를 포함하도록 대상 스키마와 데이터 세트가 자동으로 생성됩니다. 또한 데이터 다시 채우기가 발생하고 최대 13개월 동안의 내역 데이터를 인제스트합니다. 초기 수집이 완료되면 Analytics 데이터가 수집되고 실시간 고객 프로필 및 세그멘테이션 서비스와 같은 다운스트림 플랫폼 서비스에서 사용됩니다. 자세한 내용은 다음 문서를 참조하십시오.

* [실시간 고객 프로필 개요](../../../../../profile/home.md)
* [세그멘테이션 서비스 개요](../../../../../segmentation/home.md)
* [데이터 과학 작업 공간 개요](../../../../../data-science-workspace/home.md)
* [쿼리 서비스 개요](../../../../../query-service/home.md)

