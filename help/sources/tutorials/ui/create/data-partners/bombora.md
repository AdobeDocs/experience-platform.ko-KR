---
title: Ui를 사용하여 Bombora 인텐트를 Experience Platform에 연결
description: Bombora Intent를 Experience Platform에 연결하는 방법 알아보기
hide: true
hidefromtoc: true
exl-id: 76a4fed5-b2d5-46d5-9245-b52792a7d323
source-git-commit: 911aad600dd2618ba98d2ccee737aaedea4f2735
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 36%

---

# UI를 사용하여 [!DNL Bombora Intent]을(를) Experience Platform에 연결

사용자 인터페이스를 사용하여 [!DNL Bombora Intent] 계정을 Adobe Experience Platform에 연결하는 방법에 대해 알아보려면 이 안내서를 참조하십시오.

## 시작하기

이 자습서에서는 Experience Platform의 다음 구성 요소를 이해하고 있어야 합니다.

* [Real-Time CDP B2B edition](../../../../../rtcdp/b2b-overview.md): Real-Time CDP B2B edition은 B2B 서비스 모델에서 작동하는 마케터용으로 특별히 빌드되었습니다. 여러 소스의 데이터를 함께 가져와서 사람 및 계정 프로필의 단일 보기로 결합합니다. 마케터는 이 통합 데이터를 통해 특정 대상자를 정확하게 타겟팅하고 사용 가능한 모든 채널에서 해당 대상자를 참여시킬 수 있습니다.
* [소스](../../../../home.md): Experience Platform을 사용하면 Experience Platform 서비스를 사용하여 들어오는 데이터를 구조화하고 레이블을 지정하고 향상시키는 기능을 제공하는 동시에 다양한 소스에서 데이터를 수집할 수 있습니다.
* [샌드박스](../../../../../sandboxes/home.md): Experience Platform은 단일 Experience Platform 인스턴스를 별도의 가상 환경으로 분할하여 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 가상 샌드박스를 제공합니다.

## 소스 카탈로그 탐색

Platform UI의 왼쪽 탐색에서 **[!UICONTROL 소스]**&#x200B;를 선택하여 [!UICONTROL 소스] 작업 영역에 액세스합니다. 화면 왼쪽에 있는 카탈로그에서 적절한 카테고리를 선택할 수 있습니다. 또는 검색 옵션을 사용하여 작업할 특정 소스를 찾을 수 있습니다.

*[!UICONTROL B2B]* 범주에서 **[!DNL Bombora Intent]**&#x200B;을(를) 선택한 다음 **[!UICONTROL 설정]**&#x200B;을(를) 선택합니다.

>[!TIP]
>
>지정된 소스에 아직 인증된 계정이 없는 경우 소스 카탈로그의 소스에 **[!UICONTROL 설정]** 옵션이 표시됩니다. 인증된 계정이 있으면 이 옵션이 **[!UICONTROL 데이터 추가]**(으)로 변경됩니다.



## 기존 계정 사용 {#existing}

## 새 계정 만들기 {#create}

## 데이터 흐름 세부 정보 제공 {#provide-dataflow-details}

>[!CONTEXTUALHELP]
>id="platform_sources_bombora_domain"
>title="도메인 소스"
>abstract="Adobe는 XDM accountOrganization.website를 사용하지만 일부 고객은 각 웹 사이트에 대해 사용자 정의 필드를 사용할 수 있습니다. 따라서 도메인 소스가 Bombora 계정 기록과 Experience Platform 계정을 일치시킬 수 있는 도메인/웹 사이트 필드인지 확인해야 합니다."

## 데이터 흐름 예약 {#schedule-dataflow}

>[!CONTEXTUALHELP]
>id="platform_sources_bombora_schedule"
>title="데이터 흐름 일정 예약"
>abstract="Bombora는 매주 월요일 오전 5시(UTC)에 데이터를 전송합니다. 따라서 데이터 수집 시작 시간을 5시(UTC) 이후로 설정해야 합니다. 또한 Bombora가 파일을 Adobe에 전송할 때 일정을 변경할 수 있으므로, 데이터 수집 시간을 Bombora에 확인해야 합니다."


## 데이터 흐름 검토 {#review-dataflow}
