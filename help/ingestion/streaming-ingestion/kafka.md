---
keywords: Experience Platform;홈;인기 항목;카프카;카프카 커넥터;Kafka
solution: Experience Platform
title: Kafka Connector
topic-legacy: overview
description: Adobe Experience Platform용 스트림 커넥터는 Apache Kafka Connect를 기반으로 합니다. 이 라이브러리는 데이터 센터의 Kafka 주제에 있는 JSON 이벤트를 실시간으로 Experience Platform에 직접 스트리밍하는 데 사용할 수 있습니다.
exl-id: 062963e5-c727-4c2c-97db-8a9a5a7d903c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# [!DNL Kafka] Adobe Experience Platform용 커넥터

Adobe Experience Platform의 스트림 커넥터는 [!DNL Apache Kafka Connect]을 기반으로 합니다. 이 라이브러리는 데이터 센터의 [!DNL Kafka] 주제에서 실시간으로 [!DNL Experience Platform]로 JSON 이벤트를 바로 스트리밍하는 데 사용할 수 있습니다.

스트림 커넥터는 싱크(단방향) 커넥터로, [!DNL Kafka] 주제의 데이터를 [!DNL Experience Platform]의 등록된 끝점으로 전달합니다. 이 커넥터를 사용하려면 라이브러리를 다운로드하고 기존 [!DNL Kafka] 배포에 추가하고 [!DNL Kafka] 항목을 Adobe 스트리밍 HTTP URL에 구성해야 합니다. 추가 코드는 **이(가) 필요하지 않습니다.** 커넥터는 다음 기능을 지원합니다.

- 인증된 데이터 수집
- 메시지를 묶어서 네트워크 호출을 줄이고 처리량을 늘림

커넥터 설정 방법에 대한 지침을 포함한 [!DNL Kafka] 커넥터에 대한 자세한 내용은 [시작 안내서](https://github.com/adobe/experience-platform-streaming-connect)를 참조하십시오. 자세한 작업 과정은 [개발자 안내서](https://www.adobe.com/go/kafka-connector-developer-guide)를 참조하십시오.
