---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 개인 정보 보호 이벤트 구독
topic: privacy events
translation-type: tm+mt
source-git-commit: ab29c7771122267634dea24582b07f605abd7ed8
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 1%

---


# 개인 정보 보호 이벤트 구독

개인정보 보호 이벤트는 Adobe Experience Platform Privacy Service에서 제공하는 메시지입니다. Adobe I/O Events가 구성된 웹 후크에 저장되어 효율적인 작업 요청 자동화를 촉진합니다. 작업이 완료되었는지 또는 워크플로우 내의 특정 이정표에 도달했는지 확인하기 위해 개인 정보 서비스 API를 폴링할 필요가 없어집니다.

개인 정보 작업 요청 라이프사이클과 관련된 4가지 유형의 알림이 현재 있습니다.

| 유형 | 설명 |
--- | ---
| 작업 완료 | 모든 Experience Cloud 솔루션이 다시 보고되었으며 작업의 전체 또는 글로벌 상태가 완료로 표시되었습니다. |
| 작업 오류 | 요청을 처리하는 동안 하나 이상의 솔루션에 오류가 보고되었습니다. |
| 제품 완료 | 이 작업과 관련된 솔루션 중 하나가 작업을 완료했습니다. |
| 제품 오류 | 요청을 처리하는 동안 솔루션 중 하나가 오류를 보고했습니다. |

이 문서에서는 Adobe I/O 내 개인정보 보호 서비스 알림에 대한 통합을 설정하는 절차를 제공합니다. 개인정보 보호 서비스 및 해당 기능에 대한 자세한 개요는 [개인정보 보호 서비스 개요를 참조하십시오](home.md).

## 시작하기

이 자습서에서는 보안 터널 **을**&#x200B;통해 로컬 서버를 일반 인터넷에 노출하는 소프트웨어 제품인 ngrok를 사용합니다. 따라하고 로컬 컴퓨터에 웹후크를 [만들려면 이 자습서를 시작하기](https://ngrok.com/download) 전에 그룹을 설치하십시오. 또한 이 안내서에서는 간단한 [Node.js 서버가 포함된 GIT 리포지토리를 다운로드해야](https://nodejs.org/) 합니다.

## 로컬 서버 만들기

Node.js 서버는 요청에 의해 전송된 `challenge` 매개 변수를 루트(`/`) 끝점으로 반환해야 합니다. 이를 위해 다음 JavaScript로 `index.js` 파일을 설정합니다.

```js
var express = require('express')
var app = express()

app.set('port', (process.env.PORT || 3000))
app.use(express.static(__dirname + '/public'))

app.get('/', function(request, response) {
  response.send(request.originalUrl.split('?challenge=')[1]);
})

app.listen(app.get('port'), function() {
  console.log("Node app is running at localhost:" + app.get('port'))
})
```

명령줄을 사용하여 Node.js 서버의 루트 디렉토리로 이동합니다. 그런 다음 다음 다음 명령을 입력합니다.

1. `npm install`
1. `npm start`

이러한 명령은 모든 종속성을 설치하고 서버를 초기화합니다. 성공하면 http://localhost:3000/에서 실행되는 서버를 찾을 수 있습니다.

## ngrok를 사용하여 웹 후크 만들기

새 명령줄 창을 열고 이전에 ngroup을 설치한 디렉토리로 이동합니다. 여기서 다음 명령을 입력합니다.

```shell
./ngrok http -bind-tls=true 3000
```

성공적인 출력은 다음과 비슷합니다.

![출력](images/privacy-events/ngrok-output.png)

다음 단계에서 웹 후크를 식별하는 데 사용되므로 `Forwarding` URL(`https://212d6cd2.ngrok.io`)을 참고하십시오.

## Adobe 개발자 콘솔에서 새 프로젝트 만들기

Adobe [Developer Console에서](https://www.adobe.com/go/devs_console_ui) Adobe ID로 로그인합니다. 그런 다음 Adobe 개발자 콘솔 문서에서 빈 프로젝트 [를 만드는 방법에 대한 자습서에 나와](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) 있는 단계를 따릅니다.

## 프로젝트에 개인 정보 이벤트 추가

콘솔에서 새 프로젝트 만들기를 완료하면 [프로젝트 개요] **[!UICONTROL 화면에서 [이벤트]** 추가]를 _클릭합니다_ .

![](./images/privacy-events/add-event-button.png)

이벤트 _추가_ 대화 상자가 나타납니다. 사용 가능한 이벤트 유형 목록을 **[!UICONTROL 필터링하려면 Experience Cloud]** 를 선택한 다음 **[!UICONTROL 다음]** 을 클릭하기 전에 **[!UICONTROL 개인 정보 서비스 이벤트]**&#x200B;를선택합니다.

![](./images/privacy-events/add-privacy-events.png)

[ _이벤트 등록_ 구성] 대화 상자가 나타납니다. 해당 확인란을 선택하여 받을 이벤트를 선택합니다. 선택한 이벤트는 왼쪽 열의 _[!UICONTROL 구독된 이벤트]_아래에 나타납니다. 완료되면 [다음]을**[!UICONTROL &#x200B;클릭합니다&#x200B;]**.

![](./images/privacy-events/choose-subscriptions.png)

다음 화면은 이벤트 등록에 대한 공개 키를 제공하라는 메시지를 표시합니다. 키 쌍을 자동으로 생성하거나 터미널에서 생성된 자신의 공개 키를 업로드할 수 있는 옵션이 제공됩니다.

이 튜토리얼의 목적을 위해 첫 번째 옵션이 따릅니다. 키 쌍 **[!UICONTROL 생성 옵션 상자]**&#x200B;를 클릭한 다음 오른쪽 아래에 있는 키 쌍 **[!UICONTROL 생성]** 단추를 클릭합니다.

![](./images/privacy-events/generate-key-value.png)

키 쌍이 생성되면 브라우저에 의해 자동으로 다운로드됩니다. 이 파일은 개발자 콘솔에서 지속되지 않으므로 직접 저장해야 합니다.

다음 화면에서는 새로 생성된 키 쌍의 세부 사항을 검토할 수 있습니다. 계속하려면 **[!UICONTROL 다음]**&#x200B;을 클릭하십시오.

![](./images/privacy-events/keypair-generated.png)

다음 화면에서 이벤트 등록에 대한 이름과 설명을 입력합니다. 가장 좋은 방법은 이 이벤트 등록을 동일한 프로젝트의 다른 사용자와 구별할 수 있는 고유한 이름을 만드는 것입니다.

![](./images/privacy-events/event-details.png)

동일한 화면에서 추가로, 이벤트를 수신하는 방법을 구성하는 두 가지 옵션이 제공됩니다. 웹 후크 **[!UICONTROL 를]** 선택하고 Webhook URL에서 이전에 만든 웹 후크의 `Forwarding` URL을 _[!UICONTROL 제공합니다]_. 다음으로, [구성된 이벤트**[!UICONTROL &#x200B;저장]을 클릭하여 이벤트 등록을 완료하기 전에 원하는 배달 스타일(단일 또는 배치)을&#x200B;]**선택합니다.

![](./images/privacy-events/webhook-details.png)

왼쪽 탐색 창의 _[!UICONTROL 이벤트]_아래에 개인정보 보호 이벤트가 나타나면서 프로젝트의 세부 사항 페이지가 다시 나타납니다.

## 이벤트 데이터 보기

프로젝트에 개인정보 보호 이벤트를 등록했고 개인 정보 작업이 처리되면 해당 등록에 대해 수신된 알림을 볼 수 있습니다. 개발자 콘솔의 **[!UICONTROL 프로젝트]** 탭에서 목록에서 프로젝트를 선택하여 _제품 개요_ 페이지를 엽니다. 여기서 왼쪽 탐색 **[!UICONTROL 에서 [개인 정보]** 이벤트]를 선택합니다.

![](./images/privacy-events/events-left-nav.png)

[ _등록 세부 정보_ ] 탭이 표시되므로 등록에 대한 자세한 정보를 보거나, 구성을 편집하거나, 웹후크를 활성화한 후 받은 실제 이벤트를 볼 수 있습니다.

![](./images/privacy-events/registration-details.png)

받은 이벤트 목록을 **[!UICONTROL 보려면 디버그 추적]** 탭을 클릭합니다. 나열된 이벤트를 클릭하여 해당 세부 사항을 봅니다.

![](images/privacy-events/debug-tracing.png)

페이로드 _[!UICONTROL 섹션]_은 위의 예에서 강조표시된 대로 선택한 이벤트에 대한 세부 사항(이벤트 유형`com.adobe.platform.gdpr.productcomplete`)을 제공합니다.

## 다음 단계

필요에 따라 다른 웹 후크 주소에 대한 새 통합을 추가하려면 위 단계를 반복할 수 있습니다.