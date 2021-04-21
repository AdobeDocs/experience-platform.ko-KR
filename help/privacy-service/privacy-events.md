---
keywords: Experience Platform;홈;인기 항목
solution: Experience Platform
title: Privacy Service 이벤트 구독
topic-legacy: privacy events
description: 미리 구성된 웹 후크를 사용하여 Privacy Service 이벤트에 구독하는 방법을 알아봅니다.
exl-id: 9bd34313-3042-46e7-b670-7a330654b178
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 1%

---

# [!DNL Privacy Service Events] 구독

[!DNL Privacy Service Events] 은 효율적인 작업 요청 자동화를 용이하게 하기 위해 구성된 웹 후크에 전송되는 Adobe I/O 이벤트를 이용하는 Adobe Experience Platform [!DNL Privacy Service]가 제공하는 메시지입니다. 작업이 완료되었는지 또는 워크플로우 내의 특정 이정표에 도달했는지 확인하기 위해 [!DNL Privacy Service] API를 폴링할 필요가 줄어들었습니다.

개인 정보 작업 요청 라이프사이클과 관련된 4가지 유형의 알림이 현재 있습니다.

| 유형 | 설명 |
| --- | --- |
| 작업 완료 | 모든 [!DNL Experience Cloud] 응용 프로그램이 다시 보고되었으며 작업의 전체 또는 전체 상태가 완료로 표시되었습니다. |
| 작업 오류 | 요청을 처리하는 동안 하나 이상의 응용 프로그램에서 오류를 보고했습니다. |
| 제품 완료 | 이 작업과 관련된 응용 프로그램 중 하나가 작업을 완료했습니다. |
| 제품 오류 | 응용 프로그램 중 하나가 요청을 처리하는 동안 오류를 보고했습니다. |

이 문서에서는 [!DNL Privacy Service] 알림에 대한 이벤트 등록을 설정하는 단계와 알림 페이로드를 해석하는 방법을 제공합니다.

## 시작하기

이 자습서를 시작하기 전에 다음 Privacy Service 설명서를 검토하십시오.

* [Privacy Service 개요](./home.md)
* [Privacy Service API 개발자 가이드](./api/getting-started.md)

## [!DNL Privacy Service Events]에 웹 후크를 등록합니다.

[!DNL Privacy Service Events]을(를) 받으려면 Adobe 개발자 콘솔을 사용하여 [!DNL Privacy Service] 통합에 웹 후크를 등록해야 합니다.

이를 수행하는 방법에 대한 자세한 단계는 [가입 [!DNL I/O Event] notifications](../observability/notifications/subscribe.md)의 자습서를 따르십시오. 위에 나열된 이벤트에 액세스하려면 이벤트 공급자로 **[!UICONTROL Privacy Service Events]**&#x200B;을 선택해야 합니다.

## [!DNL Privacy Service Event] 알림 받기

웹 후크 및 개인 정보 작업이 성공적으로 실행되면 이벤트 알림 수신을 시작할 수 있습니다. 이러한 이벤트는 웹 후크 자체를 사용하거나 Adobe 개발자 콘솔에서 프로젝트의 이벤트 등록 개요에서 **[!UICONTROL Debug Tracing]** 탭을 선택하여 볼 수 있습니다.

![](images/privacy-events/debug-tracing.png)

다음 JSON은 개인 정보 작업과 관련된 응용 프로그램 중 하나가 작업을 완료하면 웹후크로 전송될 [!DNL Privacy Service Event] 알림 페이로드의 예입니다.

```json
{
  "id":"b472e249-368b-4706-90f3-1d774713f827",
  "event_id":"b116f797-e50b-432e-9c65-189106a34820",
  "specversion":"0.2",
  "type":"com.adobe.platform.gdpr.productcomplete",
  "source":"https://ns.adobe.com/platform/gdpr",
  "time":"Wed Oct 23 18:52:32 GMT 2019",
  "data":{
    "imsOrg":"{IMS_ORG}",
    "value":{
      "jobId":"6f0f2b62-88a7-4515-ba05-432d9a7021c5",
      "message":"analytics.access.complete"
    }
  }
}
```

| 속성 | 설명 |
| --- | --- |
| `id` | 알림에 대한 고유한 시스템 생성 ID. |
| `type` | 전송 중인 알림 유형으로, `data`에 제공된 정보에 컨텍스트를 제공합니다. 잠재적 값은 다음과 같습니다. <ul><li>`com.adobe.platform.gdpr.jobcomplete`</li><li>`com.adobe.platform.gdpr.joberror`</li><li>`com.adobe.platform.gdpr.productcomplete`</li><li>`com.adobe.platform.gdpr.producterror`</li></ul> |
| `time` | 이벤트가 발생한 타임스탬프. |
| `data.value` | 알림을 트리거한 항목에 대한 추가 정보가 포함되어 있습니다. <ul><li>`jobId`:알림을 트리거한 개인 정보 작업의 ID입니다.</li><li>`message`:작업의 특정 상태에 대한 메시지입니다. `productcomplete` 또는 `producterror` 알림의 경우 이 필드는 문제의 Experience Cloud 응용 프로그램을 나타냅니다.</li></ul> |

## 다음 단계

이 문서에서는 Privacy Service 이벤트를 구성된 웹 후크에 등록하는 방법과 알림 페이로드를 해석하는 방법에 대해 다룹니다. 사용자 인터페이스를 사용하여 개인 정보 작업을 추적하는 방법을 알아보려면 [Privacy Service 사용자 안내서](./ui/user-guide.md)를 참조하십시오.
