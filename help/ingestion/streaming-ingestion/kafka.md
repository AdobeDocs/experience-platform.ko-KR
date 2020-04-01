---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 카프카 커넥터
topic: overview
translation-type: tm+mt
source-git-commit: f80b2e1d787d1f8d9fe8ac306422aa7744a69cd3

---


# Kafka Connector for Adobe Experience Platform

Adobe Experience Platform용 스트림 커넥터는 Apache Kafka Connect를 기반으로 합니다. 이 라이브러리는 데이터 센터의 Kafka 주제에서 Experience Platform으로 JSON 이벤트를 실시간으로 스트리밍하는 데 사용할 수 있습니다.

스트림 커넥터는 싱크(단방향) 커넥터로, Kafka 주제에서 Experience Platform의 등록된 끝점으로 데이터를 전달합니다. 이 커넥터를 사용하려면 라이브러리를 다운로드하고 기존 Kafka 배포에 추가한 다음 Kafka 항목을 Adobe Streaming HTTP URL에 구성해야 합니다. 추가 코드는 **필요하지 않습니다** . 커넥터는 다음 기능을 지원합니다.

- 인증된 데이터 수집
- 메시지를 일괄 처리하여 네트워크 호출 감소 및 처리량 향상

Kafka 커넥터에 대한 자세한 내용 및 커넥터 설정 방법은 [시작 안내서를](https://github.com/adobe/experience-platform-streaming-connect)참조하십시오. 자세한 워크플로우는 [개발자 안내서를](https://github.com/adobe/experience-platform-streaming-connect/blob/master/DEVELOPER_GUIDE.md)참조하십시오.