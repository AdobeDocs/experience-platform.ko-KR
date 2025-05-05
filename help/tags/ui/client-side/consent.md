---
title: JavaScript 태그를 배포하여 고객 동의 관리
description: Adobe Experience Platform의 다양한 Adobe 솔루션에 대한 고객 옵트인 및 옵트아웃 신호를 관리하는 방법을 알아봅니다.
exl-id: 7762c42f-71c8-4f29-a96b-c6c04b838a91
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 79%

---

# JavaScript 태그를 배포하여 고객 동의 관리

>[!NOTE]
>
>Adobe Experience Platform Launch는 Adobe Experience Platform의 데이터 수집 기술로 새롭게 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](../../term-updates.md)를 참조하십시오.

GDPR(일반 데이터 보호 규정)과 같은 법적 개인 정보 보호 규정에 따라 회사는 사용자에 대한 동의를 관리할 수 있어야 합니다. 주어진 방문자에 대해 Adobe 솔루션을 실행하려면 Adobe 고객이 방문자에게 옵트인하도록 요청할 수 있습니다. 방문자는 자신의 옵트인 및 옵트아웃 상태를 관리할 수 있어야 합니다.

Adobe Experience Cloud 고객은 이러한 요구 사항에 대한 다양한 구현이 필요합니다. 일부는 엔터프라이즈급 동의 관리자를 사용하고, 그 외에는 직접 구축합니다.

Adobe Experience Platform 확장 개발자는 확장 및 규칙 빌더를 사용하여 옵트인 및 옵트아웃 솔루션을 정의합니다.

이 문서에는 동의를 얻을 때까지 Adobe 태그가 실행되지 않도록 하는 방법에 대한 정보를 제공합니다.

## Advertising Cloud

Adobe Experience Platform에서 [!DNL Advertising Cloud]을(를) 자동으로 실행하지 않습니다. [!DNL Advertising Cloud]는 규칙 작업에 명시적으로 지시한 경우에만 실행됩니다. 규칙 조건을 사용하여 언제 및 무엇을 실행할지 결정합니다. 예를 들어 쿠키를 사용하여 옵트인 상태를 결정하려면 데이터 요소를 설정하여 해당 쿠키를 읽은 후 규칙의 조건으로 사용하여 변환 추적 작업을 언제 실행할지 결정합니다.

동의 관리자(예: OneTrust)와 통합하면 고객에 대한 동의 쿠키를 설정 및 추적할 수 있으며, 이를 규칙 빌더에서 사용할 수 있습니다.

## Analytics

[!DNL Analytics] 확장의 구성 설정에 있는 Link Tracking 섹션에서 다음을 선택하지 *않았는지* 확인합니다.

* 다운로드 링크 추적
* 아웃바운드 링크 추적

이러한 설정을 선택하지 않으면 Experience Platform에서 [!DNL Adobe Analytics]을(를) 자동으로 실행하지 않습니다. [!DNL Analytics]는 규칙 작업에 명시적으로 지시한 경우에만 실행됩니다. 규칙 조건을 사용하여 언제 및 무엇을 실행할지 결정합니다. 예를 들어 쿠키를 사용하여 옵트인 상태를 결정하려면 데이터 요소를 설정하여 해당 쿠키를 읽은 후 규칙의 조건으로 사용하여 비콘 보내기 작업을 언제 실행할지 결정합니다.

별도로 동의 관리 플랫폼과 함께 [Adobe 옵트인 개체](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=ko)를 사용하여 이 태그의 실행을 제어할 수 있습니다.

동의 관리자(예: OneTrust)와 통합하면 고객에 대한 동의 쿠키를 설정 및 추적할 수 있으며, 이를 규칙 빌더에서 사용할 수 있습니다.

## Audience Manager

현재 DIL은 고객 페이지에 배치되면 자동으로 실행되도록 설정되어 있습니다. 동의 관리 플랫폼과 함께 [Adobe 옵트인 개체](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=ko)를 사용하여 이 태그의 실행을 제어하십시오.

[!DNL Adobe]는 [!DNL Analytics] 내에서 서버측 전달을 사용할 것을 권장합니다.

## Experience Cloud ID

현재 [!DNL Experience Cloud ID]는 고객 페이지에 배치되면 자동으로 실행됩니다. 

동의 관리 플랫폼과 함께 [Adobe 옵트인 개체](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=ko)를 사용하여 이 태그의 실행을 제어하십시오.

## Target

Adobe Experience Platform에서 [!DNL Target]을(를) 자동으로 실행하지 않습니다. [!DNL Target]는 규칙 작업에 명시적으로 지시한 경우에만 실행됩니다. 규칙 조건을 사용하여 언제 및 무엇을 실행할지 결정합니다. 예를 들어 쿠키를 사용하여 옵트인 상태를 결정하려면 데이터 요소를 설정하여 해당 쿠키를 읽은 후 규칙의 조건으로 사용하여 [!DNL Target] 로드 작업을 언제 실행할지 결정합니다.

별도로 동의 관리 플랫폼과 함께 [Adobe 옵트인 개체](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=ko)를 사용하여 이 태그의 실행을 제어할 수 있습니다.

동의 관리자(예: OneTrust)와 통합하면 고객에 대한 동의 쿠키를 설정 및 추적할 수 있으며, 이를 규칙 빌더에서 사용할 수 있습니다.
