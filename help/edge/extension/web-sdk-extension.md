---
title: Adobe Experience Platform 웹 SDK 확장 개요
description: Adobe Experience Platform Launch용 Adobe Experience Platform Web SDK 익스텐션에 대한 자세한 내용
translation-type: tm+mt
source-git-commit: 0b9a92f006d1ec151a0bb11c10c607ea9362f729
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 53%

---


# Adobe Experience Platform 웹 SDK 확장 개요

Adobe Experience Platform 웹 SDK 익스텐션은 Adobe Experience Platform Edge 네트워크를 통해 웹 속성에서 Adobe Experience Cloud으로 데이터를 전송합니다. Adobe Experience Platform 웹 SDK 확장을 사용하면 데이터를 플랫폼으로 스트리밍하고 ID와 옵트인을 동기화하며 컨텍스트 데이터를 자동으로 수집할 수 있습니다.

## 확장 프로그램 구성

이 섹션에서는 Adobe Experience Platform 웹 SDK 확장을 구성할 때 사용할 수 있는 옵션에 대한 참조를 제공합니다.

Adobe Experience Platform 웹 SDK 익스텐션이 아직 설치되어 있지 않은 경우 속성을 열고 **[!UICONTROL 확장 > 카탈로그]**&#x200B;를 선택하고 Adobe Experience Platform 웹 SDK 확장 프로그램 위로 마우스를 가져간 다음 **[!UICONTROL 설치]**&#x200B;를 선택합니다.

확장을 구성하려면 **[!UICONTROL 확장]** 탭을 열고 확장자 위로 마우스를 가져간 다음 **[!UICONTROL 구성]**&#x200B;을 선택합니다.

![](./assets/ext-aep-config.png)

### 인스턴스 이름

Adobe Experience Platform 웹 SDK 익스텐션은 페이지에서 여러 인스턴스를 지원합니다. 이 확장은 단일 Adobe Experience Platform Launch 구성을 사용하여 여러 조직에 데이터를 전송하는 데 사용됩니다. **[!UICONTROL 이름]** 기본값은 합금입니다. 그러나 인스턴스 이름을 유효한 JavaScript 개체 이름으로 변경할 수 있습니다. Adobe Experience Platform 확장 기능을 사용하려면 각 인스턴스에 다른 **[!UICONTROL 구성 ID]**&#x200B;와 다른 **[!UICONTROL 조직 ID]**&#x200B;가 있어야 합니다.

## **[!UICONTROL 구성 ID]**

**[!UICONTROL 구성 ID]**&#x200B;는 Adobe Experience Platform에서 데이터를 라우팅해야 하는 위치와 서버에서 어떤 구성을 사용해야 하는지를 알리는 것입니다. Adobe Experience Platform 확장이 작동하는 데 필요합니다. 클라이언트 지원팀에 연락하여 구성 ID를 얻을 수 있습니다.


### **[!UICONTROL 조직 ID]**

**[!UICONTROL 조직 ID]**&#x200B;는 Adobe에서 데이터를 보내려는 조직입니다. 대부분의 경우 자동 채우기되는 기본값을 사용해야 합니다. 페이지에 인스턴스가 여러 개 있으면 데이터를 보낼 두 번째 조직의 값으로 이 인스턴스를 채웁니다.

### **[!UICONTROL Edge 도메인]**

**[!UICONTROL Edge 도메인]**&#x200B;은 Adobe Experience Platform 확장이 데이터를 보내고 받는 도메인입니다. 기본 타사 도메인은 프로덕션 트래픽에 자사 CNAME을 사용해야 합니다. 기본 타사 도메인은 개발 환경에서 작동하지만, 프로덕션 환경에는 적합하지 않습니다. 자사 CNAME을 설정하는 방법에 대한 지침은 [여기](https://docs.adobe.com/content/help/ko-KR/core-services/interface/ec-cookies/cookies-first-party.html)에 나와 있습니다.

### **[!UICONTROL 오류 사용]**

기본적으로 확장 프로그램에 오류가 있으면 콘솔에 오류가 기록됩니다. 제작 환경에서 오류를 숨기려면 **[!UICONTROL 오류 사용]** 확인란의 선택을 취소할 수 있습니다. Platform Launch에서 디버깅이 설정되어 있어도 오류가 인쇄됩니다.

### **[!UICONTROL 옵트인 활성화]**

**[!UICONTROL Enable Opt-in]**&#x200B;이(가) 활성화된 경우, 확장이 옵트인을 받을 때까지 히트를 보류할 수 있습니다. 이 확장은 옵트인 환경 설정을 지정하는 동작을 표시합니다.

### **[!UICONTROL ECID 마이그레이션 활성화]**

플랫폼 웹 SDK 확장 프로그램은 새 쿠키를 사용하여 ECID를 저장합니다. 이 설정을 사용하면 마이그레이션을 위해 새 쿠키와 이전 쿠키가 호환됩니다. ECID가 있는 기존 방문자가 없는 한 이 기능을 사용할 것을 적극 권장합니다.

### **[!UICONTROL 타사 쿠키 사용]**

Adobe Experience Platform은 쿠키를 항상 자사 도메인에 저장합니다. 이 옵션을 사용하면 자사 도메인의 쿠키뿐만 아니라 demdex.net에 설정된 타사 쿠키를 사용할 수 있습니다. 이 기능은 여러 도메인 간에 전환하는 사용자가 있을 때 유용합니다. 이 옵션을 선택하면 demdex.net 호출이 비활성화됩니다.

### **[!UICONTROL 컨텍스트]**

확장은 요청 컨텍스트에 대한 정보(예: URL 및 브라우저에 대한 세부 정보)를 자동으로 수집합니다. 특정 컨텍스트를 선택 취소하여 비활성화할 수 있습니다.

- **[!UICONTROL 웹]**  - url, 레퍼러 등 웹 페이지에 대한 세부 사항
- **[!UICONTROL 장치]**  - 화면 방향, 화면 높이 및 화면 폭과 같은 장치에 대한 세부 사항.
- **[!UICONTROL 환경]**  - 컴퓨팅 환경에 대한 정보(브라우저, 연결 등)
- **[!UICONTROL 위치]**  - 사용자 위치에 대한 제한된 정보

## 다음 단계

1. [작업 유형](action-types.md)을 설정합니다.
2. [데이터 요소 유형](data-element-types.md)을 설정합니다.
