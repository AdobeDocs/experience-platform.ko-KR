---
keywords: Experience Platform;대상 api;애드혹 활성화;대상 활성화 애드혹
solution: Experience Platform
title: 임시 활성화 API를 통해 대상을 일괄 대상으로 활성화
description: 이 문서에서는 활성화 전에 수행되는 세분화 작업을 포함하여 임시 활성화 API를 통해 대상을 활성화하기 위한 전체적인 워크플로를 보여 줍니다.
type: Tutorial
exl-id: 1a09f5ff-0b04-413d-a9f6-57911a92b4e4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1623'
ht-degree: 0%

---

# 애드혹 활성화 API를 통해 온디맨드로 대상자를 배치 대상으로 활성화합니다

>[!IMPORTANT]
>
>Beta 단계를 완료하면 이제 모든 Experience Platform 고객이 [!DNL ad-hoc activation API]을(를) GA(일반 출시)할 수 있습니다. GA 버전에서 API가 버전 2로 업그레이드되었습니다. API에 더 이상 내보내기 ID가 필요하지 않으므로 4단계([최신 대상 내보내기 작업 ID 가져오기](#segment-export-id))는 더 이상 필요하지 않습니다.
>
>자세한 내용은 이 자습서의 아래 [임시 활성화 작업 실행](#activation-job)을 참조하십시오.

## 개요 {#overview}

임시 활성화 API 를 사용하면 마케터가 즉각적인 활성화가 필요한 상황에 대해 빠르고 효율적인 방식으로 대상 대상을 프로그래밍 방식으로 활성화할 수 있습니다.

임시 활성화 API를 사용하여 전체 파일을 원하는 파일 수신 시스템으로 내보냅니다. 임시 대상 활성화는 [일괄 파일 기반 대상](../destination-types.md#file-based)에서만 지원됩니다.

아래 다이어그램은 24시간마다 Experience Platform에서 발생하는 세분화 작업을 포함하여 임시 활성화 API를 통해 대상을 활성화하기 위한 전체적인 워크플로우를 보여 줍니다.

![ad-hoc-activation](../assets/api/ad-hoc-activation/ad-hoc-activation-overview.png)

## 사용 사례 {#use-cases}

### 플래시 판매 또는 프로모션

온라인 retailer은 제한된 플래시 세일을 준비하고 있으며 고객에게 짧은 시간에 알리기를 원합니다. 마케팅 팀은 Experience Platform 임시 활성화 API를 통해 온디맨드로 대상자를 내보내고 프로모션 이메일을 신속하게 고객 기반으로 전송할 수 있습니다.

### 최신 이벤트 또는 속보

A호텔 측은 앞으로 며칠간 악천후가 예상되며, 해당 팀은 도착 손님들에게 신속히 알리기를 원하기 때문에 그에 맞는 계획을 세울 수 있다. 마케팅 팀은 Experience Platform 애드혹 활성화 API 를 사용하여 대상을 온디맨드로 내보내고 게스트에게 알릴 수 있습니다.

### 통합 테스트

IT 관리자는 Experience Platform 임시 활성화 API를 사용하여 대상을 온디맨드로 내보낼 수 있으므로 Adobe Experience Platform과의 사용자 정의 통합을 테스트하고 모든 것이 올바르게 작동하는지 확인할 수 있습니다.

## 가드레일 {#guardrails}

임시 활성화 API를 사용할 때는 다음 보호 기능에 유의하십시오.

* 현재 각 임시 활성화 작업은 최대 80개의 대상을 활성화할 수 있습니다. 작업당 80개 이상의 대상을 활성화하려고 하면 작업이 실패합니다. 이 동작은 향후 릴리스에서 변경될 수 있습니다.
* 임시 활성화 작업은 예약된 [대상 내보내기 작업](../../segmentation/api/export-jobs.md)과(와) 동시에 실행할 수 없습니다. 임시 활성화 작업을 실행하기 전에 예약된 대상자 내보내기 작업이 완료되었는지 확인하십시오. 활성화 흐름의 상태를 모니터링하는 방법에 대한 자세한 내용은 [대상 데이터 흐름 모니터링](../../dataflows/ui/monitor-destinations.md)을 참조하십시오. 예를 들어 활성화 데이터 흐름에서 **[!UICONTROL 처리 중]** 상태가 표시되면 임시 활성화 작업을 실행하기 전에 완료될 때까지 기다리십시오.
* 대상자당 두 개 이상의 동시 임시 활성화 작업을 실행하지 마십시오.

## 세그먼테이션 고려 사항 {#segmentation-considerations}

Adobe Experience Platform은 예약된 세분화 작업을 24시간마다 한 번씩 실행합니다. 임시 활성화 API는 최신 세분화 결과를 기반으로 실행됩니다.

## 1단계: 사전 요구 사항 {#prerequisites}

Adobe Experience Platform API를 호출하려면 먼저 다음 전제 조건을 충족하는지 확인하십시오.

* Adobe Experience Platform에 액세스할 수 있는 조직 계정이 있습니다.
* Experience Platform 계정에 Adobe Experience Platform API 제품 프로필에 대해 `developer` 및 `user` 역할이 활성화되어 있습니다. 계정에 대해 이러한 역할을 활성화하려면 [Admin Console](../../access-control/home.md) 관리자에게 문의하십시오.
* Adobe ID이 있습니다. Adobe ID이 없는 경우 [Adobe Developer Console](https://developer.adobe.com/console)&#x200B;(으)로 이동하여 새 계정을 만드십시오.

## 2단계: 자격 증명 수집 {#credentials}

Experience Platform API를 호출하려면 먼저 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 모든 Experience Platform API 호출에서 필요한 각 헤더에 대한 값이 제공됩니다.

* 인증: 전달자 `{ACCESS_TOKEN}`
* x-api 키: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Experience Platform의 리소스는 특정 가상 샌드박스로 분리될 수 있습니다. Experience Platform API 요청에서 작업이 수행될 샌드박스의 이름과 ID를 지정할 수 있습니다. 이러한 매개 변수는 선택 사항입니다.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Experience Platform의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하십시오.

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* Content-Type: `application/json`

## 3단계: Experience Platform UI에서 활성화 흐름 만들기 {#activation-flow}

임시 활성화 API를 통해 대상을 활성화하려면 먼저 선택한 대상에 대해 Experience Platform UI에 활성화 흐름이 구성되어 있어야 합니다.

여기에는 활성화 워크플로, 대상자 선택, 일정 구성 및 활성화가 포함됩니다. UI 또는 API를 사용하여 활성화 플로우를 만들 수 있습니다.

* [Experience Platform UI를 사용하여 프로필 내보내기 대상을 일괄 처리하는 활성화 플로우를 만듭니다](../ui/activate-batch-profile-destinations.md)
* [흐름 서비스 API를 사용하여 프로필 내보내기 대상 일괄 연결에 연결하고 데이터를 활성화합니다](../api/connect-activate-batch-destinations.md)

## 4단계: 최신 대상 내보내기 작업 ID 가져오기(v2에서는 필요하지 않음) {#segment-export-id}

>[!IMPORTANT]
>
>임시 활성화 API v2에서는 최신 대상 내보내기 작업 ID를 가져올 필요가 없습니다. 이 단계를 건너뛰고 다음 단계로 진행할 수 있습니다.

배치 대상에 대한 활성화 흐름을 구성하면 예약된 세분화 작업이 24시간마다 자동으로 실행됩니다.

임시 활성화 작업을 실행하려면 먼저 최신 대상자 내보내기 작업의 ID를 얻어야 합니다. 임시 활성화 작업 요청에서 이 ID를 전달해야 합니다.

[여기](../../segmentation/api/export-jobs.md#retrieve-list)에 설명된 지침에 따라 모든 대상자 내보내기 작업 목록을 검색합니다.

응답에서 아래의 스키마 속성을 포함하는 첫 번째 레코드를 찾습니다.

```
"schema":{
   "name":"_xdm.context.profile"
}
```

대상 내보내기 작업 ID는 아래와 같이 `id` 속성에 있습니다.

![대상 내보내기 작업 ID](../assets/api/ad-hoc-activation/segment-export-job-id.png)


## 5단계: 임시 활성화 작업 실행 {#activation-job}

Adobe Experience Platform은 예약된 세분화 작업을 24시간마다 한 번씩 실행합니다. 임시 활성화 API는 최신 세분화 결과를 기반으로 실행됩니다.

>[!IMPORTANT]
>
>다음 일회성 제한 사항을 참고하십시오. 임시 활성화 작업을 실행하기 전에, [3단계 - Experience Platform UI에서 활성화 흐름 만들기](#activation-flow)에서 설정한 일정에 따라 대상이 처음 활성화된 순간부터 최소 1시간이 경과되었는지 확인하십시오.

임시 활성화 작업을 실행하기 전에 대상에 대해 예약된 대상 내보내기 작업이 완료되었는지 확인하십시오. 활성화 흐름의 상태를 모니터링하는 방법에 대한 자세한 내용은 [대상 데이터 흐름 모니터링](../../dataflows/ui/monitor-destinations.md)을 참조하십시오. 예를 들어 활성화 데이터 흐름에서 **[!UICONTROL 처리 중]** 상태가 표시되면 임시 활성화 작업을 실행하여 전체 파일을 내보내기 전에 완료될 때까지 기다리십시오.

대상자 내보내기 작업이 완료되면 활성화를 트리거할 수 있습니다.

>[!NOTE]
>
>현재 각 임시 활성화 작업은 최대 80개의 대상을 활성화할 수 있습니다. 작업당 80개 이상의 대상을 활성화하려고 하면 작업이 실패합니다. 이 동작은 향후 릴리스에서 변경될 수 있습니다.

### 요청 {#request}

>[!IMPORTANT]
>
>임시 활성화 API의 v2를 사용하려면 요청에 `Accept: application/vnd.adobe.adhoc.activation+json; version=2` 헤더를 포함해야 합니다.

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/disflowprovider/adhocrun' \
--header 'x-gw-ims-org-id: 5555467B5D8013E50A494220@AdobeOrg' \
--header 'Authorization: Bearer {{token}}' \
--header 'x-sandbox-id: 6ef74723-3ee7-46a4-b747-233ee7a6a41a' \
--header 'x-sandbox-name: {sandbox-id}' \
--header 'Accept: application/vnd.adobe.adhoc.activation+json; version=2' \
--header 'Content-Type: application/json' \
--data-raw '{
   "activationInfo":{
      "destinationId1":[
         "segmentId1",
         "segmentId2"
      ],
      "destinationId2":[
         "segmentId2",
         "segmentId3"
      ]
   }
}'
```

| 속성 | 설명 |
| -------- | ----------- |
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | 대상자를 활성화할 대상 인스턴스의 ID입니다. **[!UICONTROL 대상]** > **[!UICONTROL 찾아보기]** 탭으로 이동한 다음 원하는 대상 행을 클릭하여 오른쪽 레일에서 대상 ID를 표시하면 Experience Platform UI에서 이러한 ID를 가져올 수 있습니다. 자세한 내용은 [대상 작업 영역 설명서](/help/destinations/ui/destinations-workspace.md#browse)를 참조하세요. |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | 선택한 대상에 활성화할 대상의 ID입니다. 임시 API를 사용하여 Experience Platform 생성 대상과 외부(사용자 지정 업로드) 대상을 내보낼 수 있습니다. 외부 대상을 활성화할 때 대상 ID 대신 시스템 생성 ID를 사용하십시오. 대상 UI의 대상 요약 보기에서 시스템 생성 ID를 찾을 수 있습니다. <br> ![선택할 수 없는 대상 ID 보기.](/help/destinations/assets/api/ad-hoc-activation/audience-id-do-not-use.png "선택하면 안 되는 대상 ID 보기."){width="100" zoomable="yes"} <br> ![사용해야 하는 시스템 생성 대상 ID 보기.](/help/destinations/assets/api/ad-hoc-activation/system-generated-id-to-use.png "사용해야 하는 시스템 생성 대상 ID를 봅니다."){width="100" zoomable="yes"} |

{style="table-layout:auto"}

### 내보내기 ID가 있는 요청 {#request-export-ids}

<!--

>[!IMPORTANT]
>
>**Deprecated request type**. This example type describes the request type for the API version 1. In the v2 of the ad-hoc activation API, you do not need to include the latest audience export job ID.

-->

```shell
curl -X POST https://platform.adobe.io/data/core/activation/disflowprovider/adhocrun \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -d '
{
   "activationInfo":{
      "destinationId1":[
         "segmentId1",
         "segmentId2"
      ],
      "destinationId2":[
         "segmentId2",
         "segmentId3"
      ]
   },
   "exportIds":[
      "exportId1"
   ]
}
```

| 속성 | 설명 |
| -------- | ----------- |
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | 대상자를 활성화할 대상 인스턴스의 ID입니다. **[!UICONTROL 대상]** > **[!UICONTROL 찾아보기]** 탭으로 이동한 다음 원하는 대상 행을 클릭하여 오른쪽 레일에서 대상 ID를 표시하면 Experience Platform UI에서 이러한 ID를 가져올 수 있습니다. 자세한 내용은 [대상 작업 영역 설명서](/help/destinations/ui/destinations-workspace.md#browse)를 참조하세요. |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | 선택한 대상에 활성화할 대상의 ID입니다. |
| <ul><li>`exportId1`</li></ul> | [대상 내보내기](../../segmentation/api/export-jobs.md#retrieve-list) 작업의 응답에서 반환된 ID입니다. 이 ID를 찾는 방법에 대한 지침은 [4단계: 최신 대상 내보내기 작업 ID 가져오기](#segment-export-id)를 참조하십시오. |

{style="table-layout:auto"}

### 응답 {#response}

성공적인 응답은 HTTP 상태 200을 반환합니다.

```shell
{
   "order":[
      {
         "segment":"db8961e9-d52f-45bc-b3fb-76d0382a6851",
         "order":"ef2dcbd6-36fc-49a3-afed-d7b8e8f724eb",
         "statusURL":"https://platform.adobe.io/data/foundation/flowservice/runs/88d6da63-dc97-460e-b781-fc795a7386d9"
      }
   ]
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `segment` | 활성화된 대상자의 ID입니다. |
| `order` | 대상이 활성화된 대상의 ID입니다. |
| `statusURL` | 활성화 흐름의 상태 URL입니다. [흐름 서비스 API](../../sources/tutorials/api/monitor.md)를 사용하여 흐름 진행 상황을 추적할 수 있습니다. |

{style="table-layout:auto"}

## API 오류 처리 {#api-error-handling}

Destination SDK API 엔드포인트는 일반적인 Experience Platform API 오류 메시지 원칙을 따릅니다. Experience Platform 문제 해결 안내서에서 [API 상태 코드](../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../landing/troubleshooting.md#request-header-errors)를 참조하십시오.

### Ad-hoc 활성화 API와 관련된 API 오류 코드 및 메시지 {#specific-error-messages}

임시 활성화 API를 사용하는 경우 이 API 끝점과 관련된 오류 메시지가 표시될 수 있습니다. 표가 표시될 때 이를 처리하는 방법을 이해하려면 표를 검토하십시오.

| 오류 메시지 | 해결 방법 |
|---------|----------|
| 실행 ID가 `flow run ID`인 주문 `dataflow ID`의 대상 `segment ID`에 대해 이미 실행 중입니다. | 이 오류 메시지는 대상에 대해 현재 임시 활성화 흐름이 진행 중임을 나타냅니다. 활성화 작업을 다시 트리거하기 전에 작업이 완료될 때까지 기다립니다. |
| `<segment name>` 세그먼트는 이 데이터 흐름의 일부가 아니거나 일정 범위를 벗어났습니다! | 이 오류 메시지는 활성화하기 위해 선택한 대상이 데이터 흐름에 매핑되지 않았거나 대상에 대해 설정된 활성화 일정이 만료되었거나 아직 시작되지 않았음을 나타냅니다. 대상이 데이터 흐름에 실제로 매핑되었는지 확인하고 대상 활성화 일정이 현재 날짜와 겹치는지 확인합니다. |

## 관련 정보 {#related-information}

* [흐름 서비스 API를 사용하여 배치 대상에 연결하고 데이터를 활성화합니다](/help/destinations/api/connect-activate-batch-destinations.md)
* [(Beta) Experience Platform UI를 사용하여 주문형 파일을 배치 대상으로 내보내기](/help/destinations/ui/export-file-now.md)