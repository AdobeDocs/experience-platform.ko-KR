---
keywords: Experience Platform;대상 api;애드혹 활성화;세그먼트 애드혹 활성화
solution: Experience Platform
title: 임시 활성화 API를 통해 대상자 세그먼트를 배치 대상으로 활성화
description: 이 문서에서는 활성화 전에 수행되는 세분화 작업을 포함하여 임시 활성화 API를 통해 대상 세그먼트를 활성화하기 위한 전체적인 워크플로를 보여 줍니다.
type: Tutorial
exl-id: 1a09f5ff-0b04-413d-a9f6-57911a92b4e4
source-git-commit: 1a7ba52b48460d77d0b7695aa0ab2d5be127d921
workflow-type: tm+mt
source-wordcount: '1554'
ht-degree: 1%

---

# 애드혹 활성화 API를 통해 대상 세그먼트를 배치 대상으로 온디맨드로 활성화합니다

>[!IMPORTANT]
>
>Beta 단계를 완료한 후 [!DNL ad-hoc activation API] 는 이제 모든 Experience Platform 고객에게 GA(General Available)됩니다. GA 버전에서 API가 버전 2로 업그레이드되었습니다. 4단계 ([최신 세그먼트 내보내기 작업 ID 얻기](#segment-export-id)API에 더 이상 내보내기 ID가 필요하지 않으므로 가 더 이상 필요하지 않습니다.
>
>다음을 참조하십시오 [임시 활성화 작업 실행](#activation-job) 자세한 내용은 이 자습서의 아래를 참조하십시오.

## 개요 {#overview}

임시 활성화 API를 사용하면 마케터가 즉각적인 활성화가 필요한 상황에 대해 대상 세그먼트를 빠르고 효율적으로 프로그래밍 방식으로 활성화할 수 있습니다.

임시 활성화 API를 사용하여 전체 파일을 원하는 파일 수신 시스템으로 내보냅니다. 임시 대상 활성화는에서 만 지원됩니다. [배치 파일 기반 대상](../destination-types.md#file-based).

아래 다이어그램은 24시간마다 플랫폼에서 수행되는 세분화 작업을 포함하여 임시 활성화 API를 통해 세그먼트를 활성화하기 위한 전체적인 워크플로를 보여 줍니다.

![애드혹 활성화](../assets/api/ad-hoc-activation/ad-hoc-activation-overview.png)



## 사용 사례 {#use-cases}

### Flash 판매 또는 프로모션

온라인 소매업체는 제한적인 플래시 세일을 준비하고 있으며 고객에게 빠른 공지로 알리기를 원합니다. 마케팅 팀은 Experience Platform 애드혹 활성화 API를 통해 온디맨드로 세그먼트를 내보내고 고객 기반으로 홍보 이메일을 신속하게 전송할 수 있습니다.

### 최신 이벤트 또는 속보

A호텔 측은 앞으로 며칠간 악천후가 예상되며, 해당 팀은 도착 손님들에게 신속히 알리기를 원하기 때문에 그에 맞는 계획을 세울 수 있다. 마케팅 팀은 Experience Platform 애드혹 활성화 API 를 사용하여 세그먼트를 온디맨드로 내보내고 게스트에게 알릴 수 있습니다.

### 통합 테스트

IT 관리자는 Experience Platform 임시 활성화 API를 사용하여 세그먼트를 온디맨드로 내보낼 수 있으므로 Adobe Experience Platform과의 사용자 정의 통합을 테스트하고 모든 것이 올바르게 작동하는지 확인할 수 있습니다.

## 가드레일 {#guardrails}

임시 활성화 API를 사용할 때는 다음 보호 기능에 유의하십시오.

* 현재 각 임시 활성화 작업은 최대 80개의 세그먼트를 활성화할 수 있습니다. 작업당 80개 이상의 세그먼트를 활성화하려고 하면 작업이 실패합니다. 이 동작은 향후 릴리스에서 변경될 수 있습니다.
* 임시 활성화 작업은 예약된 작업과 동시에 실행할 수 없습니다. [세그먼트 내보내기 작업](../../segmentation/api/export-jobs.md). 임시 활성화 작업을 실행하기 전에 예약된 세그먼트 내보내기 작업이 완료되었는지 확인하십시오. 다음을 참조하십시오 [대상 데이터 흐름 모니터링](../../dataflows/ui/monitor-destinations.md) 활성화 플로우 상태를 모니터링하는 방법에 대한 정보입니다. 예를 들어 활성화 데이터 흐름에 **[!UICONTROL 처리 중]** 상태를 확인하고 ad-hoc 활성화 작업을 실행하기 전에 작업이 완료될 때까지 기다리십시오.
* 세그먼트당 동시 임시 활성화 작업을 두 개 이상 실행하지 마십시오.

## 세그먼테이션 고려 사항 {#segmentation-considerations}

Adobe Experience Platform은 예약된 세분화 작업을 24시간마다 한 번씩 실행합니다. 임시 활성화 API는 최신 세분화 결과를 기반으로 실행됩니다.

## 1단계: 사전 요구 사항 {#prerequisites}

Adobe Experience Platform API를 호출하려면 먼저 다음 전제 조건을 충족하는지 확인하십시오.

* Adobe Experience Platform에 액세스할 수 있는 IMS 조직 계정이 있습니다.
* Experience Platform 계정에는 `developer` 및 `user` Adobe Experience Platform API 제품 프로필에 대해 활성화된 역할. 다음으로 연락 [Admin Console](../../access-control/home.md) 관리자가 귀하의 계정에 대해 이러한 역할을 활성화하도록 할 수 있습니다.
* Adobe ID이 있습니다. Adobe ID이 없는 경우 [Adobe Developer 콘솔](https://developer.adobe.com/console) 새 계정을 만듭니다.

## 2단계: 자격 증명 수집 {#credentials}

Platform API를 호출하려면 먼저 다음을 완료해야 합니다 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 아래와 같이 모든 Experience Platform API 호출에서 필요한 각 헤더의 값이 제공됩니다.

* 인증: 전달자 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Experience Platform의 리소스는 특정 가상 샌드박스로 격리될 수 있습니다. Platform API에 대한 요청에서 작업이 수행될 샌드박스의 이름과 ID를 지정할 수 있습니다. 이러한 매개 변수는 선택 사항입니다.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Experience Platform의 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md).

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에는 추가 미디어 유형 헤더가 필요합니다.

* Content-Type: `application/json`

## 3단계: Platform UI에서 활성화 흐름 만들기 {#activation-flow}

Ad-hoc 활성화 API를 통해 세그먼트를 활성화하려면 먼저 선택한 대상에 대해 Platform UI에 활성화 흐름이 구성되어 있어야 합니다.

여기에는 활성화 워크플로, 세그먼트 선택, 일정 구성 및 활성화가 포함됩니다. UI 또는 API를 사용하여 활성화 플로우를 만들 수 있습니다.

* [Platform UI를 사용하여 프로필 내보내기 대상을 일괄 처리하는 활성화 플로우를 만듭니다](../ui/activate-batch-profile-destinations.md)
* [흐름 서비스 API를 사용하여 프로필 내보내기 대상 일괄 연결에 연결하고 데이터를 활성화합니다](../api/connect-activate-batch-destinations.md)

## 4단계: 최신 세그먼트 내보내기 작업 ID 가져오기(v2에서는 필요하지 않음) {#segment-export-id}

>[!IMPORTANT]
>
>Ad-hoc 활성화 API v2에서는 최신 세그먼트 내보내기 작업 ID를 가져올 필요가 없습니다. 이 단계를 건너뛰고 다음 단계로 진행할 수 있습니다.

배치 대상에 대한 활성화 흐름을 구성하면 예약된 세분화 작업이 24시간마다 자동으로 실행됩니다.

임시 활성화 작업을 실행하려면 먼저 최신 세그먼트 내보내기 작업의 ID를 가져와야 합니다. 임시 활성화 작업 요청에서 이 ID를 전달해야 합니다.

설명된 지침을 따르십시오 [여기](../../segmentation/api/export-jobs.md#retrieve-list) 모든 세그먼트 내보내기 작업 목록을 검색합니다.

응답에서 아래의 스키마 속성을 포함하는 첫 번째 레코드를 찾습니다.

```
"schema":{
   "name":"_xdm.context.profile"
}
```

세그먼트 내보내기 작업 ID는 `id` 속성(아래 참조).

![세그먼트 내보내기 작업 ID](../assets/api/ad-hoc-activation/segment-export-job-id.png)


## 5단계: 임시 활성화 작업 실행 {#activation-job}

Adobe Experience Platform은 예약된 세분화 작업을 24시간마다 한 번씩 실행합니다. 임시 활성화 API는 최신 세분화 결과를 기반으로 실행됩니다.

>[!IMPORTANT]
>
>다음 일회성 제한 사항 참고: 임시 활성화 작업을 실행하기 전에, 설정한 일정에 따라 세그먼트가 처음 활성화된 순간부터 최소 20분이 경과되었는지 확인하십시오 [3단계 - Platform UI에서 활성화 흐름 만들기](#activation-flow).

임시 활성화 작업을 실행하기 전에 세그먼트에 대해 예약된 세그먼트 내보내기 작업이 완료되었는지 확인하십시오. 다음을 참조하십시오 [대상 데이터 흐름 모니터링](../../dataflows/ui/monitor-destinations.md) 활성화 플로우 상태를 모니터링하는 방법에 대한 정보입니다. 예를 들어 활성화 데이터 흐름에 **[!UICONTROL 처리 중]** 상태, 전체 파일을 내보내기 위해 임시 활성화 작업을 실행하기 전에 완료될 때까지 기다립니다.

세그먼트 내보내기 작업이 완료되면 활성화를 트리거할 수 있습니다.

>[!NOTE]
>
>현재 각 임시 활성화 작업은 최대 80개의 세그먼트를 활성화할 수 있습니다. 작업당 80개 이상의 세그먼트를 활성화하려고 하면 작업이 실패합니다. 이 동작은 향후 릴리스에서 변경될 수 있습니다.

### 요청 {#request}

>[!IMPORTANT]
>
>다음을 포함해야 합니다. `Accept: application/vnd.adobe.adhoc.activation+json; version=2` ad-hoc activation API v2를 사용하기 위한 요청의 헤더.

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
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | 세그먼트를 활성화할 대상 인스턴스의 ID입니다. Platform UI에서 로 이동하여 이러한 ID를 가져올 수 있습니다. **[!UICONTROL 대상]** > **[!UICONTROL 찾아보기]** 을 탭하고 원하는 대상 행을 클릭하여 오른쪽 레일에서 대상 ID를 표시합니다. 자세한 내용은 [대상 작업 영역 설명서](/help/destinations/ui/destinations-workspace.md#browse). |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | 선택한 대상에 활성화할 세그먼트의 ID입니다. |

{style="table-layout:auto"}

### 내보내기 ID를 사용하는 요청(더 이상 사용되지 않음) {#request-deprecated}

>[!IMPORTANT]
>
>**더 이상 사용되지 않는 요청 유형**. 이 예제 유형은 API 버전 1의 요청 유형을 설명합니다. 임시 활성화 API v2에서는 최신 세그먼트 내보내기 작업 ID를 포함할 필요가 없습니다.

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
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | 세그먼트를 활성화할 대상 인스턴스의 ID입니다. Platform UI에서 로 이동하여 이러한 ID를 가져올 수 있습니다. **[!UICONTROL 대상]** > **[!UICONTROL 찾아보기]** 을 탭하고 원하는 대상 행을 클릭하여 오른쪽 레일에서 대상 ID를 표시합니다. 자세한 내용은 [대상 작업 영역 설명서](/help/destinations/ui/destinations-workspace.md#browse). |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | 선택한 대상에 활성화할 세그먼트의 ID입니다. |
| <ul><li>`exportId1`</li></ul> | 의 응답에서 반환된 ID [세그먼트 내보내기](../../segmentation/api/export-jobs.md#retrieve-list) 작업. 다음을 참조하십시오 [4단계: 최신 세그먼트 내보내기 작업 ID 가져오기](#segment-export-id) 이 ID를 찾는 방법에 대한 지침입니다. |

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
| `segment` | 활성화된 세그먼트의 ID. |
| `order` | 세그먼트가 활성화된 대상의 ID입니다. |
| `statusURL` | 활성화 흐름의 상태 URL입니다. 다음을 사용하여 플로우 진행률을 추적할 수 있습니다. [플로우 서비스 API](../../sources/tutorials/api/monitor.md). |

{style="table-layout:auto"}

## API 오류 처리 {#api-error-handling}

Destination SDK API 엔드포인트는 일반적인 Experience Platform API 오류 메시지 원칙을 따릅니다. 을(를) 참조하십시오 [API 상태 코드](../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../landing/troubleshooting.md#request-header-errors) 플랫폼 문제 해결 안내서에서 확인할 수 있습니다.

### Ad-hoc 활성화 API와 관련된 API 오류 코드 및 메시지 {#specific-error-messages}

임시 활성화 API를 사용하는 경우 이 API 끝점과 관련된 오류 메시지가 표시될 수 있습니다. 표가 표시될 때 이를 처리하는 방법을 이해하려면 표를 검토하십시오.

| 오류 메시지 | 해결 방법 |
|---------|----------|
| 세그먼트에 대한 실행이 이미 진행 중입니다. `segment ID` 주문용 `dataflow ID` 실행 id 사용 `flow run ID` | 이 오류 메시지는 세그먼트에 대해 임시 활성화 흐름이 현재 진행 중임을 나타냅니다. 활성화 작업을 다시 트리거하기 전에 작업이 완료될 때까지 기다립니다. |
| 세그먼트 `<segment name>` 은(는) 이 데이터 흐름의 일부가 아니거나 일정 범위를 벗어났습니다! | 이 오류 메시지는 활성화하기 위해 선택한 세그먼트가 데이터 흐름에 매핑되지 않았거나 세그먼트에 대해 설정된 활성화 일정이 만료되었거나 아직 시작되지 않았음을 나타냅니다. 세그먼트가 데이터 흐름에 실제로 매핑되었는지 확인하고 세그먼트 활성화 일정이 현재 날짜와 겹치는지 확인합니다. |

## 관련 정보 {#related-information}

* [흐름 서비스 API를 사용하여 배치 대상에 연결하고 데이터를 활성화합니다](/help/destinations/api/connect-activate-batch-destinations.md)
* [(베타) Experience Platform UI를 사용하여 주문형 파일을 배치 대상으로 내보내기](/help/destinations/ui/export-file-now.md)