---
keywords: Experience Platform;home;popular topics;kafka;kafka connector;Kafka;
solution: Experience Platform
title: Kafka 커넥터
topic: overview
description: Adobe Experience Platform용 스트림 커넥터는 Apache Kafka Connect를 기반으로 합니다. 이 라이브러리는 데이터 센터의 Kafka 주제에서 실시간으로 Experience Platform으로 JSON 이벤트를 스트리밍하는 데 사용할 수 있습니다.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---


# [!DNL Kafka] adobe experience platform

Adobe Experience Platform의 스트림 커넥터는 기반 [!DNL Apache Kafka Connect]입니다. 이 라이브러리를 사용하여 데이터 센터의 [!DNL Kafka] 주제 [!DNL Experience Platform] 에서 실시간으로 JSON 이벤트를 스트리밍할 수 있습니다.

스트림 커넥터가 싱크(단방향) 커넥터로 주제의 데이터를 등록된 종단점으로 [!DNL Kafka] 배달합니다 [!DNL Experience Platform]. 이 커넥터를 사용하려면 라이브러리를 다운로드하고 기존 배포에 추가하고 Adobe 스트리밍 HTTP URL에 [!DNL Kafka] [!DNL Kafka] 항목을 구성해야 합니다. 추가 코드는 **필요하지 않습니다** . 커넥터는 다음 기능을 지원합니다.

- 인증된 데이터 수집
- 메시지를 일괄 처리하여 네트워크 호출 감소 및 처리량 증가

커넥터를 설정하는 방법에 대한 지침을 비롯하여 [!DNL Kafka] 커넥터에 대한 자세한 내용은 [시작 안내서를 참조하십시오](https://github.com/adobe/experience-platform-streaming-connect). 자세한 작업 과정은 [개발자 안내서를 참조하십시오](https://github.com/adobe/experience-platform-streaming-connect/blob/master/DEVELOPER_GUIDE.md).