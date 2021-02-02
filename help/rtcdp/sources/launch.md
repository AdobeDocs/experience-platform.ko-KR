---
keywords: 웹 태그 시작;웹 태그 시작;웹 사이트 태그;웹 태그;시작;시작;Launch web tags launch;web tags launch;web tags launch;web tags launch;launch;launch;launch;launch
title: 자습서 Adobe 시작을 사용하여 웹 사이트 태그 구현
seo-title: Adobe 시작을 사용하여 웹 사이트 태그 구현
description: Adobe 시작을 사용하여 Adobe Experience Platform에서 웹 사이트 태그 구현
seo-description: Adobe 시작을 사용하여 Adobe Experience Platform에서 웹 사이트 태그 구현
translation-type: tm+mt
source-git-commit: 00010d38a5d05800aeac9af8505093fee3593b45
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 8%

---


# 자습서:Adobe 시작을 사용하여 웹 사이트 태그 구현

이 자습서에서는 Adobe Launch를 사용하여 웹 사이트 태그를 구현하여 데이터를 Adobe Experience Platform으로 보내는 방법을 설명합니다.

## 전제 조건

* 필요한 스키마 및 데이터 집합이 [!DNL Platform]에서 만들어집니다.
* 필요한 구성이 Experience Edge에 배포되었으며 일치하는 구성 ID 및 Edge 도메인이 있습니다.
* 회사 CMS는 Platform으로 전송하는 데 필요한 데이터가 포함된 각 페이지에 JavaScript 개체를 제공하도록 이미 구성되었습니다.

## 단계

이 자습서에는 다음 단계가 포함됩니다.

1. Adobe Experience Platform [!DNL Web SDK] 확장을 설치합니다.
1. 전송할 데이터를 [!DNL Launch]에 알리는 규칙을 만듭니다.
1. 라이브러리에서 확장 기능과 규칙을 번들로 묶습니다.

## Adobe Experience Platform [!DNL Web SDK] 확장 설치

먼저 Adobe Experience Platform [!DNL Web SDK] 확장을 설치합니다.

1. [!DNL Launch]에서 **[!UICONTROL Extensions]** 탭을 엽니다.

   ![image](assets/launch-overview.png)

1. Launch Extension Catalog에서 Adobe Experience Platform Web SDK 익스텐션을 선택합니다.
구성 화면이 열립니다.

   ![이미지](assets/launch-extension-install.png)

   자세한 내용은 [!DNL Launch] 설명서의 [확장](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html)을 참조하십시오.

1. 확장을 구성합니다.

   지금 필요한 유일한 설정은 다음과 같습니다.

   * **구성 ID:** Adobe 담당자로부터 받은 구성 ID를 지정합니다.
   * **Edge** Domain: Adobe 담당자로부터 받은 Edge Domain을 지정합니다.

1. **[!UICONTROL 저장]**&#x200B;을 선택하고 다음 단계로 이동합니다.

## 보낼 데이터를 [!DNL Launch]에 알려주는 규칙을 만듭니다.

그런 다음 Adobe Experience Platform으로 보낼 데이터와 보낼 시기를 [!DNL Launch]에 알도록 규칙을 만듭니다.

1. **[!UICONTROL 규칙]** 탭에서 [!DNL Launch] 라이브러리가 로드될 때 웹 사이트의 새 각 페이지에서 트리거되는 이벤트를 구성합니다.

   ![이미지](assets/launch-make-a-rule.png)

1. 작업 추가.

   동작을 구성하려면 데이터 레이어를 찾을 위치를 [!DNL Launch]에 알려주십시오. 데이터 레이어는 페이지에 존재하는 JavaScript 개체이며, 웹 페이지를 렌더링하는 동일한 CMS에서 제공됩니다. 데이터 객체에 대한 JavaScript 경로를 제공합니다.

   ![이미지](assets/launch-add-aep-action.png)

   전송하는 데이터 개체는 구성 ID에 연결된 데이터 세트에 의해 사용되는 스키마에 대한 유효성 검사를 전달하는 유효한 XDM이어야 합니다.

1. **[!UICONTROL 변경 내용 유지]**&#x200B;를 선택합니다.

자세한 내용은 [!DNL Launch] 설명서의 [규칙](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/rules.html)을 참조하십시오.

## 라이브러리에 확장 및 규칙 번들로 제공

그런 다음 [확장](https://docs.adobe.com/content/help/en/launch/using/reference/publish/overview.html)과 새 규칙을 라이브러리에 함께 번들하고 개발 환경에서 이러한 변경 사항을 테스트합니다.

![이미지](assets/launch-add-changes-to-library.png)

테스트를 완료한 후 워크플로우를 통해 라이브러리를 홍보하여 프로덕션 사이트에 배포할 수 있습니다. 이제 데이터는 각 개인 사용자에서 Adobe Experience Platform으로 전송됩니다.

![이미지](assets/launch-promote-library.png)

자세한 내용은 [!DNL Launch] 설명서의 [라이브러리](https://docs.adobe.com/content/help/ko-KR/launch/using/reference/publish/libraries.html)를 참조하십시오.