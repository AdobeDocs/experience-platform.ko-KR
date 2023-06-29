---
title: Mailchimp 확장 개요
description: 이벤트 전달을 사용하여 Mailchimp 이메일을 트리거합니다.
type: Documentation
feature: Data Collection, Event Forwarding
level: Beginner
role: User, Developer, Admin
topic: Integrations
exl-id: a52870c4-10e6-45a0-a502-f48da3398f3f
source-git-commit: 12bd4c6c1993afc438b75a3e5163ebe2fe8a8dd0
workflow-type: tm+mt
source-wordcount: '1303'
ht-degree: 5%

---

# Mailchimp 이벤트 전달 확장 개요

>[!NOTE]
>  
>Adobe Experience Platform Launch은 Adobe Experience Platform의 데이터 수집 기술군으로 새롭게 브랜딩되었습니다. 그 결과로 제품 설명서 전반에서 몇 가지 용어 변경이 있었습니다. 용어 변경에 대한 통합 참고 자료는 다음 [문서](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html)를 참조하십시오.

Mailchimp [이벤트 전달](../../../ui/event-forwarding/overview.md) 확장은 Mailchimp 마케팅 캠페인, 여정 또는 트랜잭션에 대한 이메일을 트리거할 수 있는 이벤트를 Mailchimp Marketing API에 보냅니다.

이 문서에서는 이벤트 추가 작업을 사용하여 확장을 설정하고 규칙을 구성하는 방법에 대해 설명합니다.

## 사전 요구 사항

이 문서에서는 사용자가 확장에서 활용하는 관련 Mailchimp 제품을 잘 알고 있다고 가정합니다. 자세한 내용은 Mailchimp 도움말 설명서 를 참조하십시오. [캠페인](https://mailchimp.com/help/getting-started-with-campaigns/), [여정](https://mailchimp.com/help/about-customer-journeys/), 및 [트랜잭션](https://mailchimp.com/help/transactional/).

이 확장을 사용하려면 Mailchimp 계정이 필요합니다. 계정에 등록할 수 있습니다 [여기](https://login.mailchimp.com/signup/). Mailchimp 계정 대시보드에서 이 안내서에 사용할 다음 값을 메모하십시오.

- Mailchimp 도메인 접두사
- API 키
- 대상자 ID
- 기본 &quot;보낸 사람&quot; 이메일 주소

Mailchimp 계정 플랜에 따라 Mailchimp 고객 여정 도구에 대한 액세스가 제한될 수 있습니다.

>[!TIP]
>  
>트랜잭션 이메일 또는 고객 여정과 같은 Mailchimp 자동화를 사용하는 경우 단계 및 화면이 여기에 나열된 것과 약간 다를 수 있습니다. 그러나 위에서 설명한 대로 이 확장을 사용하려면 동일한 정보가 필요합니다. 다음을 참조하십시오. [Mailchimp 도움말 센터](https://mailchimp.com/help/) 특정 계정 및 플랜에 대한 이러한 각 값에 대한 세부 정보.

### 도메인 접두사

Mailchimp에 로그인하고 대시보드 보기에 랜딩한 후에는 브라우저의 주소 표시줄에 다음과 같은 URL이 표시됩니다 `https://us11.admin.mailchimp.com` 또는 `us11.admin.mailchimp.com`. 이 예에서 접두사 `us11` 는 자리 표시자일 뿐이며 값은 달라집니다. 이후 단계를 위해 접두사로 URL을 기록합니다.

### API 키

계정에 대한 API 키를 찾으려면 Mailchimp UI에서 프로필 아이콘을 선택한 다음 을 선택합니다. **프로필**. 다음과 같은 URL이 표시됩니다. `https://us11.admin.mailchimp.com/account/profile/` 하지만 **본인** 대신 접두사 `us11`.

선택 **기타**, 그런 다음 **API 키**:

![Extras 메뉴, API 키 링크](../../../images/extensions/server/mailchimp/menu-API-keys.png)

아래 **내 API 키**, 기존 키를 선택하거나 **키 만들기** 을 클릭하여 새 템플릿을 만듭니다. 이 확장에서 특별히 사용할 새 키를 만들 수 있습니다. API 키를 복사하고 이후 단계를 위해 저장합니다. 자세한 내용은 Mailchimp 설명서 를 참조하십시오 [api 키 생성](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key).

### 대상자 ID 및 보낸 사람 주소

선택 **대상자** 왼쪽 탐색에서 **대상 대시보드**. 그런 다음 이 확장에 사용할 대상을 선택합니다. 자세한 내용은 의 Mailchimp 문서를 참조하십시오. [대상자 만들기](https://mailchimp.com/help/create-audience/).

대상을 만들고 선택한 상태에서 **대상자 관리** 드롭다운 및 선택 **설정**. 이 화면에서는 대상에 대한 다양한 설정을 보여 줍니다.

설정 화면 하단에 다음이 표시됩니다 `Unique id for audience [audience name]` 위치 `[audience name]` 는 실제 대상자의 이름입니다. 대상 ID를 복사하여 이후 단계를 위해 저장합니다.

선택 **대상 이름 및 기본값** 다음을 확인합니다. **이메일 주소의 기본값** 은(는) 캠페인에 대한 올바른 값을 갖습니다. 대상 ID도 이 페이지의 맨 위에 나열되며 이 값은 마지막 단계에서 복사한 값과 동일합니다.

## Mailchimp 자동화

Mailchimp 플랜과 트랜잭션 이메일, 고객 여정 또는 기타 Mailchimp 자동화 사용 여부에 따라 특정 여정 설정이 다를 수 있습니다.

>[!IMPORTANT]
>  
>Mailchimp에서 자동화 또는 여정을 트리거하기 위해 선택한 이벤트 이름은 이 확장과 함께 보내야 하는 동일한 이벤트 이름입니다. Mailchimp 자동화에서 이벤트 이름을 기록하고 이후 단계를 위해 저장합니다.

## 설치 및 구성

이 섹션에서는 확장을 설치하고 구성하는 단계를 나열합니다. Mailchimp API 키를 안전하게 저장하려면 이벤트 전달을 사용해야 합니다 [비밀](../../../ui/event-forwarding/secrets.md).

### 암호 및 데이터 요소 만들기

이벤트 전달 속성에서 [만들기 [!UICONTROL 토큰] 비밀](../../../ui/event-forwarding/secrets.md#token) 호출됨 `Mailchimp API Key`.

다음, [데이터 요소 만들기](../../../ui/managing-resources/data-elements.md#create-a-data-element) 사용 [!UICONTROL 코어] 확장 및 a [!UICONTROL 암호] 참조할 데이터 요소 유형 `Mailchimp API Key` 방금 생성한 암호. 입력 `Mailchimp Token` 를 데이터 요소 이름으로 사용하십시오.

###  확장 설치 및 구성

동일한 이벤트 전달 속성에서 **[!UICONTROL 확장],** 그러면 **[!UICONTROL 카탈로그]** 을 클릭하여 설치에 사용할 수 있는 확장을 표시합니다. 여기에서 Mailchimp 확장을 검색한 다음 을 선택합니다. **[!UICONTROL 설치]**.

![Mailchimp 확장 설치](../../../images/extensions/server/mailchimp/install.png)

구성 화면이 나타납니다. 아래 **[!UICONTROL Mailchimp 서버 접두사 도메인 이름]**, 고유한 도메인 접두사를 포함하여 Mailchimp 계정에서 이전에 복사한 도메인을 입력합니다.

>[!IMPORTANT]
>
>포함하지 않음 `http://` 또는 `https://` 이 필드에서 을(를) 참조하십시오.

![확장 구성](../../../images/extensions/server/mailchimp/mailchimp-domain.png)

아래 **[!UICONTROL Mailchimp 토큰]**, 데이터 요소 아이콘을 선택하고 `Mailchimp Token` 이전에 만든 데이터 요소입니다. 선택 **[!UICONTROL 저장]** 변경 내용을 저장합니다.

이제 확장이 설치되고 속성에서 사용하도록 구성되었습니다.

## 데이터 수집

에서 이 확장을 사용할 때 [규칙](../../../ui/managing-resources/rules.md), 확장에서 각 이벤트와 함께 Mailchimp에 보내는 여러 데이터 값이 있습니다. 일반적인 구현의 경우 다음을 구성할 수 있습니다 [Adobe Experience Platform 웹 SDK 확장](../../client/web-sdk/overview.md) 해당 데이터를 (으)로 보내기 [!DNL Platform Edge Network] 이벤트 전달 속성에서 확장에서 사용하는 경우.

이 확장에 필요한 데이터는 Web SDK에서 XDM 데이터 또는 XDM이 아닌 데이터로 보낼 수 있습니다. 자세한 내용은 설명서 를 참조하십시오. [xdm 데이터 보내기](../../../../edge/fundamentals/tracking-events.md#sending-non-xdm-data).

예를 들어 고객이 사이트에서 이벤트를 구매하거나 등록하는 경우 이 확장 기능을 사용하여 Mailchimp를 통해 확인 이메일을 보낼 수 있습니다. Web SDK에서 Edge Network로 필수 정보를 전송하면 확장 프로그램에서 Mailchimp를 사용하여 이메일을 트리거합니다.

![이벤트 작업 구성 추가](../../../images/extensions/server/mailchimp/action-configurations.png)

### 데이터 요소

이전 섹션의 스크린샷은 이 확장에서 Mailchimp로 각 이벤트와 함께 보낼 수 있는 데이터를 보여 줍니다. 이 데이터를 Edge Network로 전송하도록 Web SDK를 구성하면 확장 프로그램이 해당 값에 액세스할 수 있도록 이벤트 전달 속성에서 데이터 요소를 만들 수 있습니다.

아래 표는 가능한 각 값에 대한 자세한 내용을 제공합니다.

| 이름 | 예제 경로 | 유형 | 설명 | 필수 여부 | 제한 |
|:---|:---:|:---:|:---|:---:|:---|
| `email` | `arc.event.xdm._tenant.emailId`<br /> 또는<br /> `arc.event.data._tenant.emailId` | 문자열 | 이메일을 받는 주소 | **예** | Mailchimp 대상에 있어야 합니다. |
| `listId` | `arc.event.xdm._tenant.listId`<br /> 또는<br /> `arc.event.data._tenant.listid` | 문자열 | 대상자 ID | **예** | 기존 대상 ID와 일치해야 함 |
| `name` | `arc.event.xdm._tenant.name`<br /> 또는<br /> `arc.event.data._tenant.name` | 문자열 | 이벤트 이름 | **예** | 2-30자 길이 |
| `properties` | `arc.event.xdm._tenant.properties`<br /> 또는<br /> `arc.event.data._tenant.properties` | 오브젝트 | 이벤트에 대한 세부 정보가 포함된 JSON 형식의 선택적 속성 목록 | 아니요 |  |
| `isSyncing` | `arc.event.xdm._tenant.isSyncing`<br /> 또는<br /> `arc.event.data._tenant.isSyncing` | 부울 | 다음으로 생성된 이벤트 `is_syncing` 을 로 설정 `true` **다음이 아님** 자동화 트리거 | 아니요 |  |
| `occurredAt` | `arc.event.xdm._tenant.occuredAt`<br /> 또는 `arc.event.data._tenant.occuredAt` | 문자열 | 이벤트가 발생한 시간의 ISO 8601 타임스탬프 | 아니요 |  |

{style="table-layout:auto"}

>[!IMPORTANT]
>  
>다음 **예제 경로** 위의 값은 예제에 불과합니다. 필드 이름 및 [경로](../../../ui/event-forwarding/overview.md#data-element-path) 이러한 데이터 요소에서 참조되는 요소는 위의 단계에서 Web SDK의 이름을 지정하고 구성한 방식에 따라 속성에서 다를 수 있습니다.

이벤트 전달 속성에서 위에 설명된 각 필드에 대한 데이터 요소를 만들 수 있습니다. 만든 후에는 의 데이터 요소를 참조할 수 있습니다. [!UICONTROL 이벤트 추가] 이 확장의 작업입니다.

![이벤트 작업 구성 추가](../../../images/extensions/server/mailchimp/action-configurations.png)

이제 이 확장 및 이벤트 추가 작업을 사용하여 대상에 대한 Mailchimp 이메일을 트리거할 수 있습니다.

## 데이터 유효성 검사

이벤트 전달 확장을 사용할 때 [Adobe Experience Platform 디버거](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) 매우 유용합니다. 로그 섹션의 에지 로그에서 이벤트 전달 규칙이 트리거된 후 수행한 요청을 볼 수 있습니다. 다음 스크린샷은 확장에 의해 Mailchimp API에 수행된 요청을 보여줍니다.

![Adobe Experience Platform 디버거](../../../images/extensions/server/mailchimp/debugger-edge-logs.png)

Mailchimp 대시보드의 활동 피드 보기에서 대상 또는 대상 구성원의 이벤트 목록이 제공됩니다. 이렇게 하려면 확장에서 전송한 이벤트와 일치해야 하며 수신한 이메일 또는 캠페인과 함께 전송된 모든 선택적 데이터를 표시해야 합니다. 다음을 참조하십시오. [Mailchimp 자동화 도움말 안내서](https://mailchimp.com/help/automation/) 을 참조하십시오.
