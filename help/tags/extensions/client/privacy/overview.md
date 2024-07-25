---
title: Adobe 개인 정보 보호 확장 개요
description: Adobe Experience Platform의 Adobe 개인 정보 보호 태그 확장에 대해 알아봅니다.
exl-id: 8401861e-93ad-48eb-8796-b26ed8963c32
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 2%

---

# Adobe 개인 정보 보호 확장 개요

>[!NOTE]
>
>Adobe Experience Platform Launch은 Adobe Experience Platform의 데이터 수집 기술군으로 새롭게 브랜딩되었습니다. 그 결과 제품 설명서에 몇 가지 용어 변경 사항이 적용되었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../../term-updates.md)를 참조하십시오.

Adobe 개인 정보 보호 태그 확장을 사용하면 클라이언트측 장치에서 Adobe 솔루션으로 최종 사용자에게 할당된 사용자 ID를 수집 및 제거할 수 있습니다. 그런 다음 수집된 ID를 [Adobe Experience Platform Privacy Service](../../../../privacy-service/home.md)(으)로 전송하여 지원되는 Adobe Experience Cloud 애플리케이션에서 관련 개인의 개인 데이터에 액세스하거나 삭제할 수 있습니다.

이 안내서에서는 Experience Platform UI 또는 데이터 수집 UI에서 Adobe 개인 정보 보호 확장을 설치하고 구성하는 방법을 다룹니다.

>[!NOTE]
>
>태그를 사용하지 않고 이러한 기능을 설치하려면 원시 코드를 사용하여 구현하는 방법에 대한 단계를 [개인 정보 보호 JavaScript 라이브러리 개요](../../../../privacy-service/js-library.md)를 참조하십시오.

## 확장 설치 및 구성

왼쪽 탐색에서 **[!UICONTROL 확장]**&#x200B;을 선택한 다음 **[!UICONTROL 카탈로그]** 탭을 선택합니다. Adobe 개인 정보 보호 를 찾을 때까지 검색 창을 사용하여 사용 가능한 확장 목록의 범위를 좁힙니다. 계속하려면 **[!UICONTROL 설치]**&#x200B;를 선택하십시오.

![확장 설치](../../../images/extensions/client/privacy/install.png)

다음 화면에서는 확장에서 ID를 수집할 소스 및 솔루션을 구성할 수 있습니다. 확장 프로그램에 대해 지원되는 솔루션은 다음과 같습니다.

* Adobe Analytics (AA)
* Adobe Audience Manager (AAM)
* Adobe Target
* Adobe Experience Cloud ID 서비스(방문자 또는 ECID)
* Adobe Advertising Cloud(AdCloud)

하나 이상의 솔루션을 선택한 다음 **[!UICONTROL 업데이트]**&#x200B;를 선택합니다.

![솔루션 선택](../../../images/extensions/client/privacy/select-solutions.png)

선택한 솔루션을 기반으로 필요한 구성 매개 변수에 대한 입력을 표시하도록 화면이 업데이트됩니다.

![필요한 속성](../../../images/extensions/client/privacy/required-properties.png)

아래 드롭다운 메뉴를 사용하여 구성에 솔루션별 매개 변수를 추가할 수도 있습니다.

![선택적 속성](../../../images/extensions/client/privacy/optional-properties.png)

>[!NOTE]
>
>지원되는 각 솔루션에 대해 허용되는 구성 값에 대한 자세한 내용은 개인 정보 보호 JavaScript 라이브러리 개요의 [구성 매개 변수](../../../../privacy-service/js-library.md#config-params)에 대한 섹션을 참조하십시오.

선택한 솔루션에 대한 매개 변수를 모두 추가했으면 **[!UICONTROL 저장]**&#x200B;을 선택하여 구성을 저장합니다.

![선택적 속성](../../../images/extensions/client/privacy/save-config.png)

## 확장 사용 {#using}

Adobe 개인 정보 보호 확장은 특정 이벤트가 발생하고 조건이 충족될 때 [규칙](../../../ui/managing-resources/rules.md)에서 사용할 수 있는 세 가지 작업 유형을 제공합니다.

* **[!UICONTROL ID 검색]**: 사용자의 저장된 ID 정보를 검색합니다.
* **[!UICONTROL ID 제거]**: 사용자의 저장된 ID 정보가 제거됩니다.
* **[!UICONTROL ID 검색 후 제거]**: 사용자의 저장된 ID 정보를 검색한 후 제거합니다.

위의 각 작업에 대해 검색된 ID 데이터를 개체 매개 변수로 수락하고 처리하는 콜백 JavaScript 함수를 제공해야 합니다. 여기에서 이러한 ID를 저장하거나 표시하거나 필요에 따라 [Privacy Service API](../../../../privacy-service/api/overview.md)로 보낼 수 있습니다.

Adobe 개인 정보 보호 태그 확장을 사용할 때 데이터 요소 형태로 필요한 콜백 함수를 제공해야 합니다. 이 데이터 요소를 구성하는 방법에 대한 단계는 다음 섹션을 참조하십시오.

### ID를 처리할 데이터 요소 정의

왼쪽 탐색에서 **[!UICONTROL 데이터 요소]**&#x200B;를 선택한 후 **[!UICONTROL 데이터 요소 추가]**&#x200B;를 선택하여 새 데이터 요소를 만드는 프로세스를 시작하십시오. 구성 화면에 표시되면 확장에 대해 **[!UICONTROL 코어]**&#x200B;를 선택하고 데이터 요소 유형에 대해 **[!UICONTROL 사용자 지정 코드]**&#x200B;를 선택합니다. 오른쪽 패널에서 **[!UICONTROL 편집기 열기]**&#x200B;를 선택합니다.

![데이터 요소 유형 선택](../../../images/extensions/client/privacy/data-element-type.png)

표시되는 대화 상자에서 검색된 ID를 처리할 JavaScript 함수를 정의합니다. 콜백은 단일 개체 유형 인수(`ids`)를 허용해야 합니다. 그런 다음 함수는 원하는 대로 ID를 처리할 수 있으며, 추가 처리를 위해 사이트에서 전역적으로 사용할 수 있는 모든 변수 및 함수를 호출할 수도 있습니다.

>[!NOTE]
>
>콜백 함수가 처리할 `ids` 개체의 구조에 대한 자세한 내용은 개인 정보 보호 JavaScript 라이브러리 개요에 제공된 [코드 샘플](../../../../privacy-service/js-library.md#samples)을 참조하십시오.

완료되면 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

![콜백 함수 정의](../../../images/extensions/client/privacy/define-custom-code.png)

다른 이벤트에 대해 다른 콜백이 필요한 경우 다른 사용자 지정 코드 데이터 요소를 계속 만들 수 있습니다.

### 개인 정보 보호 작업을 사용하여 규칙 만들기

검색된 ID를 처리하도록 콜백 데이터 요소를 구성한 후에는 필요한 다른 조건과 함께 사이트에서 특정 이벤트가 발생할 때마다 Adobe 개인 정보 보호 확장을 호출하는 규칙을 만들 수 있습니다.

규칙에 대한 작업을 구성할 때 확장에 대해 **[!UICONTROL Adobe 개인 정보]**&#x200B;을(를) 선택하십시오. 작업 유형에 대해 확장에서 제공하는 [3개의 함수](#using) 중 하나를 선택하십시오.

![작업 유형 선택](../../../images/extensions/client/privacy/action-type.png)

오른쪽 패널은 작업의 콜백 역할을 할 데이터 요소를 선택하라는 메시지를 표시합니다. 데이터베이스 아이콘(![데이터베이스 아이콘](/help/images/icons/database.png))을 선택하고 목록에서 이전에 만든 데이터 요소를 선택합니다. 계속하려면 **[!UICONTROL 변경 내용 유지]**&#x200B;를 선택하십시오.

![데이터 요소 선택](../../../images/extensions/client/privacy/add-data-element.png)

여기에서 필요한 이벤트 및 조건에 따라 Adobe 개인 정보 보호 작업이 실행되도록 규칙 구성을 계속할 수 있습니다. 만족하면 **[!UICONTROL 저장]**&#x200B;을 선택하세요.

![규칙 저장](../../../images/extensions/client/privacy/save-rule.png)

이제 테스트를 위해 웹 사이트에 빌드로 배포할 규칙을 라이브러리에 추가할 수 있습니다. 자세한 내용은 [태그 게시 흐름](../../../ui/publishing/overview.md)에 대한 개요를 참조하십시오.

## 확장 비활성화 또는 제거

확장을 설치한 후에 확장을 비활성화하거나 삭제할 수 있습니다. 설치된 확장의 Adobe 개인 정보 보호 카드에서 **[!UICONTROL 구성]**&#x200B;을 선택한 다음 **[!UICONTROL 비활성화]** 또는 **[!UICONTROL 제거]**&#x200B;를 선택합니다.

## 다음 단계

이 안내서에서는 UI에서 Adobe 개인 정보 보호 태그 확장 사용에 대해 다룹니다. 원시 코드를 사용하여 사용하는 방법에 대한 예를 포함하여 확장에서 제공하는 기능에 대한 자세한 내용은 Privacy Service 설명서의 [개인 정보 보호 JavaScript 라이브러리 개요](../../../../privacy-service/js-library.md)를 참조하십시오.
