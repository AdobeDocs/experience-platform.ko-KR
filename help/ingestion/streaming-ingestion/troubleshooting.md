---
keywords: Experience Platform;home;popular topics;streaming;streaming ingestion;troubleshooting;streaming ingestion troubleshooting;streaming ingestion faq;faq;
solution: Experience Platform
title: 스트리밍 통합 문제 해결
topic: troubleshooting
description: 이 문서에서는 Adobe Experience Platform의 스트리밍 통합 관련 FAQ에 대한 답변을 제공합니다.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 0%

---


# 스트리밍 통합 문제 해결 가이드

이 문서에서는 Adobe Experience Platform의 스트리밍 통합 관련 FAQ에 대한 답변을 제공합니다. 모든 API에서 발생한 서비스 등 다른 [!DNL Platform] 서비스와 관련된 질문 및 문제 해결 [!DNL Platform] 은 [Experience Platform 문제 해결 가이드를 참조하십시오](../../landing/troubleshooting.md).

Adobe Experience Platform [!DNL Data Ingestion] 는 데이터를 인제스트하는 데 사용할 수 있는 RESTful API를 제공합니다 [!DNL Experience Platform]. 인제스트한 데이터는 개별 고객 프로필을 실시간으로 업데이트하는 데 사용되며, 이를 통해 다양한 채널에 개인화되고 연관성 있는 경험을 전달할 수 있습니다. 서비스에 대한 자세한 내용과 [다른 수집 방법은 데이터 통합 개요를](../home.md) 참조하십시오. 스트리밍 통합 API를 사용하는 방법에 대한 자세한 내용은 [스트리밍 통합 개요를 참조하십시오](../streaming-ingestion/overview.md).

## FAQ

다음은 스트리밍 통합 관련 FAQ에 대한 답변 목록입니다.

### 보내는 페이로드가 제대로 포맷되었는지 어떻게 알 수 있습니까?

[!DNL Data Ingestion] 는 [!DNL Experience Data Model] (XDM) 스키마를 활용하여 들어오는 데이터의 형식을 확인합니다. 사전 정의된 XDM 스키마의 구조에 맞지 않는 데이터를 전송하면 통합 작업이 실패합니다. XDM 및 XDM의 사용 방법에 대한 자세한 내용 [!DNL Experience Platform]은 [XDM 시스템 개요를 참조하십시오](../../xdm/home.md).

스트리밍 통합 기능은 두 가지 인증 모드를 지원합니다.동기 및 비동기. 각 유효성 검사 방법은 실패한 데이터를 다르게 처리합니다.

**개발 과정 중에 동기 유효성** 검사를 사용해야 합니다. 유효성 검사에 실패한 레코드가 삭제되고 실패한 이유에 대한 오류 메시지를 반환합니다(예:&quot;잘못된 XDM 메시지 형식&quot;).

**비동기식 유효성** 검사는 제작 과정에서 사용해야 합니다. 유효성 검사를 통과하지 않는 잘못된 형식의 데이터는 [!DNL Data Lake] 실패한 배치 파일로 전송되며 나중에 검색하여 추가 분석을 수행할 수 있습니다.

동기 및 비동기 유효성 검사에 대한 자세한 내용은 [스트리밍 유효성 검사 개요를 참조하십시오](../quality/streaming-validation.md). 유효성 검사에 실패한 배치를 보는 방법에 대한 자세한 내용은 실패한 배치 [검색 지침을 참조하십시오](../quality/retrieve-failed-batches.md).

### 요청 페이로드를 보내기 전에 유효성을 확인할 수 있습니까 [!DNL Platform]?

요청 페이로드는 전송 후에만 평가할 수 [!DNL Platform]있습니다. 동기 유효성 검사를 수행할 때 유효한 페이로드는 잘못된 페이로드를 수행하는 동안 채워진 JSON 개체를 반환합니다. 비동기 유효성 검사 동안 서비스는 잘못된 형식의 데이터를 감지하여 나중에 분석을 위해 검색할 수 있는 [!DNL Data Lake] 위치로 보냅니다. 자세한 내용은 [스트리밍 유효성 검사 개요를](../quality/streaming-validation.md) 참조하십시오.

### 동기적 유효성 검사가 지원되지 않는 가장자리에서 요청되면 어떻게 됩니까?

요청한 위치에 대해 동기 유효성 검사가 지원되지 않으면 501 오류 응답이 반환됩니다. 동기 유효성 검사에 대한 자세한 내용은 [스트리밍 유효성 검사 개요를](../quality/streaming-validation.md) 참조하십시오.

### 신뢰할 수 있는 소스에서만 데이터를 수집하려면 어떻게 해야 합니까?

[!DNL Experience Platform] 보안 데이터 수집을 지원합니다. 인증된 데이터 수집이 활성화되면 클라이언트는 JWT(JSON Web Token) 및 IMS 조직 ID를 요청 헤더로 전송해야 합니다. 인증된 데이터를 보내는 방법에 대한 자세한 내용 [!DNL Platform]은 [인증된 데이터 수집에 대한 안내서를 참조하십시오](../tutorials/create-authenticated-streaming-connection.md).

### 스트리밍 데이터의 지연은 [!DNL Real-time Customer Profile]무엇입니까?

스트리밍된 이벤트는 일반적으로 60초 [!DNL Real-time Customer Profile] 이내에 반영됩니다. 실제 대기 시간은 데이터 볼륨, 메시지 크기 및 대역폭 제한으로 인해 달라질 수 있습니다.

### 동일한 API 요청에 여러 메시지를 포함할 수 있습니까?

하나의 요청 페이로드 내에서 여러 메시지를 그룹화하여 스트림할 수 있습니다 [!DNL Platform]. 올바르게 사용할 경우 단일 요청 내에서 여러 메시지를 그룹화하는 것은 데이터 작업을 최적화하는 데 가장 좋은 방법입니다. 자세한 내용은 요청에서 [](../tutorials/streaming-multiple-messages.md) 여러 메시지를 전송하는 방법에 대한 자습서를 참조하십시오.

### 보내는 데이터가 수신되고 있는지 어떻게 알 수 있습니까?

전송 대상 [!DNL Platform] (성공 또는 기타)으로 전송된 모든 데이터는 데이터 세트에 지속되기 전에 일괄 파일로 저장됩니다. 배치의 처리 상태가 보낸 데이터 세트 내에 나타납니다.

데이터 세트 작업을 [Experience Platform 사용자 인터페이스를 사용하여 검사하여 데이터를 성공적으로 인제스트했는지 확인할 수 있습니다](https://platform.adobe.com). 왼쪽 탐색 **[!UICONTROL 에서 데이터]** 세트를 클릭하여 데이터 집합 목록을 표시합니다. 표시된 목록에서 스트리밍하고 있는 데이터 세트를 선택하여 데이터 세트 **[!UICONTROL 활동]** 페이지를 열고 선택한 기간 동안 전송된 모든 배치를 표시합니다. 데이터 스트림 모니터링 [!DNL Experience Platform] 에 사용하는 방법에 대한 자세한 내용은 스트리밍 데이터 흐름 [모니터링에 대한 가이드를 참조하십시오](../quality/monitor-data-flows.md).

데이터를 인제스트하지 못하고 데이터를 복구하려는 경우 해당 ID를 로 전송하여 실패한 배치를 검색할 수 [!DNL Platform][!DNL Data Access API]있습니다. 자세한 내용은 실패한 [배치](../quality/retrieve-failed-batches.md) 검색에 대한 가이드를 참조하십시오.

### Data Lake에서 내 스트리밍 데이터를 사용할 수 없는 이유는 무엇입니까?

잘못된 서식, 데이터 누락 또는 시스템 오류와 같이 일괄 처리 수집에 실패할 수 [!DNL Data Lake]있는 다양한 이유가 있습니다. 배치가 실패한 이유를 결정하려면 을 사용하여 배치를 [!DNL Data Ingestion Service API] 검색하고 세부 사항을 확인해야 합니다. 실패한 배치를 검색하는 방법에 대한 자세한 내용은 실패한 배치 [를 검색하는 방법에 대한 가이드를 참조하십시오](../quality/retrieve-failed-batches.md).

### API 요청에 대해 반환된 응답을 어떻게 분석합니까?

먼저 서버 응답 코드를 확인하여 요청이 수락되었는지 확인하여 응답을 구문 분석할 수 있습니다. 성공 응답 코드가 반환되면 배열 개체를 검토하여 통합 작업의 상태를 확인할 수 있습니다. `responses`

성공적인 단일 메시지 API 요청은 상태 코드 200을 반환합니다. 성공적으로(또는 부분적으로 성공한) 일괄 처리된 메시지 API 요청은 상태 코드 207을 반환합니다.

다음 JSON은 두 개의 메시지가 있는 API 요청에 대한 예제 응답 개체입니다.한 명은 성공했고 한 명은 실패했다. 성공적으로 스트리밍한 메시지가 속성을 `xactionId` 반환합니다. 스트림하지 않는 메시지는 `statusCode` 속성 및 추가 정보가 있는 응답 `message` 을 반환합니다.

```JSON
{
    "inletId": "9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5",
    "batchId": "1565638336649:1750:244",
    "receivedTimeMs": 1565638336705,
    "responses": [
        {
            "xactionId": "1565650704337:2124:92:3"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a
                79b25e9421ea127f5] 
                imsOrgId: [{IMS_ORG}] 
                Message has unknown xdm format"
        }
    ]
}
```

### 보낸 메시지가 수신되지 않는 이유는 무엇입니까 [!DNL Real-time Customer Profile]?

메시지를 [!DNL Real-time Customer Profile] 거부하면 잘못된 ID 정보 때문일 수 있습니다. 이는 ID에 대해 잘못된 값 또는 네임스페이스를 제공한 결과일 수 있습니다.

ID 네임스페이스에는 두 가지 유형이 있습니다.기본 및 사용자 지정. 사용자 정의 네임스페이스를 사용할 때는 네임스페이스가 안에 등록되어 있는지 확인하십시오 [!DNL Identity Service]. 기본 및 사용자 정의 네임스페이스 사용에 대한 자세한 내용은 [ID 네임스페이스 개요를](../../identity-service/namespaces.md) 참조하십시오.

메시지 수집에 실패한 이유에 대한 자세한 내용을 보려면 [[!DNL Experience Platform UI]를](https://platform.adobe.com) 사용할 수 있습니다. 왼쪽 탐색 **[!UICONTROL 에서 모니터링]** 을 클릭한 다음 **[!UICONTROL 전체]** 스트리밍 탭을 확인하여 선택한 기간 동안 스트리밍된 메시지 배치를 볼 수 있습니다.
