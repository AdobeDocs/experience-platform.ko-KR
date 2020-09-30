---
keywords: Experience Platform;home;popular topics;data ingestion notifications;notifications;subscribe events;data ingestion status events;status events;subscribe;status notifications;
solution: Experience Platform
title: 데이터 수집 이벤트 가입
topic: overview
description: 수집 프로세스 모니터링을 지원하기 위해, Adobe Experience Platform은 프로세스의 각 단계에 의해 게시된 일련의 이벤트에 가입할 수 있도록 하여, 인제스트된 데이터의 상태 및 발생 가능한 실패를 사용자에게 알립니다.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '663'
ht-degree: 2%

---


# 데이터 수집 알림

데이터를 Adobe Experience Platform에 수집하는 프로세스는 여러 단계로 구성됩니다. 인제스트해야 하는 데이터 파일을 식별하면 수집 프로세스 [!DNL Platform]가 시작되고 데이터가 성공적으로 인제스트되거나 실패할 때까지 각 단계가 연속적으로 수행됩니다. 수집 프로세스는 [Adobe Experience Platform 데이터 통합 API를](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) 사용하거나 [!DNL Experience Platform] 사용자 인터페이스를 사용하여 시작할 수 있습니다.

로 로드된 데이터는 대상, [!DNL Platform] 또는 [!DNL Data Lake] [!DNL Real-time Customer Profile] 데이터 저장소에 도달하려면 여러 단계를 거쳐야 합니다. 각 단계에는 데이터를 처리하고, 데이터의 유효성을 검사한 다음 다음 다음 단계로 전달하기 전에 데이터를 저장하는 작업이 포함됩니다. 수집되는 데이터의 양에 따라 시간이 많이 소요되기 때문에 유효성 검사, 의미 체계 또는 처리 오류로 인해 프로세스가 실패할 가능성이 항상 있습니다. 오류가 발생한 경우 데이터 문제를 해결해야 하며 수정된 데이터 파일을 사용하여 전체 처리 과정을 다시 시작해야 합니다.

수집 프로세스 모니터링을 지원하기 위해, [!DNL Experience Platform] 인제스트된 데이터의 상태 및 발생 가능한 실패를 알려 주기 위해 프로세스의 각 단계에 의해 게시된 일련의 이벤트에 가입할 수 있습니다.

## 데이터 통합 알림에 대한 웹 후크 등록

데이터 통합 알림을 수신하려면 [Adobe 개발자 콘솔을](https://www.adobe.com/go/devs_console_ui) 사용하여 Experience Platform 통합에 웹 후크를 등록해야 합니다.

가입 [방법에 대한 자세한 [!DNL Adobe I/O Event] 내용은](../../observability/notifications/subscribe.md) 설정에 대한 자습서를따르십시오.

>[!IMPORTANT]
>
>구독 프로세스 동안 **[!UICONTROL 플랫폼 알림을]** 이벤트 제공자로 선택하고 메시지가 표시되었을 때 **[!UICONTROL 데이터 통합 알림]** 이벤트 구독을 선택합니다.

## 데이터 수집 알림 받기

웹 후크를 등록했고 새 데이터가 인제스트되면 이벤트 알림 수신을 시작할 수 있습니다. 이러한 이벤트는 웹 후크 자체를 사용하거나 Adobe 개발자 콘솔에서 프로젝트의 이벤트 등록 개요에서 **[!UICONTROL 디버그 추적]** 탭을 선택하여 볼 수 있습니다.

다음 JSON은 실패한 일괄 처리 통합 이벤트의 경우 웹 후크에 전송되는 알림 페이로드의 예입니다.

```json
{
  "event_id": "93a5b11a-b0e6-4b29-ad82-81b1499cb4f2",
  "event": {
    "xdm:ingestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:customerIngestionId": "01EGK8H8HF9JGFKNDCABHGA24G",
    "xdm:imsOrg": "{IMS_ORG}",
    "xdm:completed": 1598374341560,
    "xdm:datasetId": "5e55b556c2ae4418a8446037",
    "xdm:eventCode": "ing_load_failure",
    "xdm:sandboxName": "prod",
    "sentTime": "1598374341595",
    "processStartTime": 1598374342614,
    "transformedTime": 1598374342621,
    "header": {
      "_adobeio": {
        "imsOrgId": "{IMS_ORG}",
        "providerMetadata": "aep_observability_catalog_events",
        "eventCode": "platform_event"
      }
    }
  }
}
```

| 속성 | 설명 |
| --- | --- |
| `event_id` | 알림을 위한 고유한 시스템 생성 ID. |
| `event` | 알림을 트리거한 이벤트의 세부 정보가 포함된 개체입니다. |
| `event.xdm:datasetId` | 통합 이벤트가 적용되는 데이터 세트의 ID입니다. |
| `event.xdm:eventCode` | 데이터 세트에 대해 트리거된 이벤트 유형을 나타내는 상태 코드입니다. 특정 값과 [그 정의에 대해서는 부록을](#event-codes) 참조하십시오. |

이벤트 알림의 전체 스키마를 보려면 [공용 GitHub 리포지토리를 참조하십시오](https://github.com/adobe/xdm/blob/master/schemas/notifications/ingestion.schema.json).

## 다음 단계

프로젝트에 [!DNL Platform] 알림을 등록하면 [!UICONTROL 프로젝트 개요에서 받은 이벤트를 볼 수 있습니다]. 이벤트 추적 방법에 대한 자세한 내용은 [Adobe I/O 이벤트](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/support/tracing.md) 추적 가이드를 참조하십시오.

## 부록

다음 섹션에는 데이터 통합 알림 페이로드 해석에 대한 추가 정보가 포함되어 있습니다.

### 사용 가능한 상태 알림 이벤트 {#event-codes}

다음 표에는 가입할 수 있는 데이터 통합 상태 알림이 나열됩니다.

| 이벤트 코드 | 플랫폼 서비스 | 상태 | 이벤트 설명 |
| --- | ---------------- | ------ | ----------------- |
| `ing_load_success` | [!DNL Data Ingestion] | 성공 | 일괄 처리를 데이터 세트에 성공적으로 [!DNL Data Lake]수집했습니다. |
| `ing_load_failure` | [!DNL Data Ingestion] | 실패 | 일괄 처리를 데이터 세트에 인제스트하지 못했습니다 [!DNL Data Lake]. |
| `ps_load_success` | [!DNL Real-time Customer Profile] | 성공 | 일괄 처리를 데이터 [!DNL Profile] 저장소에 수집했습니다. |
| `ps_load_failure` | [!DNL Real-time Customer Profile] | 실패 | 일괄 처리를 데이터 [!DNL Profile] 저장소에서 인제스트하지 못했습니다. |
| `ig_load_success` | [!DNL Identity Service] | 성공 | 데이터가 ID 그래프로 로드되었습니다. |
| `ig_load_failure` | [!DNL Identity Service] | 실패 | 데이터를 ID 그래프로 로드하지 못했습니다. |

>[!NOTE]
>
>모든 데이터 수집 알림에 대해 제공된 이벤트 주제는 하나만 있습니다. 다른 상태를 구분하기 위해 이벤트 코드를 사용할 수 있습니다.