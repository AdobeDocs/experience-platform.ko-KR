---
keywords: Experience Platform;홈;인기 항목;날짜 범위
title: Adobe I/O 이벤트 알림 구독
description: 이 문서에서는 Adobe Experience Platform 서비스를 위한 Adobe I/O 이벤트 알림을 구독하는 방법에 대한 단계를 제공합니다. 사용 가능한 이벤트 유형에 대한 참조 정보가 제공되며 적용 가능한 각  [!DNL Experience Platform] 서비스에 대해 반환된 이벤트 데이터를 해석하는 방법에 대한 추가 설명서 링크도 함께 제공됩니다.
feature: Alerts
exl-id: c0ad7217-ce84-47b0-abf6-76bcf280f026
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 1%

---

# Adobe I/O 이벤트 알림 구독

[!DNL Observability Insights]을(를) 통해 Adobe Experience Platform 활동에 대한 Adobe I/O 이벤트 알림을 구독할 수 있습니다. 이러한 이벤트는 활동 모니터링의 효율적인 자동화를 용이하게 하기 위해 구성된 웹후크로 전송됩니다.

이 문서에서는 Adobe Experience Platform 서비스에 대한 Adobe I/O 이벤트 알림을 구독하는 방법에 대한 단계를 제공합니다. 사용 가능한 이벤트 유형에 대한 참조 정보가 제공되며 각 적용 가능한 [!DNL Experience Platform] 서비스에 대해 반환된 이벤트 데이터를 해석하는 방법에 대한 추가 설명서에 대한 링크도 제공됩니다.

## 시작하기

이 문서에서는 웹후크 및 하나의 애플리케이션에서 다른 애플리케이션에 웹후크를 연결하는 방법에 대해 작업해야 합니다. Webhooks에 대한 소개는 [[!DNL I/O Events] 설명서](https://www.adobe.io/apis/experienceplatform/events/docs.html#!adobedocs/adobeio-events/master/intro/webhook_docs_intro.md)를 참조하세요.

## 웹후크 만들기

[!DNL I/O Event] 알림을 받으려면 고유한 웹후크 URL을 이벤트 등록 세부 정보의 일부로 지정하여 웹후크를 등록해야 합니다.

원하는 클라이언트를 사용하여 Webhook을 구성할 수 있습니다. 이 자습서의 일부로 사용할 임시 웹후크 주소를 보려면 [Webhook.site](https://webhook.site/)를 방문하여 제공된 고유 URL을 복사하십시오.

![](../images/notifications/webhook-url.png)

초기 유효성 검사 프로세스 중에 [!DNL I/O Events]이(가) GET 요청의 `challenge` 쿼리 매개 변수를 웹후크로 보냅니다. 응답 페이로드에서 이 매개 변수의 값을 반환하도록 웹후크를 구성해야 합니다. Webhook.site를 사용하는 경우 오른쪽 상단에서 **[!DNL Edit]**&#x200B;을(를) 선택한 다음 **[!DNL Save]**&#x200B;을(를) 선택하기 전에 **[!DNL Response body]** 아래에 `$request.query.challenge$`을(를) 입력하십시오.

![](../images/notifications/response-challenge.png)

## Adobe Developer Console에서 새 프로젝트 만들기

[Adobe Developer Console](https://www.adobe.com/go/devs_console_ui)&#x200B;(으)로 이동하여 Adobe ID으로 로그인합니다. 그런 다음 Adobe Developer Console 설명서에서 [빈 프로젝트 만들기](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/)에 대한 자습서에 설명된 단계를 수행합니다.

## 이벤트 구독

>[!NOTE]
>
>데이터 수집 알림 이벤트는 Adobe I/O에서 더 이상 사용되지 않습니다. 대신 **소스 흐름 실행 정보** I/O 이벤트를 사용해야 합니다.

새 프로젝트를 만든 후 해당 프로젝트의 개요 화면으로 이동합니다. 여기에서 **[!UICONTROL 이벤트 추가]**&#x200B;를 선택하십시오.

![](../images/notifications/add-event-button.png)

프로젝트에 이벤트 공급자를 추가할 수 있는 대화 상자가 나타납니다.

* Experience Platform 알림을 구독하는 경우 **[!UICONTROL 플랫폼 알림]**&#x200B;을 선택하세요.
* Adobe Experience Platform [!DNL Privacy Service] 알림을 구독하는 경우 **[!UICONTROL Privacy Service 이벤트]**&#x200B;를 선택하세요.

이벤트 공급자를 선택한 후 **[!UICONTROL 다음]**&#x200B;을(를) 선택하십시오.

![](../images/notifications/event-provider.png)

다음 화면에는 가입할 이벤트 유형 목록이 표시됩니다. 구독할 이벤트를 선택한 후 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

>[!NOTE]
>
>작업 중인 서비스에 대해 구독할 이벤트를 잘 모르는 경우 다음 설명서를 참조하십시오.
>
>* [플랫폼 알림](./rules.md)
>* [Privacy Service 알림](../../privacy-service/privacy-events.md)

>[!IMPORTANT]
>
>Edge 관련 경고는 현재 beta 버전이며 일부 베타 고객만 사용할 수 있습니다.

![](../images/notifications/choose-event-subscriptions.png)

다음 화면에서는 JSON 웹 토큰(JWT)을 만들라는 메시지를 표시합니다. 키 쌍을 자동으로 생성하거나 터미널에서 생성한 자신의 공개 키를 업로드할 수 있는 옵션이 제공됩니다.

이 자습서에서는 첫 번째 옵션을 따릅니다. **[!UICONTROL 키 쌍 생성]**&#x200B;에 대한 옵션 상자를 선택한 다음 오른쪽 하단에 있는 **[!UICONTROL 키 쌍 생성]** 단추를 선택합니다.

![](../images/notifications/generate-keypair.png)

키 쌍이 생성되면 브라우저가 자동으로 다운로드합니다. 이 파일은 Developer Console에서 유지되지 않으므로 직접 저장해야 합니다.

다음 화면에서는 새로 생성된 키 쌍의 세부 사항을 검토할 수 있습니다. 계속하려면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

![](../images/notifications/keypair-generated.png)

다음 화면에서는 [!UICONTROL 이벤트 등록 세부 정보] 섹션에서 이벤트 등록에 대한 이름과 설명을 입력합니다. 가장 좋은 방법은 이 이벤트 등록을 동일한 프로젝트의 다른 등록과 구분할 수 있도록 고유하고 쉽게 식별할 수 있는 이름을 만드는 것입니다.

![](../images/notifications/registration-details.png)

[!UICONTROL 이벤트를 받는 방법] 섹션 아래의 같은 화면에서 아래쪽으로 내려가면 이벤트를 받는 방법을 선택적으로 구성할 수 있습니다. **[!UICONTROL Webhook]**&#x200B;을(를) 사용하면 이벤트를 수신할 사용자 지정 Webhook 주소를 제공할 수 있지만 **[!UICONTROL 런타임 작업]**&#x200B;을(를) 사용하면 [Adobe I/O Runtime](https://www.adobe.io/apis/experienceplatform/runtime/docs.html)을(를) 사용하여 동일한 작업을 수행할 수 있습니다.

이 자습서에서는 **[!UICONTROL Webhook]**&#x200B;을(를) 선택하고 이전에 만든 Webhook의 URL을 제공합니다. 완료되면 **[!UICONTROL 구성된 이벤트 저장]**&#x200B;을 선택하여 이벤트 등록을 완료합니다.

![](../images/notifications/receive-events.png)

새로 만든 이벤트 등록에 대한 세부 정보 페이지가 표시되어 구성을 편집하고, 받은 이벤트를 검토하고, 디버그 추적을 수행하고, 새 이벤트 공급자를 추가할 수 있습니다.

![](../images/notifications/registration-complete.png)

## 다음 단계

이 자습서에 따라 [!DNL Experience Platform] 및/또는 [!DNL Privacy Service]에 대한 [!DNL I/O Event] 알림을 받을 웹후크를 등록했습니다. 사용 가능한 이벤트 및 각 서비스에 대한 알림 페이로드를 해석하는 방법에 대한 자세한 내용은 다음 설명서를 참조하십시오.

* [[!DNL Privacy Service] 알림](../../privacy-service/privacy-events.md)
* [[!DNL Flow Service]개(원본) 알림](../../sources/notifications.md)

[!DNL Experience Platform] 및 [!DNL Privacy Service]에서 활동을 모니터링하는 방법에 대한 자세한 내용은 [[!DNL Observability Insights] 개요](../home.md)를 참조하십시오.
