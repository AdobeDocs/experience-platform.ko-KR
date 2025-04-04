---
keywords: Experience Platform;홈;인기 항목;데이터 수집 알림;알림;이벤트 구독;데이터 수집 상태 이벤트;상태 이벤트;구독;상태 알림;
solution: Experience Platform
title: 데이터 수집 알림
description: 수집 프로세스 모니터링을 지원하기 위해 Adobe Experience Platform에서는 프로세스의 각 단계에서 게시되는 이벤트 세트를 구독하여 수집된 데이터의 상태와 가능한 오류를 알릴 수 있습니다.
exl-id: fd34e1ab-f6f6-44f0-88ee-7020e9322c39
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 1%

---

# 데이터 수집 알림

Adobe Experience Platform으로 데이터를 수집하는 프로세스는 여러 단계로 구성됩니다. [!DNL Experience Platform]에 수집해야 하는 데이터 파일을 식별하면 수집 프로세스가 시작되고 데이터가 성공적으로 수집되거나 실패할 때까지 각 단계가 연속적으로 발생합니다. [Adobe Experience Platform 일괄 처리 수집 API](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)를 사용하거나 [!DNL Experience Platform] 사용자 인터페이스를 사용하여 수집 프로세스를 시작할 수 있습니다.

[!DNL Experience Platform]에 로드된 데이터는 해당 대상, [!DNL Data Lake] 또는 [!DNL Real-Time Customer Profile] 데이터 저장소에 도달하려면 여러 단계를 거쳐야 합니다. 각 단계에는 데이터를 처리하고, 데이터의 유효성을 검사한 다음, 데이터를 다음 단계로 전달하기 전에 저장하는 작업이 포함됩니다. 수집하는 데이터의 양에 따라 시간이 오래 걸리는 프로세스가 될 수 있으며 유효성 검사, 의미 체계 또는 처리 오류로 인해 프로세스가 실패할 가능성이 항상 있습니다. 장애가 발생하면 데이터 문제를 해결한 다음 수정된 데이터 파일을 사용하여 전체 수집 프로세스를 다시 시작해야 합니다.

수집 프로세스를 모니터링하기 위해 [!DNL Experience Platform]을(를) 사용하면 프로세스의 각 단계에서 게시되는 이벤트 집합을 구독하여 수집된 데이터의 상태와 가능한 오류를 알릴 수 있습니다.

## 데이터 수집 알림을 위한 웹후크 등록

데이터 수집 알림을 받으려면 [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui)을 사용하여 Experience Platform 통합에 웹후크를 등록해야 합니다.

이를 수행하는 방법에 대한 자세한 단계는 [구독 [!DNL Adobe I/O Event] 알림](../../observability/alerts/subscribe.md)에 대한 자습서를 참조하십시오.

>[!IMPORTANT]
>
>가입 프로세스 중에 이벤트 공급자로 **[!UICONTROL 플랫폼 알림]**&#x200B;을 선택하고 메시지가 표시되면 **[!UICONTROL 데이터 수집 알림]** 이벤트 가입을 선택하십시오.

## 데이터 수집 알림 수신

Webhook을 성공적으로 등록하고 새 데이터를 수집하면 이벤트 알림을 받을 수 있습니다. 이러한 이벤트는 웹후크 자체를 사용하거나 Adobe Developer Console에서 프로젝트의 이벤트 등록 개요에서 **[!UICONTROL 추적 디버그]** 탭을 선택하여 볼 수 있습니다.

다음 JSON은 일괄 처리 수집 이벤트 실패 시 웹 후크로 전송되는 알림 페이로드의 예입니다.

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
| `event_id` | 알림에 대한 시스템 생성 고유 ID. |
| `event` | 알림을 트리거한 이벤트의 세부 사항이 포함된 객체입니다. |
| `event.xdm:datasetId` | 수집 이벤트가 적용되는 데이터 세트의 ID입니다. |
| `event.xdm:eventCode` | 데이터 세트에 대해 트리거된 이벤트 유형을 나타내는 상태 코드입니다. 특정 값과 해당 정의에 대해서는 [부록](#event-codes)을 참조하십시오. |

이벤트 알림에 대한 전체 스키마를 보려면 [공개 GitHub 저장소](https://github.com/adobe/xdm/blob/master/schemas/notifications/ingestion.schema.json)를 참조하세요.

## 다음 단계

프로젝트에 [!DNL Experience Platform]개의 알림을 등록하면 [!UICONTROL 프로젝트 개요]에서 받은 이벤트를 볼 수 있습니다. 이벤트를 추적하는 방법에 대한 자세한 지침은 [Adobe I/O Events 추적](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md)에 대한 안내서를 참조하세요.

## 부록

다음 섹션에는 데이터 수집 알림 페이로드 해석에 대한 추가 정보가 포함되어 있습니다.

### 사용 가능한 상태 알림 이벤트 {#event-codes}

다음 표에는 가입할 수 있는 사용 가능한 데이터 수집 상태 알림이 나열되어 있습니다.

| 이벤트 코드 | Experience Platform 서비스 | 상태 | 이벤트 설명 |
| --- | ---------------- | ------ | ----------------- |
| `ing_load_success` | [!DNL Data Ingestion] | 성공 | 배치가 [!DNL Data Lake] 내의 데이터 세트로 수집되었습니다. |
| `ing_load_failure` | [!DNL Data Ingestion] | 실패 | 일괄 처리를 [!DNL Data Lake] 내의 데이터 세트로 수집하지 못했습니다. |
| `ps_load_success` | [!DNL Real-Time Customer Profile] | 성공 | 일괄 처리가 [!DNL Profile] 데이터 저장소에 수집되었습니다. |
| `ps_load_failure` | [!DNL Real-Time Customer Profile] | 실패 | 일괄 처리를 [!DNL Profile] 데이터 저장소에 수집하지 못했습니다. |
| `ig_load_success` | [!DNL Identity Service] | 성공 | 데이터가 ID 그래프에 성공적으로 로드되었습니다. |
| `ig_load_failure` | [!DNL Identity Service] | 실패 | ID 그래프로 데이터를 로드하지 못했습니다. |

>[!NOTE]
>
>모든 데이터 수집 알림에 대해 제공되는 이벤트 주제는 하나만 있습니다. 상이한 상태를 구별하기 위해, 이벤트 코드가 사용될 수 있다.
