---
keywords: Experience Platform;홈;인기 항목;스트리밍;스트리밍 수집;문제 해결;스트리밍 수집 문제 해결;스트리밍 수집 faq;faq;
solution: Experience Platform
title: 스트리밍 수집 문제 해결 안내서
topic-legacy: troubleshooting
description: 이 문서에서는 Adobe Experience Platform의 수집 스트리밍에 대한 FAQ에 대한 답변을 제공합니다.
exl-id: 5d5deccf-25b8-44c9-ae27-9a4713ced274
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 0%

---

# 스트리밍 수집 문제 해결 안내서

이 문서에서는 Adobe Experience Platform의 수집 스트리밍에 대한 FAQ에 대한 답변을 제공합니다. 기타 관련 질문 및 문제 해결 [!DNL Platform] 서비스(모든 위치에서 발생한 서비스 포함) [!DNL Platform] API는 [Experience Platform 문제 해결 안내서](../../landing/troubleshooting.md).

Adobe Experience Platform [!DNL Data Ingestion] 는 데이터를 수집하기 위해 사용할 수 있는 RESTful API를 제공합니다. [!DNL Experience Platform]. 수집된 데이터는 개별 고객 프로필을 거의 실시간으로 업데이트하는 데 사용되므로 여러 채널에서 개인화된 관련 경험을 제공할 수 있습니다. 자세한 내용은 [데이터 수집 개요](../home.md) 를 참조하십시오. 스트리밍 수집 API를 사용하는 방법에 대한 단계는 다음을 참조하십시오. [스트리밍 수집 개요](../streaming-ingestion/overview.md).

## FAQ

다음은 스트리밍 통합에 대한 FAQ에 대한 답변 목록입니다.

### 보내는 페이로드가 제대로 포맷되었는지 어떻게 알 수 있습니까?

[!DNL Data Ingestion] 활용 [!DNL Experience Data Model] (XDM) 스키마를 사용하여 들어오는 데이터 형식의 유효성을 검사합니다. 사전 정의된 XDM 스키마 구조를 준수하지 않는 데이터를 보내면 수집이 실패합니다. XDM 및 의 사용에 대한 자세한 정보 [!DNL Experience Platform]를 참조하고 [XDM 시스템 개요](../../xdm/home.md).

스트리밍 수집은 두 가지 유효성 검사 모드를 지원합니다. 동기 및 비동기. 각 유효성 검사 방법은 실패한 데이터를 다르게 처리합니다.

**동기 유효성 검사** 는 개발 프로세스 중에 사용해야 합니다. 유효성 검사에 실패한 레코드는 삭제하고 실패한 이유에 대한 오류 메시지를 반환합니다(예: &quot;잘못된 XDM 메시지 형식&quot;).

**비동기 유효성 검사** 프로덕션에 사용해야 합니다. 유효성 검사를 통과하지 않는 잘못된 데이터는 모두 [!DNL Data Lake] 실패한 배치 파일로, 나중에 검색하여 추가로 분석할 수 있습니다.

동기 및 비동기 유효성 검사에 대한 자세한 내용은 [스트리밍 유효성 검사 개요](../quality/streaming-validation.md). 유효성 검사가 실패한 배치를 보는 방법에 대한 단계는 다음 안내서를 참조하십시오 [실패한 배치 검색](../quality/retrieve-failed-batches.md).

### 요청 페이로드를 전송하기 전에 유효성을 검사할 수 있습니까? [!DNL Platform]?

요청 페이로드는 전송 후에만 평가할 수 있습니다 [!DNL Platform]. 동기 유효성 검사를 수행할 때 유효한 페이로드는 채워진 JSON 개체를 반환하고 잘못된 페이로드는 오류 메시지를 반환합니다. 비동기 유효성 검사 중에 서비스는 잘못된 데이터를 감지하여 로 보냅니다 [!DNL Data Lake] 나중에 검색하여 분석할 수 있습니다. 자세한 내용은 [스트리밍 유효성 검사 개요](../quality/streaming-validation.md) 추가 정보.

### 지원하지 않는 에지에서 동기 유효성 검사가 요청되면 어떻게 됩니까?

요청한 위치에 대해 동기 유효성 검사가 지원되지 않으면 501 오류 응답이 반환됩니다. 자세한 내용은 [스트리밍 유효성 검사 개요](../quality/streaming-validation.md) 동기 유효성 검사에 대한 자세한 정보.

### 신뢰할 수 있는 소스에서만 데이터를 수집하려면 어떻게 해야 합니까?

[!DNL Experience Platform] 에서는 보안 데이터 수집을 지원합니다. 인증된 데이터 수집이 활성화되면 클라이언트는 JSON 웹 토큰(JWT) 및 IMS 조직 ID를 요청 헤더로 전송해야 합니다. 인증된 데이터를에 보내는 방법에 대한 자세한 정보 [!DNL Platform], 다음 안내서를 참조하십시오. [인증된 데이터 수집](../tutorials/create-authenticated-streaming-connection.md).

### 에 데이터를 스트리밍할 때까지의 지연 시간은 얼마입니까 [!DNL Real-Time Customer Profile]?

스트리밍되는 이벤트는 일반적으로 [!DNL Real-Time Customer Profile] 60초 이내에 실제 지연 시간은 데이터 볼륨, 메시지 크기 및 대역폭 제한 때문에 달라질 수 있습니다.

### 동일한 API 요청에 여러 메시지를 포함할 수 있습니까?

단일 요청 페이로드 내에 여러 메시지를 그룹화하고 스트리밍할 수 있습니다 [!DNL Platform]. 올바르게 사용하는 경우 단일 요청 내에 여러 메시지를 그룹화하는 것이 데이터 작업을 최적화하는 좋은 방법입니다. 다음 내용을 참조하십시오. [요청에서 여러 메시지 보내기](../tutorials/streaming-multiple-messages.md) 추가 정보.

### 보내는 데이터가 수신되는지 어떻게 알 수 있습니까?

전송되는 모든 데이터 [!DNL Platform] (성공적 또는 다른 방식으로) 는 데이터 세트에 유지되기 전에 배치 파일로 저장됩니다. 일괄 처리의 처리 상태가 보낸 데이터 세트 내에 표시됩니다.

를 사용하여 데이터 집합 활동을 확인하여 데이터가 성공적으로 수집되었는지 확인할 수 있습니다. [Experience Platform 사용자 인터페이스](https://platform.adobe.com). 클릭 **[!UICONTROL 데이터 세트]** 왼쪽 탐색에서 데이터 세트 목록을 표시합니다. 표시된 목록에서 스트리밍할 데이터 세트를 선택하여 엽니다 **[!UICONTROL 데이터 집합 활동]** 페이지, 선택한 기간 동안 전송된 모든 배치를 표시합니다. 사용에 대한 자세한 정보 [!DNL Experience Platform] 데이터 스트림을 모니터링하려면 안내서 를 참조하십시오 [스트리밍 데이터 흐름 모니터링](../quality/monitor-data-ingestion.md).

데이터를 수집하지 않고 복구하려는 경우 [!DNL Platform]로 해당 ID를 보내어 실패한 배치를 검색할 수 있습니다 [!DNL Data Access API]. 다음 안내서를 참조하십시오. [실패한 배치 검색](../quality/retrieve-failed-batches.md) 추가 정보.

### Data Lake에서 스트리밍 데이터를 사용할 수 없는 이유는 무엇입니까?

배치 수집이 [!DNL Data Lake]잘못된 형식, 누락된 데이터 또는 시스템 오류와 같은 문제가 발생합니다. 배치에 실패한 이유를 확인하려면 [!DNL Data Ingestion Service API] 세부 사항을 확인합니다. 실패한 배치를 검색하는 자세한 단계는 다음 사항에 대한 안내서를 참조하십시오. [실패한 배치 검색](../quality/retrieve-failed-batches.md).

### API 요청에 대해 반환된 응답을 구문 분석하려면 어떻게 합니까?

먼저 서버 응답 코드를 확인하여 응답을 통해 구문 분석하여 요청이 수락되었는지 확인할 수 있습니다. 성공적인 응답 코드가 반환되면 `responses` 배열 개체를 사용하여 수집 작업의 상태를 확인합니다.

성공적인 단일 메시지 API 요청은 상태 코드 200을 반환합니다. 성공적으로(또는 부분적으로 성공한) 일괄 처리된 메시지 API 요청은 상태 코드 207을 반환합니다.

다음 JSON은 두 개의 메시지가 있는 API 요청에 대한 예제 응답 개체입니다. 하나는 성공했고 하나는 실패했어요. 성공적으로 스트리밍한 메시지는 `xactionId` 속성을 사용합니다. 스트리밍되지 않은 메시지는 `statusCode` 속성 및 응답 `message` 추가 정보 포함.

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
                imsOrgId: [{ORG_ID}] 
                Message has unknown xdm format"
        }
    ]
}
```

### 보낸 메시지가 수신되지 않는 이유는 무엇입니까? [!DNL Real-Time Customer Profile]?

If [!DNL Real-Time Customer Profile] 는 메시지를 거부하므로 잘못된 ID 정보로 인해 발생할 수 있습니다. 이는 ID에 잘못된 값 또는 네임스페이스를 제공한 결과일 수 있습니다.

ID 네임스페이스에는 두 가지 유형이 있습니다. 기본 및 사용자 지정. 사용자 지정 네임스페이스를 사용할 때는 네임스페이스가 [!DNL Identity Service]. 자세한 내용은 [id 네임스페이스 개요](../../identity-service/namespaces.md) 기본 및 사용자 지정 네임스페이스 사용에 대한 자세한 내용을 참조하십시오.

를 사용할 수 있습니다 [[!DNL Experience Platform UI]](https://platform.adobe.com) 를 참조하십시오. 클릭 **[!UICONTROL 모니터링]** 왼쪽 탐색에서 **[!UICONTROL 처음부터 끝까지 스트리밍]** 탭하여 선택한 기간 동안 스트리밍되는 메시지 배치를 볼 수 있습니다.
