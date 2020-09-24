---
keywords: Experience Platform;home;popular topics;Audience manager source connector;Audience Manager;audience manager connector
solution: Experience Platform
title: UI에서 Adobe Audience Manager 소스 커넥터 만들기
topic: overview
type: Tutorial
description: 이 자습서에서는 사용자 인터페이스를 사용하여 소비자 경험 이벤트 데이터를 플랫폼에 가져오기 위한 Adobe Audience Manager용 소스 커넥터를 만드는 단계를 안내합니다.
translation-type: tm+mt
source-git-commit: 97dfd3a9a66fe2ae82cec8954066bdf3b6346830
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 2%

---


# UI에서 Adobe Audience Manager 소스 커넥터 만들기

이 자습서에서는 사용자 인터페이스를 사용하여 소비자 경험 이벤트 데이터를 플랫폼에 가져오기 위한 Adobe Audience Manager용 소스 커넥터를 만드는 단계를 안내합니다.

## Adobe Audience Manager과 소스 연결 만들기

소스 작업 영역에 액세스하려면 [Adobe Experience Platform](https://platform.adobe.com) 에 로그인한 다음 **** 왼쪽 탐색 막대에서 소스를 선택합니다. [ *카탈로그* ] 화면에는 소스 연결을 만들 수 있는 다양한 소스가 표시되며, 각 소스에는 연관된 기존 연결 수가 표시됩니다.

Adobe 애플리케이션 *카테고리 아래에서* Adobe Audience Manager **** 을 선택하여 화면 오른쪽에 정보 막대를 표시합니다. 정보 표시줄에는 선택한 소스에 대한 간단한 설명과 해당 설명서를 보거나 소스와 연결할 수 있는 옵션이 제공됩니다.

Adobe Audience Manager용 새 소스 커넥터를 만들려면 데이터 **추가를 클릭합니다**.

![](../../../../images/tutorials/create/aam/catalog.png)

대화 상자가 나타납니다. 연결 **을** 클릭하여 연결을 만듭니다.

![](../../../../images/tutorials/create/aam/connect_full.png)

Adobe Audience Manager과 소스 연결이 설정된 경우 Audience Manager 커넥터에 대한 *소스 활동* 페이지가 표시됩니다.

![](../../../../images/tutorials/create/aam/flow.png)

들어오는 Audience Manager 데이터를 일시 중지하려면 데이터 흐름 목록을 클릭하고 해당 *상태* 열을 오른쪽 *속성* 열에서 토글하여 일시 중지할 수 있습니다.

![](../../../../images/tutorials/create/aam/flow_disable.png)

## 다음 단계

Audience Manager 데이터 프롤이 활성화되면 들어오는 데이터가 실시간 고객 프로필로 자동으로 수집됩니다. 이제 이 수신 데이터를 활용하고 플랫폼 세그멘테이션 서비스를 사용하여 고객 세그먼트를 만들 수 있습니다. 자세한 내용은 다음 문서를 참조하십시오.

- [실시간 고객 프로필 개요](../../../../../profile/home.md)
- [세그멘테이션 서비스 개요](../../../../../segmentation/home.md)