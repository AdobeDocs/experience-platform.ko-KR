---
keywords: Experience Platform;홈;인기 항목;데이터 수집 알림;알림;가입 이벤트;데이터 수집 상태 이벤트;상태 이벤트;가입;상태 알림;
solution: Experience Platform
title: 데이터 수집 알림
topic-legacy: overview
description: 수집 프로세스 모니터링을 지원하기 위해 Adobe Experience Platform에서는 프로세스의 각 단계에서 게시되는 이벤트 세트에 가입할 수 있으므로 수집된 데이터의 상태와 가능한 오류를 알려줍니다.
exl-id: fd34e1ab-f6f6-44f0-88ee-7020e9322c39
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '677'
ht-degree: 2%

---

# 데이터 수집 알림

데이터를 Adobe Experience Platform에 수집하는 프로세스는 여러 단계로 구성됩니다. 수집해야 하는 데이터 파일을 식별하면 [!DNL Platform]: 수집 프로세스가 시작되고 데이터가 성공적으로 수집되거나 실패할 때까지 각 단계가 연속적으로 발생합니다. 수집 프로세스는 [Adobe Experience Platform 데이터 수집 API](https://www.adobe.io/experience-platform-apis/references/data-ingestion/) 또는 [!DNL Experience Platform] 사용자 인터페이스.

에 로드된 데이터 [!DNL Platform] 목적지에 도달하려면 여러 단계를 수행해야 합니다. [!DNL Data Lake] 또는 [!DNL Real-Time Customer Profile] 데이터 저장소. 각 단계에는 데이터를 처리하고, 데이터를 확인한 다음, 다음 단계로 전달하기 전에 데이터를 저장하는 작업이 포함됩니다. 수집되는 데이터의 양에 따라 시간이 많이 소요되는 프로세스가 될 수 있으며 유효성 검사, 의미 체계 또는 처리 오류로 인해 프로세스가 실패할 가능성이 항상 있습니다. 오류가 발생하는 경우 데이터 문제를 수정한 후 수정된 데이터 파일을 사용하여 전체 수집 프로세스를 다시 시작해야 합니다.

수집 프로세스 모니터링을 지원하려면 [!DNL Experience Platform] 에서는 프로세스의 각 단계에서 게시한 이벤트 세트에 가입할 수 있도록 하여 수집된 데이터의 상태와 가능한 오류를 알려줍니다.

## 데이터 수집 알림에 웹 후크 등록

데이터 수집 알림을 수신하려면 [Adobe Developer 콘솔](https://www.adobe.com/go/devs_console_ui) Experience Platform 통합에 웹 후크를 등록하려면

다음의 자습서를 따르십시오 [구독 [!DNL Adobe I/O Event] 알림](../../observability/alerts/subscribe.md) 를 참조하십시오.

>[!IMPORTANT]
>
>구독 프로세스 중에 **[!UICONTROL 플랫폼 알림]** 을 이벤트 공급자로 선택하고 **[!UICONTROL 데이터 수집 알림]** 이벤트 구독 메시지가 표시되면

## 데이터 수집 알림 수신

웹 후크를 등록했고 새 데이터를 수집하면 이벤트 알림 수신을 시작할 수 있습니다. 이러한 이벤트는 웹 후크 자체를 사용하거나 **[!UICONTROL 디버그 추적]** Adobe Developer 콘솔에서 프로젝트의 이벤트 등록 개요에 있는 탭입니다.

다음 JSON은 실패한 배치 수집 이벤트의 경우 웹 후크에 전송되는 알림 페이로드의 예입니다.

```json
{
  "event_id": "93a5b11a-b0e6-4b29-ad82-81b1499cb4f2",
  "event": {
    "xdm:ingestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:customerIngestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:imsOrg": "{ORG_ID}",
    "xdm:completed": 1598374341560,
    "xdm:datasetId": "5e55b556c2ae4418a8446037",
    "xdm:eventCode": "ing_load_failure",
    "xdm:sandboxName": "prod",
    "sentTime": "1598374341595",
    "processStartTime": 1598374342614,
    "transformedTime": 1598374342621,
    "header": {
      "_adobeio": {
        "imsOrgId": "{ORG_ID}",
        "providerMetadata": "aep_observability_catalog_events",
        "eventCode": "platform_event"
      }
    }
  }
}
```

| 속성 | 설명 |
| --- | --- |
| `event_id` | 알림에 대한 고유한 시스템 생성 ID입니다. |
| `event` | 알림을 트리거한 이벤트의 세부 정보가 포함된 객체입니다. |
| `event.xdm:datasetId` | 수집 이벤트가 적용되는 데이터 세트의 ID입니다. |
| `event.xdm:eventCode` | 데이터 집합에 대해 트리거된 이벤트 유형을 나타내는 상태 코드입니다. 자세한 내용은 [부록](#event-codes) 참조하십시오. |

이벤트 알림에 대한 전체 스키마를 보려면 [공용 GitHub 리포지토리](https://github.com/adobe/xdm/blob/master/schemas/notifications/ingestion.schema.json).

## 다음 단계

등록했으면 [!DNL Platform] 프로젝트에 대한 알림에서는 [!UICONTROL 프로젝트 개요]. 다음 안내서를 참조하십시오. [추적 Adobe I/O 이벤트](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md) 를 참조하십시오.

## 부록

다음 섹션에는 데이터 수집 알림 페이로드 해석에 대한 추가 정보가 포함되어 있습니다.

### 사용 가능한 상태 알림 이벤트 {#event-codes}

다음 표에는 구독할 수 있는 사용 가능한 데이터 수집 상태 알림이 나열되어 있습니다.

| 이벤트 코드 | 플랫폼 서비스 | 상태 | 이벤트 설명 |
| --- | ---------------- | ------ | ----------------- |
| `ing_load_success` | [!DNL Data Ingestion] | success | 일괄 처리가 [!DNL Data Lake]. |
| `ing_load_failure` | [!DNL Data Ingestion] | 실패 | 일괄 처리를 [!DNL Data Lake]. |
| `ps_load_success` | [!DNL Real-Time Customer Profile] | success | 일괄 처리를 [!DNL Profile] 데이터 저장소. |
| `ps_load_failure` | [!DNL Real-Time Customer Profile] | 실패 | 일괄 처리를 [!DNL Profile] 데이터 저장소. |
| `ig_load_success` | [!DNL Identity Service] | success | 데이터가 ID 그래프에 로드되었습니다. |
| `ig_load_failure` | [!DNL Identity Service] | 실패 | 데이터를 ID 그래프에 로드하지 못했습니다. |

>[!NOTE]
>
>모든 데이터 수집 알림에 대해 제공되는 이벤트 항목은 하나뿐입니다. 서로 다른 상태를 구분하기 위해 이벤트 코드를 사용할 수 있습니다.
