---
title: Edge Network Server API 개요
description: Edge Network Server API란 무엇이며 이를 사용하는 방법에 대해 알아봅니다.
seo-description: Learn what the Edge Network Server API is and how you can use it.
keywords: 데이터 수집;수집;Adobe Experience Platform Edge Network;서버 api;
exl-id: 46bd8798-d7f9-405b-9ca8-856ad4aa688c
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 5%

---

# Edge Network Server API 개요 {#overview}

Adobe Experience Platform Edge Network는 고객이 모든 Adobe Experience Cloud 또는 Adobe Experience Platform Edge 서비스와 상호 작용할 수 있는 최적화된 방법을 제공합니다.

다음 [!DNL Edge Network Server API] 는 다양한 데이터 수집, 개인화, 광고 및 마케팅 활용 사례에 사용할 수 있습니다. 다음 [!DNL Server API] 서버에서 사용할 수 있으며 [!DNL IoT] 장치, 셋톱 박스 및 다양한 기타 장치.

다음 이후 [!DNL Server API] 로드할 라이브러리에 의존하지 않고 Adobe Experience Platform Edge Network 및 지원되는 솔루션과 빠르게 상호 작용하는 방법을 제공합니다.

의 이점 [!DNL Server API] 아키텍처는 다음과 같습니다.

* 페이지 로드 시간 감소
* 지연 시간 개선
* 자사 데이터 수집
* 서비스 간의 간소화된 서버측 통신

다음 [!DNL Server API] 에서는 두 개의 전용 엔드포인트를 통해 대화형 및 배치 데이터 수집을 지원합니다.

1. 대화형 종단점은 고급 세그멘테이션, 개인화 및 기타 마케팅 사용 사례를 지원하는 Adobe Experience Platform 및 Adobe Experience Cloud 서비스와의 통신을 지원합니다.
2. 배치 종단점을 사용하면 호출되는 응용 프로그램에서 응답을 받지 않고 데이터를 온보딩해야 할 때 요청을 일괄적으로 보낼 수 있습니다.

다음 [!DNL Server API] 는 다음 유형의 요청을 지원합니다.

* 를 통해 인증된 요청 [Adobe I/O](https://developer.adobe.com/), 새 `server.adobedc.net` 엔드포인트.
* 를 통해 인증되지 않은 요청 `edge.adobedc.net` 엔드포인트.

이를 통해 조직의 개인정보 처리방침에 따라 인증된 안전한 데이터를 수집할 수 있는 사용 사례를 가능하게 합니다. 인증 외에 서버 API는 API를 통해 인증된 통신만 수락하도록 데이터 스트림 표시를 지원합니다.

서버 API에 대한 간소화된 개요를 살펴보려면 아래 비디오를 시청하십시오.

>[!VIDEO](https://video.tv.adobe.com/v/341448/)
