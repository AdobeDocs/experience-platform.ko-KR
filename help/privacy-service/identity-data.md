---
keywords: Experience Platform;홈;인기 항목;ECID;ecid
solution: Experience Platform
title: 개인 정보 요청에 대한 ID 데이터
description: 이 문서에서는 데이터 작업을 구성하고 Adobe 기술을 활용하여 고객 개인 정보 보호 요청에 대한 적절한 ID 정보를 효과적으로 검색하는 방법에 대한 일반적인 지침을 제공합니다.
exl-id: 43b0292a-ea4d-4858-b584-ba71029724f6
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 2%

---

# 개인 정보 요청에 대한 ID 데이터

Adobe Experience Platform 주문 [!DNL Privacy Service] 개인 데이터에 대한 고객 요청을 처리(액세스, 삭제 또는 판매 중지 요청 포함)하려면 특정 고객을 Adobe Experience Cloud 지원 애플리케이션에서 저장된 개인 데이터에 연결하는 고유한 식별자를 제공해야 합니다. [!DNL Privacy Service] 그런 다음 를 사용하여 내에서 고객의 ID에 저장된 모든 데이터를 수집합니다 [!DNL Experience Cloud], 고객의 요청에 따라 처리합니다.

이 문서에서는 데이터 작업을 구성하고 Adobe 기술을 활용하여 고객 개인 정보 보호 요청에 대한 적절한 ID 정보를 효과적으로 검색하는 방법에 대한 일반적인 지침을 제공합니다.

## ID 및 네임스페이스

고객이 여러 가지 채널을 통해 브랜드와 상호 작용할 수 있는 경우 이러한 많은 상호 작용에서 기록된 서로 다른 식별자를 조정하는 것이 어려울 수 있습니다. 따라서 사용자의 특정 사람에 속하는 데이터를 확인하기 어려울 수 있습니다 [!DNL Experience Cloud] 응용 프로그램.

예를 들어에서 고객 데이터 요청을 처리할 때 [!DNL Privacy Service]를 지정하는 경우, id는 Adobe 제어 도메인에 설정된 쿠키 값, 타사 도메인 아래에 있고 Adobe과 공유되는 쿠키 값 또는 조직 내에서 명시적으로 정의하는 사용자 지정 식별자를 나타낼 수 있습니다.

따라서 각 ID를에 보내야 합니다 [!DNL Privacy Service] 는 id 값을 원본 시스템과 관련시켜 컨텍스트를 제공하는 네임스페이스와 함께 사용됩니다. 네임스페이스는 이메일 주소(&quot;이메일&quot;)와 같은 일반적인 개념을 나타내거나 ID를 Adobe Advertising Cloud ID(&quot;AdCloud&quot;) 또는 Adobe Target ID(&quot;TNTID&quot;)와 같은 특정 애플리케이션과 연결할 수 있습니다.

Adobe Experience Platform Identity 서비스는 전역적으로 정의된 사용자 정의 ID 네임스페이스의 저장소를 유지 관리합니다. 네임스페이스에 대한 자세한 내용은 [id 네임스페이스 개요](../identity-service/namespaces.md). 에서 일반적으로 사용되는 표준 네임스페이스 및 네임스페이스 한정자 목록을 보려면 [!DNL Privacy Service]를 참조하고 [부록 섹션](api/appendix.md) 를 참조하십시오.

## ECID 및 옵트인 서비스

Adobe Experience Cloud [!DNL Identity Service] 는 의 공통 식별 프레임워크로서 사용됩니다. [!DNL Experience Cloud], 및은 각 사이트 방문자에게 고유한 영구 ID를 할당합니다. 다음 [!DNL Experience Cloud] ECID(ID)는 자사 쿠키를 사용하여 고객의 활동을 추적하고 여러 애플리케이션에서 장치를 고유하게 식별할 수 있으며 동일한 사이트 방문자와 해당 데이터를 다른 곳에서 식별할 수 있습니다 [!DNL Experience Cloud] 응용 프로그램. 자세한 내용은 [Experience Cloud ID 서비스 개요](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html) 추가 정보.

옵트인 서비스, 확장 [!DNL Experience Cloud Identity Service]를 사용하면 방문자가 방문자의 장치나 브라우저에서 쿠키를 설정할 수 있는지 여부를 확인할 수 있도록 애플리케이션에 프로토콜을 설정할 수 있습니다. 애플리케이션 서비스 설정 방법 등 옵트인 서비스에 대한 자세한 내용은 다음을 참조하십시오 [옵트인 서비스 설명서](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=ko-KR).

사이트 방문자에게 ECID가 할당되면 Adobe을 활용할 수 있습니다 [!DNL Privacy JavaScript Library] 다음 섹션에 설명된 대로 개인 정보 보호 요청에 사용할 해당 ID를 검색하기 위한 것입니다.

## [!DNL Privacy JS Library]

다음 [!DNL Adobe Privacy JavaScript Library] 는 브라우저에 저장된 고객 ID를 검색하고 제거할 수 있도록 해주는 여러 기능을 제공합니다. 라이브러리는 ECID를 포함하여 여러 Adobe 애플리케이션에서 ID 정보를 검색하도록 구성할 수 있습니다. 콜백 또는 약속을 사용하여 검색된 ID를 프로그래밍 방식으로 처리하고 ID를 [!DNL Privacy Service] API.

에 대한 자세한 정보 [!DNL Privacy JS Library]여러 가지 일반적인 사용 사례에 대한 코드 샘플을 포함한 는 [개인 정보 JS 라이브러리 개요](js-library.md).

## 다음 단계

이 문서에서는 개인 정보 보호 요청에 사용할 고객 ID 데이터를 검색하는 것과 관련된 중앙 개념에 대한 간단한 개요를 제공합니다. 이러한 개념 및 서비스에 대한 자세한 내용은 각 섹션에 제공된 설명서 링크를 검토하는 것이 좋습니다. 검색된 ID를 로 보내는 방법에 대한 절차 [!DNL Privacy Service] 액세스, 삭제 또는 판매 중지 요청을 만들려면 [Privacy Service API 안내서](api/overview.md).
