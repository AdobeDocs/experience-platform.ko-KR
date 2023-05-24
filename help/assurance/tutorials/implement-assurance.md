---
title: Adobe Experience Platform Assurance 확장 구현
description: 이 안내서에서는 Adobe Experience Platform Assurance 확장을 구현하고 설치하는 방법을 설명합니다.
exl-id: b7bd1bb1-1606-4d00-97e0-c329c86d8ca4
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 3%

---

# Adobe Experience Platform Assurance 확장 구현

이 튜토리얼에서는 Mobile SDK에 Platform Assurance 확장을 설치하고 구현하는 방법을 설명합니다. Assurance 확장을 애플리케이션에 추가하는 방법에 대한 지침은 [Adobe Experience Platform Assurance 확장 개요](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

## 시작하기

Assurance 확장을 설치하고 구현하려면 다음 서비스에 액세스해야 합니다.

- 다음 [Adobe Experience Platform 데이터 수집 UI](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

## 모바일 속성을 만듭니다

>[!NOTE]
>
>모바일 속성이 이미 있는 경우 다음 단계로 진행할 수 있습니다.

데이터 수집 UI에서 **[!UICONTROL 태그]**. 조직에 속한 속성에 대한 정보가 포함된 모바일 및 웹 속성 목록이 나타납니다. 선택 **[!UICONTROL 새 속성]** 새 속성을 만듭니다.

![새 속성 버튼이 강조 표시되어 새 속성을 만들기 위해 선택한 항목을 보여 줍니다](./images/implement-assurance/create-new-property.png)

다음 **[!UICONTROL 속성 만들기]** 페이지가 나타납니다. 새 속성의 이름을 입력하고 를 선택합니다. **[!UICONTROL 모바일]** 를 플랫폼으로 사용하십시오. 세부 정보를 삽입한 후 다음을 선택합니다. **[!UICONTROL 저장]** 모바일 속성을 만듭니다.

>[!NOTE]
>
>모바일 속성의 **[!UICONTROL 개인 정보 보호]** 설정 **아님** 은 Assurance의 데이터 수집에 영향을 줍니다.

![[속성 생성] 페이지가 표시됩니다. 여기에 모바일 속성에 대한 정보를 삽입할 수 있습니다.](./images/implement-assurance/create-property.png)

## Assurance 확장 설치

Assurance 확장을 설치할 모바일 속성을 선택합니다.

![선택한 모바일 속성이 강조 표시된 태그 속성 페이지가 표시됩니다.](./images/implement-assurance/select-mobile-property.png)

다음 **모바일 속성 세부 정보** 페이지가 나타납니다. 선택 **[!UICONTROL 확장]** 를 클릭하여 현재 모바일 속성과 연결된 확장 목록을 표시합니다.

![모바일 속성 세부 사항 페이지가 표시됩니다. 최근 활동에 대한 정보가 표시됩니다. 확장 탭이 강조 표시됩니다.](./images/implement-assurance/tag-properties.png)

선택 **[!UICONTROL 카탈로그]** 를 클릭하여 mobile 속성에 추가할 수 있는 확장 목록을 확인합니다. 필터를 사용하여 **[!UICONTROL AEP 보증]** 확장 및 선택 **[!UICONTROL 설치]**.

![확장 카탈로그가 표시됩니다. Assurance 확장이 필터링되고 설치 버튼이 강조 표시된 상태로 표시됩니다.](./images/implement-assurance/assurance-extension.png)

## 다음 단계

이제 모바일 속성에 Assurance 확장을 설치했으므로 애플리케이션 내에서 Assurance를 사용할 수 있습니다. Assurance 확장을 애플리케이션에 추가하는 방법을 알아보려면 [Adobe Experience Platform Assurance 확장 개요](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app). Assurance 사용 방법을 알아보려면 [assurance 안내서 사용](./using-assurance.md).
