---
title: Edge Network Server API 개요
description: Edge Network Server API란 무엇이며 이를 사용하는 방법에 대해 알아봅니다.
source-git-commit: 68174928d3b005d1e5a31b17f3f287e475b5dc86
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 5%

---


# Edge Network Server API 개요 {#overview}

Adobe Experience Platform Edge Network는 고객이 Adobe Experience Cloud 또는 Adobe Experience Platform Edge 서비스와 상호 작용할 수 있는 최적화된 방법을 제공합니다.

다음 [!DNL Edge Network Server API] 다양한 데이터 수집, 개인화, 광고 및 마케팅 사용 사례에 사용할 수 있습니다. 다음 [!DNL Server API] 서버에서 사용할 수 있습니다. [!DNL IoT] 장치, 셋톱 박스 및 다양한 기타 장치.

다음 이후 [!DNL Server API] 로드하는 라이브러리에 의존하지 않으며, Adobe Experience Platform Edge Network 및 지원되는 솔루션과 상호 작용하는 빠른 방법을 제공합니다.

의 이점 [!DNL Server API] 아키텍처는 다음과 같습니다.

* 페이지 로드 시간 단축
* 향상된 지연 시간
* 자사 데이터 수집
* 서비스 간 서버 측 통신 간소화

다음 [!DNL Server API] 는 두 개의 전용 끝점을 통해 대화형 및 일괄 데이터 수집을 지원합니다.

1. 대화형 엔드포인트는 고급 세분화, 개인화 및 기타 마케팅 사용 사례를 지원하는 Adobe Experience Platform 및 Adobe Experience Cloud 서비스와의 통신을 지원합니다.
2. 배치 끝점을 사용하면 호출되는 애플리케이션에서 응답을 받지 않고 데이터를 온보딩해야 하는 경우 요청을 일괄적으로 전송할 수 있습니다.

다음 [!DNL Server API] 는 다음 유형의 요청을 지원합니다.

* 다음을 통해 인증된 요청 [Adobe Developer](https://developer.adobe.com/), 사용 `server.adobedc.net` 엔드포인트.
* 를 통한 인증되지 않은 요청 `edge.adobedc.net` 엔드포인트.

이를 통해 조직의 개인정보 처리방침에 따라 중요한 데이터의 안전하고 인증된 수집을 허용하는 사용 사례를 사용할 수 있습니다. 인증 외에도 Server API는 API를 통해 인증된 통신만 수락하도록 데이터스트림 표시를 지원합니다.

서버 API에 대한 간소화된 개요는 아래 비디오를 참조하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/341448/)
