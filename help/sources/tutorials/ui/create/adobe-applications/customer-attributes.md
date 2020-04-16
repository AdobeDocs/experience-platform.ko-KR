---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: UI에서 고객 속성 소스 커넥터 만들기
topic: overview
translation-type: tm+mt
source-git-commit: f09ff4d1b159a6989868c5cfc35b361cfb640a99

---


# UI에서 고객 속성 소스 커넥터 만들기

이 자습서에서는 고객 속성 프로필 데이터를 Adobe Experience Platform으로 수집하기 위해 UI에서 소스 커넥터를 만드는 단계를 제공합니다. 고객 속성에 대한 자세한 내용은 [개요 문서를](https://docs.adobe.com/content/help/ko-KR/core-services/interface/customer-attributes/attributes.html)참조하십시오.

## 소스 연결 만들기

Adobe Experience <a href="https://platform.adobe.com" target="_blank">Platform에</a> 로그인한 다음 **왼쪽 탐색** 막대에서 소스를 선택하여 소스 작업 영역에 액세스합니다. [ *카탈로그* ] 화면에는 인바운드 연결을 만들 수 있는 사용 가능한 소스가 표시되며 각 소스에는 연결된 기존 연결 수가 표시됩니다. [고객 속성] 옵션을 **선택한** 다음 [연결] **소스를**&#x200B;클릭합니다. 연결이 설정될 때까지 잠시 기다려 주십시오. 연결이 성공적으로 이루어지면 리디렉션됩니다.

>[!NOTE] 고객 속성 프로필 데이터에 대한 소스 커넥터를 이미 설정한 경우 소스와 연결할 수 없습니다.

![](../../../../images/tutorials/create/customer-attributes/CA-sources_catalog.png)

소스 *활동* 화면에는 고객 속성 프로필 데이터에 대해 이전에 설정한 모든 연결이 나열되며 데이터 **선택을 클릭하여 새 연결을 만들 수**&#x200B;있습니다.

>[!NOTE] 서로 다른 데이터를 가져오기 위해 소스에 대한 여러 인바운드 연결을 만들 수 있습니다.

![](../../../../images/tutorials/create/customer-attributes/CA-source_activity.png)

사용 가능한 고객 속성 프로필 데이터 집합 목록에서 플랫폼으로 가져올 항목을 선택하고 다음을 **클릭합니다**.

>[!NOTE] 고객 속성 소스 연결당 하나의 데이터 세트만 선택할 수 있습니다.

![](../../../../images/tutorials/create/customer-attributes/CA-select_data.png)

검토 *단계가* 표시되어 새로 인바운드 연결을 만들기 전에 검토할 수 있습니다. 연결 세부 사항은 다음을 포함하여 범주별로 그룹화됩니다.

* *소스 세부 정보*:소스 연결 유형과 선택한 소스 데이터를 표시합니다.
* *타겟 세부 사항*:다른 소스 커넥터를 만들 때 이 컨테이너는 데이터 집합이 준수하는 스키마를 포함하여 소스 데이터가 인제스트하는 데이터 집합을 표시합니다. 고객 속성 프로필 데이터는 자동으로 매핑되고 실시간 고객 프로파일에 수집됩니다.

![](../../../../images/tutorials/create/customer-attributes/CA-review.png)

## 다음 단계

연결이 만들어지면 들어오는 데이터를 포함하도록 대상 스키마와 데이터 세트가 자동으로 생성됩니다. 초기 수집이 완료되면 고객 속성 프로필 데이터를 실시간 고객 프로필 및 세그멘테이션 서비스와 같은 다운스트림 플랫폼 서비스에서 사용할 수 있습니다. 자세한 내용은 다음 문서를 참조하십시오.

* [실시간 고객 프로필 개요](../../../../../profile/home.md)
* [세그멘테이션 서비스 개요](../../../../../segmentation/home.md)
