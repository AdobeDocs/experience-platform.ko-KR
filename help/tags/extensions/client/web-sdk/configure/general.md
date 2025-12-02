---
title: SDK 인스턴스 구성 설정
description: 웹 SDK 인스턴스에 대한 일반 설정을 구성합니다.
source-git-commit: 09799847c61d82ed5b7cd372d92aa436697d54f3
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 2%

---

# SDK 인스턴스 구성 설정

이 구성 섹션은 웹 SDK 인스턴스 이름, 적용되는 IMS 조직 및 데이터를 보낼 위치를 제어합니다. 기본적으로 인스턴스 이름은 `alloy`입니다.

1. Adobe ID 자격 증명을 사용하여 [experience.adobe.com](https://experience.adobe.com)에 로그인합니다.
1. **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**(으)로 이동합니다.
1. 원하는 태그 속성을 선택합니다.
1. **[!UICONTROL Extensions]**(으)로 이동한 다음 **[!UICONTROL Configure]** 카드에서 [!UICONTROL Adobe Experience Platform Web SDK]을(를) 선택합니다.
1. 확장된 [!UICONTROL SDK instances] 아코디언 바로 아래에서 인스턴스 이름을 찾습니다.

![태그 UI에서 웹 SDK 태그 확장의 일반 설정을 보여 주는 이미지](../assets/web-sdk-ext-general.png)

다음 옵션을 사용할 수 있습니다.

## [!UICONTROL Name]

Adobe Experience Platform 웹 SDK 태그 확장은 페이지에서 여러 인스턴스를 지원합니다. 이 이름은 웹 SDK 태그 라이브러리를 중복하지 않고도 여러 조직에 데이터를 전송하는 데 사용됩니다. 인스턴스 이름을 유효한 JavaScript 개체 이름으로 변경할 수 있습니다.

## [!UICONTROL IMS organization ID]

Adobe에 데이터를 전송할 조직의 ID입니다. 대부분의 경우 자동으로 채워진 기본값을 사용합니다. 페이지에 인스턴스가 여러 개 있으면 이 필드를 데이터를 보낼 두 번째 조직의 값으로 채웁니다.

## [!UICONTROL Edge domain]

확장에서 데이터를 보내고 받는 도메인입니다. Adobe 기본값인 `edge.adobedc.net`은(는) 작동하지만, 대부분의 경우 자사 도메인을 사용하는 것이 좋습니다. 데이터 수집에 적합한 자사 도메인을 설정하는 방법에 대한 지침은 [Adobe 관리 인증서 프로그램](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/adobe-managed-cert)을 참조하세요. 이 값을 설정하는 방법에 대한 지침은 JavaScript 라이브러리 설명서에서 [`edgeDomain`](/help/collection/js/commands/configure/edgedomain.md)을(를) 참조하십시오.
