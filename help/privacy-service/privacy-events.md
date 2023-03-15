---
keywords: Experience Platform;홈;인기 있는 주제
solution: Experience Platform
title: Privacy Service 이벤트 구독
description: 사전 구성된 Webhook을 사용하여 Privacy Service 이벤트에 가입하는 방법을 알아봅니다.
exl-id: 9bd34313-3042-46e7-b670-7a330654b178
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 2%

---

# 구독 대상 [!DNL Privacy Service Events]

[!DNL Privacy Service Events] Adobe Experience Platform에서 제공한 메시지 [!DNL Privacy Service]- 구성된 웹후크로 전송된 Adobe I/O 이벤트를 활용하여 효율적인 작업 요청 자동화를 가능하게 합니다. 또한 폴링을 수행할 필요가 줄어들거나 없어집니다. [!DNL Privacy Service] 작업이 완료되었는지 또는 워크플로우 내의 특정 이정표에 도달했는지 확인하기 위한 API입니다.

현재 개인 정보 작업 요청 수명 주기와 관련된 네 가지 유형의 알림이 있습니다.

| 유형 | 설명 |
| --- | --- |
| 작업 완료 | 모두 [!DNL Experience Cloud] 애플리케이션이 다시 보고되었으며 작업의 전체 또는 전역 상태가 완료로 표시되었습니다. |
| 작업 오류 | 하나 이상의 애플리케이션에서 요청을 처리하는 동안 오류가 보고되었습니다. |
| 제품 완료 | 이 작업과 연결된 응용 프로그램 중 하나가 작업을 완료했습니다. |
| 제품 오류 | 요청을 처리하는 동안 애플리케이션 중 하나에서 오류를 보고했습니다. |

이 문서에서는에 대한 이벤트 등록을 설정하는 단계를 제공합니다. [!DNL Privacy Service] 알림 및 알림 페이로드를 해석하는 방법.

## 시작하기

이 자습서를 시작하기 전에 다음 Privacy Service 설명서를 검토하십시오.

* [Privacy Service 개요](./home.md)
* [Privacy Service API 안내서](./api/overview.md)

## 에 웹후크 등록 [!DNL Privacy Service Events]

받으려면 [!DNL Privacy Service Events], Adobe Developer 콘솔을 사용하여에 웹후크를 등록해야 합니다 [!DNL Privacy Service] 통합.

다음에 대한 자습서를 따르십시오 [[!DNL I/O Event] 알림 구독](../observability/alerts/subscribe.md) 을 수행하는 방법에 대한 자세한 단계입니다. 다음을 선택해야 합니다. **[!UICONTROL Privacy Service 이벤트]** 위에 나열된 이벤트에 액세스하기 위해 이벤트 공급자로 사용됩니다.

## 수신 [!DNL Privacy Service Event] 알림

웹후크 및 개인 정보 보호 작업이 정상적으로 등록되면 이벤트 알림을 받을 수 있습니다. 이러한 이벤트는 Webhook 자체를 사용하거나 **[!UICONTROL 추적 디버그]** Adobe Developer Console에서 프로젝트의 이벤트 등록 개요 탭

![](images/privacy-events/debug-tracing.png)

다음 JSON은 [!DNL Privacy Service Event] 개인 정보 보호 작업과 연관된 애플리케이션 중 하나가 작업을 완료했을 때 웹후크로 전송되는 알림 페이로드:

```json
{
  "id":"b472e249-368b-4706-90f3-1d774713f827",
  "event_id":"b116f797-e50b-432e-9c65-189106a34820",
  "specversion":"0.2",
  "type":"com.adobe.platform.gdpr.productcomplete",
  "source":"https://ns.adobe.com/platform/gdpr",
  "time":"Wed Oct 23 18:52:32 GMT 2019",
  "data":{
    "imsOrg":"{ORG_ID}",
    "value":{
      "jobId":"6f0f2b62-88a7-4515-ba05-432d9a7021c5",
      "message":"analytics.access.complete"
    }
  }
}
```

| 속성 | 설명 |
| --- | --- |
| `id` | 알림에 대한 시스템 생성 고유 ID. |
| `type` | 아래에 제공된 정보에 컨텍스트를 제공하는 전송 중인 알림 유형 `data`. 잠재적 값은 다음과 같습니다. <ul><li>`com.adobe.platform.gdpr.jobcomplete`</li><li>`com.adobe.platform.gdpr.joberror`</li><li>`com.adobe.platform.gdpr.productcomplete`</li><li>`com.adobe.platform.gdpr.producterror`</li></ul> |
| `time` | 이벤트가 발생한 시간의 타임스탬프입니다. |
| `data.value` | 알림을 트리거한 것에 대한 추가 정보를 포함합니다. <ul><li>`jobId`: 알림을 트리거한 개인 정보 보호 작업의 ID입니다.</li><li>`message`: 작업의 특정 상태에 대한 메시지입니다. 대상 `productcomplete` 또는 `producterror` 통지, 이 필드는 해당 Experience Cloud 애플리케이션을 나타냅니다.</li></ul> |

## 다음 단계

이 문서에서는 구성된 웹후크에 Privacy Service 이벤트를 등록하는 방법과 알림 페이로드를 해석하는 방법에 대해 설명합니다. 사용자 인터페이스를 사용하여 개인 정보 작업을 추적하는 방법에 대해 알아보려면 다음을 참조하십시오. [Privacy Service 사용 안내서](./ui/user-guide.md).
