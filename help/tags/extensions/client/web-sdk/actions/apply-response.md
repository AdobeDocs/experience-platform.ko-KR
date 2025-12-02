---
title: 응답 적용
description: Edge Network의 응답을 기반으로 작업을 수행합니다.
source-git-commit: f87e6a0e969aa0924656cdb2ea56aa79d2d7c841
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---

# 응답 적용

**[!UICONTROL Apply response]** 작업 유형을 사용하면 Edge Network의 응답을 기반으로 다양한 작업을 수행할 수 있습니다. 이 작업 유형은 일반적으로 서버가 Edge Network을 처음 호출한 후 해당 호출에서 응답을 가져와 브라우저에서 웹 SDK을 초기화하는 하이브리드 배포에서 사용됩니다. 이 작업 유형을 사용하면 하이브리드 개인화 사용 사례에 대한 클라이언트 로드 시간을 줄일 수 있습니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL Rules]**(으)로 이동한 다음 원하는 규칙을 선택합니다.
1. [!UICONTROL Actions]에서 기존 작업을 선택하거나 작업을 만듭니다.
1. [!UICONTROL Extension] 드롭다운 필드를 **[!UICONTROL Adobe Experience Platform Web SDK]**(으)로 설정한 다음 [!UICONTROL Action type]을(를) **[!UICONTROL Apply response]**(으)로 설정합니다.

![응답 적용 작업 유형을 표시하는 Experience Platform 사용자 인터페이스의 이미지](../assets/apply-response.png)

## 사용 사례

* **데이터 수집과 개인화 간 수동 분할**: 렌더링 결정이 [(으)로 설정된 상태에서 ](send-event.md)이벤트 보내기`false` 작업을 트리거한 다음 &#39;이벤트 보내기 완료&#39; 규칙이 약속을 catch할 수 있습니다. 이 규칙 내의 첫 번째 작업은 &#39;응답 적용&#39;이 될 수 있습니다. 이 워크플로우를 사용하면 조직의 자체 코드가 다른 작업을 완료할 때까지 DOM 조작을 지연할 수 있습니다.
* **웹 SDK 외부에서 받은 Edge 응답**: 다른 라이브러리를 사용하여 Edge Network과 통신하는 경우 이 작업을 사용하여 웹 SDK에서 Edge Network의 응답을 계속 처리하도록 할 수 있습니다.

## 사용 가능한 필드

이 작업 유형은 다음 구성 옵션을 지원합니다.

* **[!UICONTROL Instance]**: 작업이 적용되는 SDK 인스턴스입니다. 구현에서 단일 SDK 인스턴스를 사용하는 경우 이 드롭다운 메뉴가 비활성화됩니다.
* **[!UICONTROL Response headers]**: Edge Network 서버 호출에서 반환된 헤더 키 및 값이 포함된 개체를 반환하는 데이터 요소를 선택합니다.
* **[!UICONTROL Response body]**: Edge Network 응답에서 제공한 JSON 페이로드가 포함된 개체를 반환하는 데이터 요소를 선택합니다.
* **[!UICONTROL Render visual personalization decisions]**: 이 옵션을 사용하면 Edge Network에서 제공하는 개인화 콘텐츠를 자동으로 렌더링하고 깜박임을 방지하기 위해 콘텐츠를 미리 숨길 수 있습니다.
