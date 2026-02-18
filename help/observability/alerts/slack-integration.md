---
title: 고객 응대 경고를 위한 Slack 통합
description: Adobe App Builder을 사용하여 Adobe I/O Events을 Slack에 연결하는 방법을 알아봅니다.
source-git-commit: c0fa0320b32e1bfe286d47a2e1af5ea1dcf74cb9
workflow-type: tm+mt
source-wordcount: '946'
ht-degree: 0%

---

# 고객 응대 경고를 위한 Slack 통합

Adobe Experience Platform을 사용하면 [Adobe App Builder](https://developer.adobe.com/app-builder/docs/get_started/app_builder_get_started/first-app)에서 웹후크 프록시를 사용하여 [에서 ](https://developer.adobe.com/events/docs/guides/)Adobe I/O Events[!DNL Slack]을(를) 받을 수 있습니다. 프록시는 Adobe의 확인 핸드셰이크를 처리하고 이벤트 페이로드를 [!DNL Slack] 메시지로 전환하므로 고객이 응대하는 알림을 작업 영역에 전달할 수 있습니다.

## 전제 조건 {#prerequisites}

시작하기 전에 다음을 확인하십시오.

* **Adobe Developer Console 액세스**: App Builder이 활성화된 조직의 시스템 관리자 또는 개발자 역할입니다.
* **Node.js 및 npm**: Adobe CLI 및 프로젝트 종속성을 설치하기 위한 npm이 포함된 Node.js(LTS 권장). 자세한 내용은 [Node.js 다운로드](https://nodejs.org/) 및 [npm 시작 안내서](https://docs.npmjs.com/getting-started)를 참조하십시오.
* **Adobe I/O CLI**: 터미널에서 Adobe I/O CLI를 설치합니다. `npm install -g @adobe/aio-cli`.
* **들어오는 Webhook가 있는 Slack 앱**: **들어오는 Webhook**&#x200B;이(가) 활성화된 작업 공간의 Slack 앱입니다. 앱을 만들고 웹후크 URL(형식: [)을 가져오려면 ](https://api.slack.com/apps)Slack 앱 만들기[ 및 ](https://api.slack.com/messaging/webhooks)Slack 수신 웹후크 안내서`https://hooks.slack.com/...`를 참조하십시오.

## 템플릿 프로젝트 설정 {#templated-project}

템플릿 프로젝트를 설정하려면 Adobe Developer Console에 로그인한 다음 **[!UICONTROL Create project from template]** 탭에서 **[!UICONTROL Home]**&#x200B;을(를) 선택합니다.

![홈 탭을 강조 표시하는 Developer Console 및 템플릿에서 프로젝트 만들기](../images/alerts/slack-integration/developer-console-home.png)

**[!UICONTROL App Builder]** 템플릿을 선택한 다음 **[!UICONTROL Project Title]**&#x200B;을(를) 입력하고 **[!UICONTROL Add workspace]**&#x200B;을(를) 선택합니다. 마지막으로 **[!UICONTROL Save]**&#x200B;을(를) 선택합니다.

![Developer Console 강조 표시 프로젝트 제목, Workspace 추가 및 저장](../images/alerts/slack-integration/developer-console-save.png)

프로젝트가 만들어졌고 **[!UICONTROL Project overview]** 탭으로 이동되었다는 확인 메시지가 표시됩니다. 여기에서 **[!UICONTROL Project description]**&#x200B;을(를) 추가할 수 있습니다.

![프로젝트 세부 정보를 표시하는 프로젝트 개요 탭입니다.](../images/alerts/slack-integration/developer-console-project.png)

## 프로젝트 초기화 {#initialize-project}

템플릿화된 프로젝트를 설정하고 나면 프로젝트를 초기화합니다.

1. 터미널을 열고 다음 명령을 입력하여 Adobe I/O에 로그인합니다.

   ```bash
   aio login
   ```

1. 응용 프로그램을 초기화하고 이름을 입력하십시오.

   ```bash
   aio app init slack-webhook-proxy
   ```

1. 화살표 키를 사용하여 `Organization`을(를) 선택한 다음 Developer Console에서 이전에 만든 `Project`을(를) 선택합니다. 검색할 템플릿에 대해 `Only Templates Supported By My Org`을(를) 선택하십시오.

   ![터미널에서 조직 및 프로젝트 선택을 표시하고 내 조직에서 지원하는 템플릿만 표시합니다.](../images/alerts/slack-integration/terminal-organization-project.png)

1. 서식 파일을 건너뛰고 독립 실행형 응용 프로그램을 설치하려면 **Enter**&#x200B;를 누르십시오.

   ![터미널에서 조직 및 프로젝트 선택을 표시하고 내 조직에서 지원하는 템플릿만 표시합니다.](../images/alerts/slack-integration/terminal-skip-templates.png)

1. 이 프로젝트에 사용할 Adobe I/O 앱 기능을 지정합니다. 화살표 키를 사용하여 스크롤하고 `Actions: Deploy Runtime actions`을(를) 선택합니다.

   ![앱 기능을 표시하는 터미널(작업: 런타임 작업 배포)을 선택했습니다.](../images/alerts/slack-integration/terminal-app-features.png)

1. 화살표 키를 사용하여 스크롤하고 만들려는 샘플 작업 유형에 대해 `Adobe Experience Platform: Realtime Customer Profile`을(를) 선택합니다.

   ![Adobe Experience Platform에서 샘플 작업 유형을 표시하는 터미널: 실시간 고객 프로필이 선택되었습니다.](../images/alerts/slack-integration/terminal-sample-actions.png)

1. 스크롤하여 템플릿에 추가할 UI에 대해 `Pure HTML/JS`을(를) 선택합니다. 샘플 작업을 기본값으로 유지하려면 **Enter**&#x200B;를 누른 다음 이름을 기본값으로 유지하려면 **Enter**&#x200B;를 다시 누르십시오.

   ![순수 HTML/JS를 선택한 UI 선택을 표시하는 터미널입니다.](../images/alerts/slack-integration/terminal-ui-template.png)

   앱 초기화가 완료되었다는 확인 메시지가 표시됩니다.

1. 프로젝트 디렉토리로 이동합니다.

   ```bash
   cd slack-webhook-proxy
   ```

1. 웹 작업을 추가합니다.

   ```bash
   aio app add action
   ```

1. `Only Action Templates Supported By My Org`을(를) 선택합니다. 템플릿 목록이 나타납니다.

   ![터미널 목록에 작업 서식 파일이 표시됩니다.](../images/alerts/slack-integration/terminal-action-templates.png)

1. 스페이스바를 눌러 템플릿을 선택한 다음 `@adobe/generator-add-publish-events`위쪽&#x200B;**및**&#x200B;아래쪽&#x200B;**화살표를 사용하여**(으)로 이동합니다. 마지막으로 **스페이스바**&#x200B;를 눌러 템플릿을 선택하고 **Enter**&#x200B;를 누릅니다.

   ![템플릿을 표시하는 터미널입니다.](../images/alerts/slack-integration/terminal-action-select-template.png)

   `npm package @adobe/generator-add-publish-events`이(가) 설치되었음을 확인하는 메시지가 표시됩니다.

1. 작업 이름을 `webhook-proxy`(으)로 지정합니다.

   ![Webhook-proxy라는 작업을 표시하는 터미널입니다.](../images/alerts/slack-integration/terminal-add-action-name.png)

   템플릿이 설치되었음을 확인하는 메시지가 표시됩니다.

## 파일 작업 만들기 및 배포 {#create-file-actions}

프록시 코드를 추가하고 환경 변수를 설정한 다음 배포합니다. 그런 다음 Developer Console에서 등록을 위해 작업을 사용할 수 있습니다.

### 런타임 프록시 구현 {#runtime-proxy}

>[!NOTE]
>
>런타임 작업 등록을 사용할 때 서명 확인 및 과제 처리가 자동으로 수행됩니다.

프로젝트 폴더로 이동하여 `actions/webhook-proxy/index.js` 파일을 엽니다. 콘텐츠를 삭제하고 다음으로 대체합니다.

```
const fetch = require("node-fetch");
const { Core } = require("@adobe/aio-sdk");
 
/**
 * Adobe I/O Events to Slack Runtime Proxy
 *
 * Receives events from Adobe I/O Events and forwards them to Slack.
 * Signature verification and challenge handling are automatic when
 * using Runtime Action registration (non-web action).
 */
async function main(params) {
  const logger = Core.Logger("runtime-proxy", { level: params.LOG_LEVEL || "info" });
 
  try {
    logger.info(`Event received: ${JSON.stringify(params)}`);
 
    // Forward to Slack
    return forwardToSlack(params, params.SLACK_WEBHOOK_URL, logger);
 
  } catch (error) {
    logger.error(`Error: ${error.message}`);
    return { statusCode: 500, body: { error: "Internal server error" } };
  }
}
 
/**
 * Forwards the event payload to Slack
 */
async function forwardToSlack(payload, webhookUrl, logger) {
  if (!webhookUrl) {
    logger.error("SLACK_WEBHOOK_URL not configured");
    return { statusCode: 500, body: { error: "Server configuration error" } };
  }
 
  // Extract Adobe headers passed to runtime action
  const headers = {
    "x-adobe-event-code": payload["x-adobe-event-code"],
    "x-adobe-event-id": payload["x-adobe-event-id"],
    "x-adobe-provider": payload["x-adobe-provider"]
  };
 
  const slackMessage = buildSlackMessage(payload, headers);
 
  const response = await fetch(webhookUrl, {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(slackMessage)
  });
 
  if (!response.ok) {
    const errorText = await response.text();
    logger.error(`Slack API error: ${response.status} - ${errorText}`);
    return { statusCode: response.status, body: { error: errorText } };
  }
 
  logger.info("Event forwarded to Slack");
  return { statusCode: 200, body: { success: true } };
}
 
/**
 * Builds a Slack Block Kit message from the event payload
 */
function buildSlackMessage(payload, headers) {
  // Adobe passes event code as x-adobe-event-code header (available in params for runtime actions)
  const eventType = headers["x-adobe-event-code"] ||
                    payload["x-adobe-event-code"] ||
                    payload.event_code ||
                    payload.type ||
                    payload.event_type ||
                    "Adobe Event";
  const eventId = headers["x-adobe-event-id"] || payload["x-adobe-event-id"] || payload.event_id || payload.id || "N/A";
  const eventData = payload.data || payload.event || payload;
 
  return {
    blocks: [
      {
        type: "header",
        text: { type: "plain_text", text: `Event: ${eventType}`, emoji: true }
      },
      {
        type: "section",
        fields: formatDataFields(eventData)
      },
      { type: "divider" },
      {
        type: "context",
        elements: [{
          type: "mrkdwn",
          text: `*Event ID:* ${eventId}  |  *Time:* ${new Date().toISOString()}`
        }]
      }
    ]
  };
}
 
/**
 * Formats event data as Slack mrkdwn fields
 */
function formatDataFields(data, maxFields = 10) {
  if (typeof data !== "object" || data === null) {
    return [{ type: "mrkdwn", text: `*Payload:*\n${String(data)}` }];
  }
 
  const entries = Object.entries(data);
  if (entries.length === 0) {
    return [{ type: "mrkdwn", text: "_No data provided_" }];
  }
 
  return entries.slice(0, maxFields).map(([key, value]) => ({
    type: "mrkdwn",
    text: `*${key}:*\n${typeof value === "object" ? `\`\`\`${JSON.stringify(value)}\`\`\`` : value}`
  }));
}
 
exports.main = main;
```

### app.config.yaml에서 작업 구성 {#app-config}

>[!IMPORTANT]
>
>`app.config.yaml`의 작업 구성이 중요합니다. Developer Console에서 런타임 작업으로 등록할 수 있는 웹이 아닌 작업을 만들려면 `web: no`을(를) 사용해야 합니다.

프로젝트 폴더로 이동하여 `app.config.yaml`을(를) 엽니다. 내용을 다음과 같이 바꿉니다.

```
application:
  runtimeManifest:
    packages:
      slack-webhook-proxy:
        license: Apache-2.0
        actions:
          webhook-proxy:
            function: actions/webhook-proxy/index.js
            web: no
            runtime: nodejs:22
            inputs:
              LOG_LEVEL: info
              SLACK_WEBHOOK_URL: $SLACK_WEBHOOK_URL
            annotations:
              require-adobe-auth: false
              final: true
```

### 환경 변수 {#environment-variables}

>[!IMPORTANT]
>
>제대로 구성된 .env 파일 없이 응용 프로그램이 실행되지 않습니다.

자격 증명을 안전하게 관리하려면 환경 변수를 사용하십시오. 프로젝트의 루트에서 `.env` 파일을 수정하고 다음을 추가하십시오.

```
SLACK_WEBHOOK_URL=https://hooks.slack.com/services/YOUR/WEBHOOK/URL
```

### 작업 배포 {#deploy-action}

환경 변수가 설정되면 작업을 배포합니다. 터미널에서 이 명령을 실행할 때 프로젝트의 루트(`slack-webhook-proxy`)에 있는지 확인하십시오.

```bash
aio app deploy
```

배포가 성공했는지 확인하는 메시지가 표시됩니다.

>[!IMPORTANT]
>
>작업이 Adobe I/O Runtime에 배포됩니다. 이제 Developer Console에서 작업을 등록에 사용할 수 있습니다.

## Adobe I/O Events에 작업 등록 {#register-events}

작업이 배포되면 Adobe I/O Events 대상으로 등록합니다.

Developer Console에서 App Builder 프로젝트를 연 다음 **[!UICONTROL Workspace]**&#x200B;을(를) 선택합니다.

Workspace 개요 페이지에서 **[!UICONTROL Add service]** 및 **[!UICONTROL Event]**&#x200B;을(를) 선택합니다.

![서비스 및 이벤트 추가를 강조 표시하는 Workspace 개요 페이지](../images/alerts/slack-integration/workspace-service-event.png)

이벤트 추가 페이지에서 **[!UICONTROL Experience Platform]** 및 **[!UICONTROL Platform notifications]**&#x200B;을(를) 선택한 다음 **[!UICONTROL Next]**&#x200B;을(를) 선택합니다.

![선택한 Experience Platform 및 플랫폼 알림을 표시하는 이벤트 추가 페이지입니다.](../images/alerts/slack-integration/add-events.png)

알림을 받을 이벤트를 선택한 다음 **[!UICONTROL Next]**&#x200B;을(를) 선택합니다.

![구독할 이벤트 목록을 표시하는 이벤트 추가 페이지입니다.](../images/alerts/slack-integration/select-events.png)

서버 간 인증 자격 증명을 선택한 다음 **[!UICONTROL Next]**&#x200B;을(를) 선택합니다.

![서버 간 인증 자격 증명 선택을 표시하는 이벤트 추가 페이지입니다.](../images/alerts/slack-integration/add-events-credentials.png)

등록을 위해 **[!UICONTROL Event registration name]**&#x200B;을(를) 입력하고 **[!UICONTROL Event registration description]**&#x200B;을(를) 지운 다음 **[!UICONTROL Next]**&#x200B;을(를) 선택하십시오.

![이벤트 등록 이름 및 이벤트 등록 설명 필드를 표시하는 이벤트 추가 페이지입니다.](../images/alerts/slack-integration/add-events-registration.png)

**[!UICONTROL Runtime Action]**&#x200B;을(를) 게재 메서드로 선택하고 `slack-webhook-proxy/runtime-proxy` 작업을 만든 다음 **[!UICONTROL Save configured events]**&#x200B;을(를) 선택합니다.

![런타임 작업 전달 방법을 표시하는 이벤트 추가 페이지와 구성된 이벤트 저장](../images/alerts/slack-integration/add-events-runtime.png)

이제 웹후크 프록시가 구성되었습니다. Webhook 프록시 페이지로 돌아갑니다. 구성된 이벤트 옆에 있는 **[!UICONTROL Send sample event]** 아이콘을 선택하여 전체 흐름을 처음부터 끝까지 테스트할 수 있습니다.

![구성된 이벤트와 샘플 이벤트 보내기 아이콘을 표시하는 웹후크 프록시 페이지입니다.](../images/alerts/slack-integration/send-sample.png)
