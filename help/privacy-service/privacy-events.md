---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 개인 정보 보호 이벤트 구독
topic: privacy events
translation-type: tm+mt
source-git-commit: e4cd042722e13dafc32b059d75fca2dab828df60

---


# 개인 정보 보호 이벤트 구독

개인 정보 보호 이벤트는 Adobe Experience Platform 개인 정보 보호 서비스에서 제공하는 메시지입니다. Adobe I/O Events는 구성된 웹 후크로 전송되어 효율적인 작업 요청 자동화를 용이하게 합니다. 작업이 완료되었는지 또는 워크플로우 내의 특정 이정표에 도달했는지 확인하기 위해 개인 정보 서비스 API를 폴링할 필요가 없어집니다.

현재 개인 정보 작업 요청 라이프사이클과 관련된 네 가지 유형의 알림이 있습니다.

| 유형 | 설명 |
--- | ---
| 작업 완료 | 모든 Experience Cloud 솔루션이 다시 보고되었으며 작업의 전체 또는 글로벌 상태가 완료로 표시되었습니다. |
| 작업 오류 | 요청을 처리하는 동안 하나 이상의 솔루션이 오류를 보고했습니다. |
| 제품 완료 | 이 작업과 관련된 솔루션 중 하나가 작업을 완료했습니다. |
| 제품 오류 | 솔루션 중 하나가 요청을 처리하는 동안 오류를 보고했습니다. |

이 문서에서는 Adobe I/O 내 개인정보 보호 서비스 알림에 대한 통합을 설정하는 절차를 제공합니다.개인정보 보호 서비스 및 기능에 대한 자세한 개요는 개인정보 보호 서비스 [개요를](home.md)참조하십시오.

## 시작하기

이 자습서에서는 **보안**&#x200B;터널을 통해 로컬 서버를 일반 인터넷에 노출하는 소프트웨어 제품인 ngrok를 사용합니다. 따라하고 로컬 컴퓨터에 웹후크를 만들려면 이 자습서를 시작하기 전에 [ngroup](https://ngrok.com/download) 을 설치하십시오. 또한 이 안내서에서는 Node.js로 작성된 간단한 서버를 포함하는 GIT 리포지토리를 다운로드해야 [합니다](https://nodejs.org/).

## 로컬 서버 만들기

Node.js 서버는 요청에 의해 전송된 `challenge` 매개 변수를 루트(`/`) 끝점으로 반환해야 합니다. 이 작업을 수행하려면 다음 JavaScript를 사용하여 `index.js` 파일을 설정하십시오.

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

이러한 명령은 모든 종속성을 설치하고 서버를 초기화합니다. 성공하면 http://localhost:3000/에서 실행 중인 서버를 찾을 수 있습니다.

## ngrok를 사용하여 웹 후크 만들기

동일한 디렉토리 및 새 명령줄 창에서 다음 명령을 입력합니다.

```shell
ngrok http -bind-tls=true 3000
```

성공적인 출력은 다음과 비슷합니다.

![ngrok 출력](images/privacy-events/ngrok-output.png)

다음 단계에서 웹후크를 `Forwarding` 식별하는 데 사용될 URL(`https://e142b577.ngrok.io`)을 주목하십시오.

## Adobe I/O 콘솔을 사용하여 새로운 통합 만들기

Adobe I/ [O 콘솔에](https://console.adobe.io) 로그인하고 통합 **탭을** 클릭합니다. 통합 _창이_ 나타납니다. 여기에서 새 통합을 **클릭합니다**.

![Adobe I/O 콘솔에서 통합 보기](images/privacy-events/integrations.png)

새 *통합* 만들기 창이 나타납니다. 거의 **실시간 이벤트**&#x200B;수신을 선택한 다음 계속을 **클릭합니다**.

![새로운 통합 만들기](images/privacy-events/new-integration.png)

다음 화면에서는 구독, 권한 및 권한에 따라 조직에서 사용할 수 있는 다양한 이벤트, 제품 및 서비스와의 통합을 만들 수 있는 옵션을 제공합니다. 이 통합을 위해 개인 정보 서비스 **이벤트를**&#x200B;선택한 다음 계속을 **클릭합니다**.

![개인 정보 보호 이벤트 선택](images/privacy-events/privacy-events.png)

통합 *세부 사항* 양식이 나타나므로 통합에 대한 이름 및 설명과 공개 키 인증서를 제공해야 합니다.

![통합 세부 사항](images/privacy-events/integration-details.png)

공용 인증서가 없는 경우 다음 터미널 명령을 사용하여 인증서를 생성할 수 있습니다.

```shell
openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate_pub
```

인증서를 생성한 후 파일을 공개 키 인증서 **상자로 드래그하여 놓거나 파일 선택을** 클릭하여 **** 파일 디렉토리를 찾아 인증서를 직접 선택합니다.

인증서를 추가하면 [이벤트 *등록* ] 옵션이 나타납니다. [이벤트 **등록 추가]를 클릭합니다**.

![이벤트 등록 추가](images/privacy-events/add-event-registration.png)

대화 상자가 확장되어 추가 컨트롤이 표시됩니다. 여기에서 원하는 이벤트 유형을 선택하고 웹 후크를 등록할 수 있습니다. 이벤트 등록의 이름, 웹 후크 URL(웹 후크를 처음 `Forwarding` 만들 때 반환된 [주소](#create-a-webhook-using-ngrok)) 및 간단한 설명을 입력합니다. 마지막으로 가입하려는 이벤트 유형을 선택한 다음 저장을 **클릭합니다**.

![이벤트 등록 양식](images/privacy-events/event-registration-form.png)

이벤트 등록 양식이 완료되면 통합 **만들기를** 클릭하면 입출력 통합이 완료됩니다.

![통합 만들기](images/privacy-events/create-integration.png)

## 이벤트 데이터 보기

I/O 통합 및 개인 정보 작업이 처리되면 해당 통합에 대해 수신된 알림을 볼 수 있습니다. I/ **O 콘솔의** 통합 탭에서 통합으로 이동하고 보기를 **클릭합니다**.

![통합 보기](images/privacy-events/view-integration.png)

통합에 대한 세부 정보 페이지가 나타납니다. 통합을 **위한** 이벤트 등록을 보려면 [이벤트]를 클릭합니다. 개인 정보 이벤트 등록을 찾아 보기를 **클릭합니다**.

![이벤트 등록 보기](images/privacy-events/view-registration.png)

[ *이벤트 세부* 사항] 창이 표시되어 등록에 대한 자세한 정보를 보거나, 구성을 편집하거나, 웹후크를 활성화한 후 받은 실제 이벤트를 볼 수 있습니다. 이벤트 세부 사항을 볼 수 있을 뿐만 아니라 디버그 추적 **옵션으로 이동할 수** 있습니다.

![디버그 추적](images/privacy-events/debug-tracing.png)

페이로드 **섹션은** 위의 예에서 강조 표시된 대로 해당 이벤트 유형(`"com.adobe.platform.gdpr.productcomplete"`)을 비롯하여 선택한 이벤트에 대한 세부 정보를 제공합니다.

## 다음 단계

필요에 따라 다른 웹 후크 주소에 대한 통합을 새로 추가하려면 위의 단계를 반복할 수 있습니다.