---
keywords: Experience Platform;홈;인기 항목;ECID;ecid
solution: Experience Platform
title: 개인 정보 요청에 대한 ID 데이터
topic-legacy: overview
description: 이 문서는 데이터 작업을 구성하고 Adobe 기술을 활용하여 고객 개인 정보 요청에 대한 적절한 ID 정보를 효과적으로 검색하는 방법에 대한 일반적인 지침을 제공합니다.
exl-id: 43b0292a-ea4d-4858-b584-ba71029724f6
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 3%

---

# 개인 정보 요청에 대한 ID 데이터

Adobe Experience Platform [!DNL Privacy Service]이(가) 개인 데이터에 대한 고객 요청을 처리(액세스, 삭제 또는 판매 거부 요청 포함)하려면 특정 고객을 Adobe Experience Cloud 사용 응용 프로그램에서 저장된 개인 데이터와 연결하는 고유한 식별자를 제공해야 합니다. [!DNL Privacy Service] 그런 다음 이러한 식별자를 사용하여 고객 ID 내에 저장된 모든 데이터 [!DNL Experience Cloud]를 수집하고 고객의 요청에 따라 데이터를 처리합니다.

이 문서는 데이터 작업을 구성하고 Adobe 기술을 활용하여 고객 개인 정보 요청에 대한 적절한 ID 정보를 효과적으로 검색하는 방법에 대한 일반적인 지침을 제공합니다.

## ID 및 네임스페이스

고객은 여러 채널을 통해 브랜드와 상호 작용할 수 있는 경우 이러한 많은 상호 작용에서 기록된 서로 다른 식별자를 조정하는 것이 어려울 수 있습니다. 따라서 [!DNL Experience Cloud] 응용 프로그램에서 어떤 데이터가 특정 사람에 속하는지 결정하기 어려울 수 있습니다.

예를 들어 [!DNL Privacy Service]에서 고객 데이터 요청을 처리할 때 ID는 Adobe 제어 도메인 아래에 설정된 쿠키 값, 제3자 도메인 아래에 있는 쿠키 값, Adobe과 공유되고에 공유되는 쿠키 값 또는 IMS 조직 내에서 명시적으로 정의하는 사용자 지정 식별자를 나타낼 수 있습니다.

따라서 [!DNL Privacy Service]에 전송된 각 ID에는 원본 시스템에 ID 값을 연결하여 컨텍스트를 제공하는 네임스페이스가 함께 있어야 합니다. 네임스페이스는 이메일 주소(&quot;이메일&quot;)와 같은 일반적인 개념을 나타내거나 ID를 Adobe Advertising Cloud ID(&quot;AdCloud&quot;) 또는 Adobe Target ID(&quot;TNTID&quot;)와 같은 특정 응용 프로그램과 연결할 수 있습니다.

Adobe Experience Platform Identity Service는 전역적으로 정의된 ID 네임스페이스와 사용자 정의 ID 네임스페이스의 저장소를 유지 관리합니다. 네임스페이스에 대한 자세한 내용은 [identity 네임스페이스 개요](../identity-service/namespaces.md)를 참조하십시오. [!DNL Privacy Service]에서 일반적으로 사용되는 표준 네임스페이스 및 네임스페이스 한정자 목록은 개발자 안내서의 [부록 섹션](api/appendix.md)을 참조하십시오.

## ECID 및 옵트인 서비스

Adobe Experience Cloud [!DNL Identity Service]은(는) [!DNL Experience Cloud]에 대한 일반적인 식별 프레임워크 역할을 하며, 각 사이트 방문자에게 고유한 영구 ID를 할당합니다. [!DNL Experience Cloud] ID(ECID)는 자사 쿠키를 사용하여 고객의 활동을 추적하고, 여러 응용 프로그램에서 장치를 고유하게 식별할 수 있으며, 다른 [!DNL Experience Cloud] 응용 프로그램에서 동일한 사이트 방문자와 해당 데이터를 식별할 수 있습니다. 자세한 내용은 [Experience Cloud ID 서비스 개요](https://docs.adobe.com/content/help/ko-KR/id-service/using/intro/overview.html)를 참조하십시오.

[!DNL Experience Cloud Identity Service] 확장 옵트인 서비스를 사용하면 방문자의 장치 또는 브라우저에서 쿠키를 설정할 수 있는지 여부를 방문자가 결정할 수 있도록 응용 프로그램에서 프로토콜을 설정할 수 있습니다. 응용 프로그램의 서비스 설정 방법을 포함하여 옵트인 서비스에 대한 자세한 내용은 [옵트인 서비스 문서](https://docs.adobe.com/content/help/ko-KR/id-service/using/implementation/opt-in-service/optin-overview.html)를 참조하십시오.

사이트 방문자에게 ECID가 할당되면 다음 섹션에 설명된 대로 Adobe [!DNL Privacy JavaScript Library]를 사용하여 개인 정보 요청에 사용할 ID를 검색할 수 있습니다.

## [!DNL Privacy JS Library]

[!DNL Adobe Privacy JavaScript Library]은 브라우저에 저장된 고객 ID를 검색하고 제거할 수 있는 여러 기능을 제공합니다. ECID를 비롯한 여러 Adobe 애플리케이션에서 ID 정보를 검색하도록 라이브러리를 구성할 수 있습니다. 콜백이나 약속을 사용하여 성공적으로 검색된 ID를 프로그래밍 방식으로 처리하고 [!DNL Privacy Service] API로 보낼 수 있습니다.

몇 가지 일반적인 사용 사례에 대한 코드 샘플을 포함하여 [!DNL Privacy JS Library]에 대한 자세한 내용은 [개인 정보 JS 라이브러리 개요](js-library.md)를 참조하십시오.

## 다음 단계

이 문서에서는 개인 정보 요청에 사용하기 위해 고객 ID 데이터를 검색하는 것과 관련된 중앙 개념 개요를 제공합니다. 이러한 개념 및 서비스에 대한 자세한 내용은 각 섹션에 제공된 설명서 링크를 검토하는 것이 좋습니다. 액세스, 삭제 또는 판매 거부 요청을 만들기 위해 검색된 ID를 [!DNL Privacy Service]으로 전송하는 방법에 대한 단계는 [Privacy Service 개발자 안내서](api/getting-started.md)를 참조하십시오.
