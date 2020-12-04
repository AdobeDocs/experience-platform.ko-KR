---
keywords: launch web tags;web tags launch;website tags;web tags;launch;Launch
title: 자습서 Adobe 시작을 사용하여 웹 사이트 태그 구현
seo-title: Adobe 시작을 사용하여 웹 사이트 태그 구현
description: Adobe 론치를 사용하여 Adobe Experience Platform에서 웹 사이트 태그 구현
seo-description: Adobe 론치를 사용하여 Adobe Experience Platform에서 웹 사이트 태그 구현
translation-type: tm+mt
source-git-commit: 54df4778a025811504801306120bda78e04281c1
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 8%

---


# 자습서:Adobe 시작을 사용하여 웹 사이트 태그 구현

이 자습서에서는 Adobe 시작을 사용하여 웹 사이트 태그를 구현하여 데이터를 Adobe Experience Platform으로 전송하는 방법을 설명합니다.

## 전제 조건

* 필요한 스키마와 데이터 집합이 [!DNL Platform]
* 필요한 구성이 Experience Edge에 배포되었으며 일치하는 구성 ID와 Edge 도메인이 있습니다.
* 회사 CMS는 플랫폼용으로 전송하는 데 필요한 데이터가 포함된 각 페이지에 JavaScript 개체를 전달하도록 이미 구성되었습니다.

## 단계

이 자습서에는 다음 단계가 포함되어 있습니다.

1. Adobe Experience Platform [!DNL Web SDK] 익스텐션을 설치합니다.
1. 전송할 데이터를 [!DNL Launch] 알려주는 규칙을 만듭니다.
1. 라이브러리의 확장명과 규칙을 번들로 묶습니다.

## Adobe Experience Platform 확장 [!DNL Web SDK] 설치

먼저 Adobe Experience Platform [!DNL Web SDK] 익스텐션을 설치합니다.

1. In [!DNL Launch], open the **[!UICONTROL Extensions]** tab.

   ![image](assets/launch-overview.png)

1. Launch Extension Catalog에서 Adobe Experience Platform 웹 SDK 익스텐션을 선택합니다. 구성 화면이 열립니다.

   ![image](assets/launch-extension-install.png)

   자세한 내용은 설명서의 [익스텐션](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html) 을 [!DNL Launch] 참조하십시오.

1. 확장 기능을 구성합니다.

   지금 필요한 유일한 설정은 다음과 같습니다.

   * **구성 ID:** Adobe 담당자로부터 받은 구성 ID를 지정합니다.
   * **Edge Domain:** Adobe 담당자로부터 받은 Edge 도메인을 지정합니다.

1. 저장 **[!UICONTROL 을]** 클릭하고 다음 단계로 계속 진행합니다.

## 전송할 데이터를 알려주는 규칙 [!DNL Launch] 만들기

그런 다음 Adobe Experience Platform으로 보낼 데이터와 보낼 시기를 알려주는 규칙을 만듭니다. [!DNL Launch]

1. [ **[!UICONTROL 규칙]** ] 탭에서 [!DNL Launch] 라이브러리가 로드될 때 웹 사이트의 새로운 각 페이지에서 트리거되는 이벤트를 구성합니다.

   ![image](assets/launch-make-a-rule.png)

1. 작업 추가.

   동작을 구성하려면 데이터 레이어 [!DNL Launch] 의 위치를 알려주십시오. 데이터 레이어는 페이지에 존재하는 JavaScript 개체로서, 웹 페이지를 렌더링하는 동일한 CMS에서 제공됩니다. 데이터 개체에 JavaScript 경로를 제공합니다.

   ![image](assets/launch-add-aep-action.png)

   전송한 데이터 개체는 올바른 XDM이어야 합니다. 이 XDM은 구성 ID에 연결된 데이터 세트에 사용되는 스키마에 대해 유효성 검사를 전달합니다.

1. Click **[!UICONTROL Keep Changes]**.

자세한 내용은 설명서의 [규칙](https://docs.adobe.com/content/help/ko-KR/launch/using/reference/manage-resources/rules.html) 을 [!DNL Launch] 참조하십시오.

## 라이브러리의 확장 및 규칙 번들

그런 다음 확장 [기능과 새로운 규칙을 라이브러리에 함께](https://docs.adobe.com/content/help/ko-KR/launch/using/reference/publish/overview.html) 번들로 구성하여 개발 환경에서 이러한 변경 사항을 테스트할 수 있습니다.

![image](assets/launch-add-changes-to-library.png)

테스트를 완료한 후 워크플로우를 통해 라이브러리를 홍보하여 프로덕션 사이트에 배포할 수 있습니다. 이제 개별 사용자마다 데이터가 Adobe Experience Platform으로 전송됩니다.

![image](assets/launch-promote-library.png)

자세한 내용은 설명서의 [라이브러리](https://docs.adobe.com/content/help/ko-KR/launch/using/reference/publish/libraries.html) 를 [!DNL Launch] 참조하십시오.