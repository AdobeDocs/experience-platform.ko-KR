---
keywords: Experience Platform;대상 api;임시 활성화;임시 세그먼트 활성화
solution: Experience Platform
title: (베타) 임시 활성화 API를 통해 대상자 세그먼트를 배치 대상에 활성화합니다
description: 이 문서에서는 활성화 전에 발생하는 세분화 작업을 포함하여 임시 활성화 API를 통해 대상 세그먼트를 활성화하는 종단 간 워크플로우를 보여줍니다.
topic-legacy: tutorial
type: Tutorial
source-git-commit: 749fa5dc1e8291382408d9b1a0391c4c7f2b2a46
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 2%

---


# (베타) 임시 활성화 API를 통해 대상자 세그먼트를 배치 대상에 활성화합니다

>[!IMPORTANT]
>
>다음 [!DNL ad-hoc activation API] in Platform은 현재 베타 버전입니다. 설명서 및 기능은 변경될 수 있습니다.

## 개요 {#overview}

Ad-hoc 활성화 API를 사용하면 즉시 활성화해야 하는 상황에서 마케터는 빠르고 효율적인 방식으로 대상 세그먼트를 대상으로 프로그래밍 방식으로 활성화할 수 있습니다.

The diagram below illustrates the end-to-end workflow for activating segments via the ad-hoc activation API, including the segmentation jobs that take place in Platform every 24 hours.

![ad-hoc-activation](../assets/api/ad-hoc-activation/ad-hoc-activation-overview.png)

>[!NOTE]
>
>임시 대상 활성화는 [배치 파일 기반 대상](../destination-types.md#file-based).

## 사용 사례 {#use-cases}

### Flash 판매 또는 프로모션

An online retailer is preparing a limited flash sale and wants to notify customers on a short notice. Through the Experience Platform ad-hoc activation API, the marketing team can export segments on-demand, and quickly send promotional emails to the customer base.


### 현재 이벤트 또는 최신 뉴스

A hotel expects inclement weather over the following days, and the team wants to inform the arriving guests quickly, so they can plan accordingly. The marketing team can use the Experience Platform ad-hoc activation API to export segments on-demand, and notify the guests.

### 통합 테스트

IT 관리자는 Experience Platform Ad-Hoc 활성화 API를 사용하여 세그먼트를 온디맨드(on-demand)로 내보낼 수 있으므로 Adobe Experience Platform와의 사용자 지정 통합을 테스트하고 모든 것이 올바르게 작동하는지 확인할 수 있습니다.


## 가드레일 {#guardrails}

임시 활성화 API를 사용할 때는 다음과 같은 보호 기능을 기억하십시오.

* Currently, each ad-hoc activation job can activate up to 20 segments. 작업당 20개 이상의 세그먼트를 활성화하려고 하면 작업이 실패합니다. 이 동작은 향후 릴리스에서 변경될 수 있습니다.
* Ad-hoc activation jobs cannot run in parallel with scheduled [segment export jobs](../../segmentation/api/export-jobs.md). 임시 활성화 작업을 실행하기 전에 예약된 세그먼트 내보내기 작업이 완료되었는지 확인하십시오. See [destination dataflow monitoring](../../dataflows/ui/monitor-destinations.md) for information on how to monitor the status of activation flows. 예를 들어 활성화 데이터 양이 **[!UICONTROL 처리 중]** 상태, ad-hoc 활성화 작업을 실행하기 전에 완료될 때까지 기다립니다.
* Do not run more than one concurrrent ad-hoc activation job per segment.

## Segmentation considerations {#segmentation-considerations}

Adobe Experience Platform은 24시간마다 예약된 세그먼테이션 작업을 실행합니다. 임시 활성화 API는 최신 세분화 결과를 기반으로 실행됩니다.

## 1단계: 전제 조건 {#prerequisites}

Before you can make calls to the Adobe Experience Platform APIs, make sure you meet the following prerequisites:

* You have an IMS Organization account with access to Adobe Experience Platform.
* Experience Platform 계정에는 `developer` 및 `user` Adobe Experience Platform API 제품 프로필에 대해 활성화된 역할. Contact your [Admin Console](../../access-control/home.md) administrator to enable these roles for your account.
* Adobe ID이 있습니다. Adobe ID이 없는 경우 [Adobe 개발자 콘솔](https://developer.adobe.com/console) 새 계정을 만듭니다.

## 2단계: 자격 증명 수집 {#credentials}

In order to make calls to Platform APIs, you must first complete the [authentication tutorial](https://www.adobe.com/go/platform-api-authentication-en). 인증 자습서를 완료하면 아래와 같이 모든 Experience Platform API 호출에서 각 필수 헤더에 대한 값을 제공합니다.

* 권한 부여: 베어러 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Resources in Experience Platform can be isolated to specific virtual sandboxes. In requests to Platform APIs, you can specify the name and ID of the sandbox that the operation will take place in. 선택적 매개 변수입니다.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>For more information on sandboxes in Experience Platform, see the [sandbox overview documentation](../../sandboxes/home.md).

All requests that contain a payload (POST, PUT, PATCH) require an additional media type header:

* Content-Type: `application/json`

## 3단계: 플랫폼 UI에서 활성화 흐름 만들기 {#activation-flow}

임시 활성화 API를 통해 세그먼트를 활성화하려면 먼저 선택한 대상에 대해 플랫폼 UI에 활성화 플로우가 구성되어 있어야 합니다.

This includes going into the activation workflow, selecting your segments, configuring a schedule, and activating them.

배치 대상에 대한 활성화 흐름을 구성하는 방법에 대한 자세한 지침은 다음 자습서를 참조하십시오. [대상자 데이터를 활성화하여 묶음 프로필 내보내기 대상 활성화](../ui/activate-batch-profile-destinations.md).

## Step 4: Obtain the latest segment export job ID {#segment-export-id}

배치 대상에 대한 활성화 흐름을 구성한 후 24시간마다 예약된 세그먼테이션 작업이 자동으로 실행됩니다.

Before you can run the ad-hoc activation job, you must obtain the ID of the latest segment export job. 임시 활성화 작업 요청에서 이 ID를 전달해야 합니다.

Follow the instructions described [here](../../segmentation/api/export-jobs.md#retrieve-list) to retrieve a list of all the segment export jobs.

In the response, look for the first record that includes the schema property below.

```
"schema":{
   "name":"_xdm.context.profile"
}
```

The segment export job ID is in the `id` property, as shown below.

![세그먼트 내보내기 작업 ID](../assets/api/ad-hoc-activation/segment-export-job-id.png)


## 5단계: 임시 활성화 작업 실행 {#activation-job}

Adobe Experience Platform은 24시간마다 예약된 세그먼테이션 작업을 실행합니다. 임시 활성화 API는 최신 세분화 결과를 기반으로 실행됩니다.

임시 활성화 작업을 실행하기 전에 세그먼트에 대해 예약된 세그먼트 내보내기 작업이 완료되었는지 확인하십시오. See [destination dataflow monitoring](../../dataflows/ui/monitor-destinations.md) for information on how to monitor the status of activation flows. For example, if your activation dataflow shows a **[!UICONTROL Processing]** status, wait for it to finish before running the ad-hoc activation job.

Once the segment export job has completed, you can trigger the activation.

>[!NOTE]
>
>Currently, each ad-hoc activation job can activate up to 20 segments. Attempting to activate more than 20 segments per job will cause the job to fail. This behavior is subject to change in future releases.

### 요청

```shell
curl -X POST https://platform.adobe.io/data/core/activation/disflowprovider/adhocrun \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | 세그먼트를 활성화할 대상 인스턴스의 ID입니다. |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | 선택한 대상으로 활성화할 세그먼트의 ID입니다. |
| <ul><li>`exportId1`</li></ul> | 의 응답으로 반환된 ID입니다 [세그먼트 내보내기](../../segmentation/api/export-jobs.md#retrieve-list) 작업. 자세한 내용은 [4단계: 최신 세그먼트 내보내기 작업 ID 가져오기](#segment-export-id) 를 참조하십시오. |

### 응답

A successful response returns HTTP status 200.

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
| `segment` | 활성화된 세그먼트의 ID입니다. |
| `order` | 세그먼트가 활성화된 대상의 ID입니다. |
| `statusURL` | 활성화 흐름의 상태 URL입니다. 를 사용하여 흐름 진행률을 추적할 수 있습니다 [Flow Service API](../../sources/tutorials/api/monitor.md). |


## API 오류 처리

대상 SDK API 엔드포인트는 일반 Experience Platform API 오류 메시지 원칙을 따릅니다. 을(를) 참조하십시오. [API 상태 코드](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) 및 [요청 헤더 오류](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) 을 참조하십시오.
