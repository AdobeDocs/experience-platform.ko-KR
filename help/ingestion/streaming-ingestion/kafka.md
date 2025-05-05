---
keywords: Experience Platform;홈;인기 항목;kafka;kafka 커넥터;Kafka;
solution: Experience Platform
title: Kafka 커넥터
description: Adobe Experience Platform용 스트림 커넥터는 Apache Kafka Connect를 기반으로 합니다. 이 라이브러리를 사용하여 데이터 센터의 Kafka 주제에서 실시간으로 Experience Platform으로 JSON 이벤트를 직접 스트리밍할 수 있습니다.
exl-id: 062963e5-c727-4c2c-97db-8a9a5a7d903c
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 0%

---

# Adobe Experience Platform용 [!DNL Kafka] 커넥터

Adobe Experience Platform용 스트림 커넥터는 [!DNL Apache Kafka Connect]을(를) 기반으로 합니다. 이 라이브러리를 사용하여 데이터 센터의 [!DNL Kafka] 항목에서 [!DNL Experience Platform] (으)로 JSON 이벤트를 실시간으로 직접 스트리밍할 수 있습니다.

스트림 커넥터는 싱크(단방향) 커넥터로 [!DNL Kafka] 항목에서 [!DNL Experience Platform]에 등록된 끝점으로 데이터를 전달합니다. 이 커넥터를 사용하려면 라이브러리를 다운로드하여 기존 [!DNL Kafka] 배포에 추가하고 Adobe 스트리밍 HTTP URL에 [!DNL Kafka] 주제를 구성해야 합니다. 추가 코드는 **필요 없음**&#x200B;입니다. 커넥터는 다음 기능을 지원합니다.

- 인증된 데이터 수집
- 메시지를 일괄 처리하여 네트워크 호출 감소 및 처리량 향상

커넥터 설정 방법에 대한 지침을 포함하여 [!DNL Kafka] 커넥터에 대한 자세한 내용은 [시작 안내서](https://github.com/adobe/experience-platform-streaming-connect)를 참조하십시오. 자세한 워크플로는 [개발자 안내서](https://www.adobe.com/go/kafka-connector-developer-guide)를 참조하십시오.
