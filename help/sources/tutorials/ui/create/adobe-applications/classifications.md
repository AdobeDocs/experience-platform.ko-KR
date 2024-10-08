---
description: UI에서 Adobe Analytics 소스 커넥터를 만들어 분류 데이터를 Adobe Experience Platform으로 가져오는 방법을 알아봅니다.
title: UI에서 분류 데이터에 대한 Adobe Analytics Source 연결 만들기
exl-id: d606720d-f1ca-47cc-919b-643a8fc61e07
source-git-commit: 02b5c5f963c21247adbb1d13114f92b22f8758de
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 0%

---

# UI에서 분류 데이터에 대한 Adobe Analytics 소스 연결 만들기

>[!TIP]
>
>기본적으로 Adobe Analytics 분류 데이터는 매주 업데이트됩니다. 분류 데이터에 대한 데이터 수집은 데이터 흐름의 초기 설정 후 7일 후에 처리됩니다. 첫 번째 로드는 전체 데이터를 수집하고 이어지는 주별 수집은 증분 데이터를 실행합니다.

사용자 인터페이스를 통해 Adobe Analytics 분류 데이터를 Adobe Experience Platform으로 수집하는 방법에 대한 절차를 알려면 이 자습서 를 참조하십시오.

## 시작하기

이 자습서에서는 Adobe Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [[!DNL Experience Data Model (XDM)] 시스템](../../../../../xdm/home.md): Experience Platform이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): 여러 원본의 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
* [[!DNL Sandboxes]](../../../../../sandboxes/home.md): Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 플랫폼 인스턴스를 별도의 가상 환경으로 분할하는 가상 샌드박스를 제공합니다.

Analytics 분류 소스 커넥터를 사용하려면 데이터를 Adobe Analytics의 새 분류 인프라로 마이그레이션해야 합니다. 데이터의 마이그레이션 상태를 확인하려면 Adobe 계정 팀에 문의하십시오.

## 분류 선택

Experience Platform UI의 왼쪽 탐색에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 [!UICONTROL 소스] 작업 영역에 액세스합니다. 화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

*Adobe 응용 프로그램* 범주에서 **[!UICONTROL Adobe Analytics]**&#x200B;을 선택한 다음 **[!UICONTROL 설정]**&#x200B;을 선택합니다.

>[!TIP]
>
>인증된 계정이 없는 경우 소스 카탈로그의 소스에 **[!UICONTROL 설정]** 옵션이 표시됩니다. 계정이 인증되면 옵션이 **[!UICONTROL 데이터 추가]**(으)로 변경됩니다.

![Adobe Analytics 원본이 선택된 Experience Platform UI의 원본 카탈로그입니다.](../../../../images/tutorials/create/classifications/catalog.png)

그런 다음 [!UICONTROL Experience Platform]을(를) 선택한 다음 수집하려는 분류 데이터 세트를 선택합니다.

최대 30개의 다양한 분류 데이터 세트를 선택하여 Experience Platform에 포함시킬 수 있습니다. 선택하는 모든 데이터 세트가 오른쪽 레일에 표시됩니다. 완료되면 [!UICONTROL 다음]을(를) 선택하여 계속하십시오.

![여러 분류 데이터 세트가 있는 분류 페이지입니다.](../../../../images/tutorials/create/classifications/select.png)

## 분류 검토

선택한 분류 데이터 세트를 만들기 전에 검토할 수 있는 **[!UICONTROL 검토]** 단계가 나타납니다. 세부 사항은 다음 범주 내에서 그룹화됩니다.

* **[!UICONTROL 연결]**: 원본 플랫폼과 연결 상태를 표시합니다.
* **[!UICONTROL 데이터 형식]**: 선택한 분류의 수를 표시합니다.
* **[!UICONTROL 예약]**: 분류 데이터의 동기화 빈도를 표시합니다. **참고**: 분류 데이터는 매주 업데이트됩니다.

데이터 흐름을 검토한 후 **[!UICONTROL 완료]**&#x200B;를 클릭하고 데이터 흐름이 만들어지도록 잠시 기다립니다.

![Adobe Analytics 분류 데이터를 검토하는 페이지입니다.](../../../../images/tutorials/create/classifications/review.png)

## 다음 단계

이 자습서에 따라 분류 데이터를 Experience Platform 상태로 가져오는 Analytics 분류 sata 커넥터를 만들었습니다. [!DNL Analytics] 및 분류 데이터에 대한 자세한 내용은 다음 문서를 참조하십시오.

* [Adobe Analytics 소스 커넥터 개요](../../../../connectors/adobe-applications/analytics.md)
* [UI에서 보고서 세트 데이터에 대한 Analytics 소스 연결 만들기](./analytics.md)
* [분류 정보](https://experienceleague.adobe.com/docs/analytics/components/classifications/c-classifications.html)
