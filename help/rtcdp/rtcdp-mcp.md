---
solution: Real-Time Customer Data Platform
title: MCP 클라이언트(Beta) 작업
description: MCP 서버를 사용하여 Adobe Real-Time CDP을 MCP 클라이언트에 연결하는 방법에 대해 알아봅니다
feature: Integrations
topic: Content Management, Artificial Intelligence
badge: label="Beta" type="Informative"
role: User, Developer
level: Beginner, Intermediate
hide: true
hidefromtoc: true
exl-id: 48dba0d2-7df9-4d76-bc87-5af49a8a40cc
source-git-commit: 8a9dd740bb210ef125bca65a8358bb6b51f6d28f
workflow-type: tm+mt
source-wordcount: '2379'
ht-degree: 0%

---

# MCP 클라이언트(Beta) 작업 {#rtcdp-mcp}

API 호출을 작성하거나 제품 화면을 탐색하지 않고도 Adobe Real-Time CDP MCP 통합을 사용하여 일반 언어 프롬프트를 사용하여 대상, 대상 및 활성화 상태를 쿼리할 수 있습니다. 이 페이지에서는 통합 작동 방식, 통합 기능으로 수행할 수 있는 작업 및 시작 방법을 설명합니다.

>[!AVAILABILITY]
>
>Real-Time CDP MCP 서버는 사용자가 지원되는 MCP 클라이언트 및 앱 플랫폼(예: Claude, ChatGPT, Claude Code, Codex, Cursor 또는 VS Code)에 설치하고 구성하는 **원격 HTTP 전송 서버**(으)로 배포됩니다. 인증은 **브라우저 기반 로그인 흐름**&#x200B;을 통해 처리됩니다. — 클라이언트가 처음 서버에 연결되면 기본 브라우저가 열리고 Adobe 자격 증명으로 로그인하고 액세스 권한을 부여할 수 있습니다. 이 Beta 프로그램에 액세스하려면 Adobe 담당자에게 문의하십시오.

## Beta, 보안 및 법적 고지 사항 {#mcp-notices}

**Beta 설명서 알림:** 이 설명서는 Beta 기능을 다루고 있으며 최종 설명서를 구성하지 않습니다. 여기에 설명된 콘텐츠는 Beta 릴리스와 관련되며, 일반 공급 이전에 변경될 수 있습니다. Adobe은 이 설명서의 완벽성이나 정확성에 대해 어떠한 표현도 하지 않습니다.

Adobe Real-Time CDP MCP 서버(Beta)(&quot;Beta&quot;)를 사용하면 Beta이 어떠한 종류의 보증도 없이 **&quot;있는 그대로&quot; 제공된다는 것을 인정합니다**. Adobe은 Beta을 유지, 수정, 업데이트, 변경, 수정 또는 지원할 의무가 없습니다. 이러한 Beta 및/또는 동봉된 자료의 올바른 기능이나 성능에 어떤 식으로든 의존하지 말고 주의하는 것이 좋습니다. Beta은 Adobe의 기밀 정보로 간주됩니다. 귀하가 Adobe에 제공한 &quot;피드백&quot;(Beta 사용 중 발생하는 문제 또는 결함, 제안, 개선 사항 및 권장 사항을 포함하되 이에 제한되지 않는 Beta 관련 정보)은 해당 피드백에 대한 모든 권한, 제목 및 관심을 포함하여 Adobe에 할당됩니다.

>[!WARNING]
>
>MCP(Model Context Protocol)는 새로운 오픈 소스 표준이며 보안 또는 신뢰성 위험을 제시할 수 있습니다. Adobe MCP 서버 통합 및 관련 설명서는 어떠한 종류의 보증도 없이 &quot;있는 그대로&quot; 제공됩니다.
>
>MCP 클라이언트 또는 서버를 Adobe 제품에 연결하는 것은 고객이 선택한 구성입니다. 고객은 MCP 통합의 보안 및 적합성을 평가할 책임이 있습니다. Adobe은 잘못된 구성, MCP 오용, 서드파티 구현의 취약점 또는 MCP 지원 워크플로우를 통해 수행된 의도하지 않은 작업으로 인해 발생하는 문제에 대해 책임을 지지 않습니다.
>
>위험을 줄이기 위해 Adobe에서는 생산적 사용을 시작하기 전에 샌드박스 환경에서 통합을 테스트하고, 이를 확인하거나 의존하기 전에 모든 MCP에서 시작한 작업과 응답을 주의 깊게 검토하고 유효성을 검사하는 것을 권장합니다.

## 모델 컨텍스트 프로토콜이란 무엇입니까? {#mcp-overview}

마케팅, 데이터 및 고객 경험 팀은 일상적인 작업을 간소화하기 위해 Anthropic Claude, OpenAI ChatGPT, Cursor 및 Microsoft Copilot Studio와 같은 채팅 기반 애플리케이션과 개발자 도구에 점점 더 의존하고 있습니다. 이러한 응용 프로그램은 응용 프로그램이 백엔드 도구를 대형 언어 모델(LLM)에 균일한 방식으로 노출할 수 있도록 해주는 개방형 표준인 **MCP(Model Context Protocol)**&#x200B;을 지원합니다.

Real-Time CDP은 이제 모든 MCP 호환 애플리케이션 내에서 직접 대상자, 대상 및 활성화 작업을 표시하는 MCP 서버를 제공합니다. Real-Time CDP MCP 통합을 통해 서로 다른 가상 사용자가 Adobe Experience Platform REST API에 대한 쿼리를 작성하거나 여러 UI 화면을 탐색하지 않고도 동일한 세분화 및 활성화 데이터에 대해 공동 작업을 수행할 수 있습니다. 고객은 대화식으로 자신의 의도를 설명하고 LLM이 적절한 MCP 도구를 호출하도록 할 수 있다.

## 주요 기능 {#mcp-capabilities}

Real-Time CDP MCP 서버를 사용하면 AI 어시스턴트에서 직접 대상과 대상을 검사하고, 요약하고, 문제를 해결할 수 있습니다. 모든 작업은 **읽기 전용**&#x200B;입니다. MCP 서버 표면이 API를 일반 언어 답변으로 검색하므로 다음을 수행할 수 있습니다.

* **즉각적인 대상 가시성 확보** - 메뉴를 탐색하거나 보고서를 수동으로 가져오지 않고 대상 정의, 라이프사이클 상태 및 네임스페이스에 대해 일반 언어로 질문합니다.
* **활성화 전 대상 크기 예상** - 대상 빌드를 약속하기 전에 PQL 또는 SDD 세그먼트 쿼리에 대한 멤버십 카운트 및 신뢰 구간을 미리 봅니다.
* **활성화 포트폴리오 감사** — JSON을 구문 분석하거나 제품 화면 사이를 이동하지 않고 구성된 대상, 해당 대상에 제공되는 데이터 흐름 및 각 흐름 뒤의 소스/타겟 연결을 검토합니다.
* **활성화 문제를 조기에 발견** — 표면이 실패했거나 진행 중인 대상이 요청한 즉시 실행되므로 팀이 빠르게 작업할 수 있습니다.
* **라이브 데이터를 중심으로 공동 작업** - 마케터, 데이터 엔지니어 및 이해 당사자는 모두 AI 도우미를 통해 동일한 라이브 Real-Time CDP 데이터를 쿼리할 수 있으므로 더 쉽게 정렬, 결정 및 이동할 수 있습니다.

## 사용 가능한 도구 {#mcp-tools}

새로운 툴을 사용할 수 있게 되면서 툴 가용성이 빠르게 변화하고 있습니다. 사용 가능한 최신 도구 목록을 얻으려면 Adobe 담당자에게 문의하십시오.

>[!NOTE]
>
>모든 도구는 **읽기 전용**&#x200B;입니다. 현재 Beta 릴리스에서는 쓰기 작업(대상, 대상 또는 데이터 흐름 만들기, 업데이트 또는 삭제)이 지원되지 않습니다.

## 사용 사례 {#mcp-use-cases}

다음 예제는 자연어를 사용하여 [!DNL Adobe Real-Time CDP] MCP 서버와 상호 작용하는 방법을 보여 줍니다.

| 목표 | 예제 프롬프트 |
| --- | --- |
| **대상 카탈로그 검색** | &quot;TikTok을 내 샌드박스에서 대상으로 사용할 수 있습니까?&quot; / &quot;계정이 이미 구성되어 있는 대상 유형은 무엇입니까?&quot; |
| **유형별 대상 인벤토리** | &quot;모든 Amazon S3 대상을 나열합니다.&quot; / &quot;데이터 세트 내보내기 대상을 설정했습니까?&quot; |
| **대상 구성 감사** | &quot;내 `Loyalty S3 Export` 대상이 쓰는 버킷은 무엇입니까?&quot; / &quot;데이터 흐름 [ID]에 대한 대상 경로와 파일 형식을 표시합니다.&quot; |
| **계정 상태** | &quot;내 대상 계정 중 만료된 자격 증명이 있는 계정은 무엇입니까?&quot; / &quot;오류 상태에 있는 Pinterest 또는 Facebook 계정이 있습니까?&quot; |
| **활성화 상태 — 지난 24시간** | &quot;지난 24시간 동안 실행되지 않은 모든 대상을 나열합니다.&quot; / &quot;내 데이터 세트 내보내기 대상에서 지난 24시간 내에 데이터를 전송했습니까?&quot; |
| 대상별 **활성화 기록** | &quot;지난 30일 동안 `Weekly Loyalty Export`에서 내보낸 항목이 있습니까?&quot; / &quot;{NAME} 대상에 대한 전체 실행 기록을 표시합니다.&quot; |
| **실패 분석** | &quot;이번 주 내 파일 기반 대상에서 가장 일반적인 실패 이유는 무엇입니까?&quot; / &quot;최근 실패한 실행을 오류 유형별로 그룹화합니다.&quot; |
| **대상 검색 및 필터링** | &quot;`marketing-prod` 샌드박스의 모든 CSV 기반 대상을 나열합니다.&quot; / &quot;외부 대상 ID가 정의된 대상은 무엇입니까?&quot; |
| **대상 크기 조정 감사** | &quot;크기가 0인 대상자를 모두 표시&quot; / &quot;1,000개 프로필보다 큰 대상자는 무엇입니까?&quot; |
| **대상 만료 감사** | &quot;종료 날짜가 이미 지난 대상이 있는 대상은 무엇입니까?&quot; / &quot;향후 7일 이내에 만료될 예정인 대상자를 나열합니다.&quot; |
| **대상 활성화 풋프린트** | &quot;10명 이상의 대상이 활성화된 대상은 무엇입니까?&quot; / &quot;어떤 대상자가 가장 많은 대상에 활성화됩니까?&quot; |
| **교차 필터: 대상자 × 활성화** | &quot;크기가 1,000보다 크고 최소 2개의 대상에서 활성화된 대상자를 표시합니다.&quot; / &quot;단일 대상에만 활성화된 대규모 대상&quot; |
| **대상자 멤버십 미리 보기** | &quot;대상 `High-Value Loyalty Members`의 멤버 자격 크기를 미리 봅니다.&quot; / &quot;저장하기 전에 이 PQL 쿼리의 크기를 예상합니다. {EXPRESSION}.&quot; |

## 전제 조건 {#mcp-prerequisites}

Real-Time CDP MCP 서버를 MCP 클라이언트에 연결하기 전에 다음 사항을 확인하십시오.

* 활성 Real-Time CDP 라이선스가 있습니다.
* 사용자는 Claude, ChatGPT, Claude Code, Codex, Cursor 또는 VS Code와 같은 원격 MCP 서버 또는 사용자 지정 MCP 앱에 연결할 수 있는 지원되는 클라이언트에 액세스할 수 있습니다.
* 조회할 조직 ID와 샌드박스의 이름이 있습니다.
* Adobe Experience Platform에서 대상자, 대상 및 흐름 서비스 엔티티를 보는 데 필요한 권한이 있습니다.

## Real-Time CDP MCP 서버 연결 {#mcp-connect}

>[!NOTE]
>
>이 통합은 Beta에 있습니다. 클라이언트 메뉴, 계획 요구 사항 및 관리 컨트롤은 애플리케이션 및 버전에 따라 다를 수 있습니다.

시작하기 전에 다음을 확인하십시오.

* MCP 서버 끝점 URL: `Available to Beta customers through your Adobe representative`.
* Adobe 사용자에게 타겟 Experience Platform 조직 및 샌드박스에 대한 액세스 권한이 있는지 확인합니다.

Real-Time CDP MCP 서버는 **원격 HTTP MCP 서버**&#x200B;입니다. 모든 클라이언트에서 설정은 동일한 패턴을 따릅니다.

1. 서버 URL을 추가합니다.
2. 연결을 저장하거나 활성화합니다.
3. 클라이언트가 도구를 처음 호출할 때 **브라우저 기반 Adobe 로그인**&#x200B;을 완료합니다.
4. 각 요청에 `imsOrgId` 및 `sandboxName`을(를) 제공합니다.

### UI 기반 클라이언트에 설치 {#mcp-connect-ui}

#### 클로드

`claude.ai` 및 Cloud Desktop의 경우 Adobe 담당자가 제공한 끝점을 사용하여 Real-Time CDP MCP 서버를 **사용자 지정 커넥터**(으)로 추가하십시오. 개별 클라우드 계획에서 **사용자 지정 > 커넥터**&#x200B;에 추가하십시오. Team 및 Enterprise 계획에서 소유자는 **조직 설정 > 커넥터**&#x200B;에 먼저 추가한 후 각 사용자가 고유한 클라우드 설정으로 연결해야 할 수 있습니다. 구성하고 나면 대화에서 커넥터를 활성화하고 최초 사용 시 Adobe 브라우저 로그인을 완료합니다.

#### ChatGPT

ChatGPT에서 Adobe 담당자가 제공한 끝점을 사용하여 Real-Time CDP MCP 서버를 **사용자 지정 앱/커넥터**(으)로 추가합니다. ChatGPT 계획에 따라 **개발자 모드** 및 작업 영역 관리자 승인이 필요할 수 있습니다. 앱/커넥터를 만들거나 활성화한 후 **설정 > 앱** 또는 **설정 > 앱 및 커넥터**&#x200B;에서 연결한 다음 메시지가 표시되면 Adobe 브라우저 로그인을 통해 인증합니다.

#### 커서

Cursor에서 Adobe 담당자가 제공한 끝점을 사용하여 Real-Time CDP MCP 서버를 원격 MCP 서버로 추가합니다. **설정 > MCP**&#x200B;를 열고 새 서버를 추가하고 끝점 URL을 붙여 넣습니다. 추가한 후에는 브라우저를 통해 인증할 **연결**&#x200B;을 선택하여 작업 영역에 대해 서버를 사용하도록 설정하십시오.

#### 기타 UI 기반 클라이언트

VS 코드 또는 원격 MCP를 지원하는 기타 데스크톱 및 웹 애플리케이션과 같은 클라이언트의 경우, Adobe 담당자가 제공한 끝점을 사용하여 Real-Time CDP MCP 서버를 **원격 HTTP** 서버로 추가하십시오. 클라이언트가 선택적 헤더 또는 전달자 토큰을 지원하는 경우 Adobe이 별도로 지시하지 않는 한 비워 두십시오. 인증은 처음 사용할 때 브라우저 기반 Adobe 로그인 흐름을 통해 처리됩니다.

### 기술 클라이언트에 설치 {#mcp-connect-technical}

#### 클로드 코드

터미널에서 서버를 추가합니다.

```bash
claude mcp add --transport http rtcdp <endpoint provided by your Adobe representative>
```

그런 다음 클라우드 코드를 시작하고 다음을 실행합니다.

```text
/mcp
```

`rtcdp` 서버를 선택하고 브라우저에서 Adobe 로그인 흐름을 완료합니다. `claude.ai`에 서버를 이미 추가한 경우 둘 다 동일한 계정을 사용하는 경우 클라우드 코드에도 자동으로 표시될 수 있습니다.

#### 코덱스

터미널에서 서버를 추가합니다.

```bash
codex mcp add rtcdp --url <endpoint provided by your Adobe representative>
```

서버 인증:

```bash
codex mcp login rtcdp
```

구성을 확인합니다.

```bash
codex mcp list
```

서버를 `~/.codex/config.toml`에 직접 추가할 수도 있습니다.

```toml
[mcp_servers.rtcdp]
url = "<endpoint provided by your Adobe representative>"
```

### 필수 요청 매개 변수 {#mcp-connect-params}

모든 도구 호출에는 요청의 범위를 지정하는 두 개의 매개 변수가 필요합니다.

* `imsOrgId` — 다운스트림 Experience Platform API 호출의 `x-gw-ims-org-id` 헤더에 매핑된 조직 ID.
* `sandboxName` — `x-sandbox-name` 헤더에 매핑된 Experience Platform 샌드박스 이름입니다.

## 알려진 제한 사항(Beta) {#mcp-limitations}

다음 제한 사항은 [!DNL Adobe Real-Time CDP] MCP 서버의 현재 Beta 릴리스에 적용됩니다.

| 제한 사항 | 설명 | 해결 방법 |
| --- | --- | --- |
| **읽기 전용 표면** | MCP 서버는 검색 API만 노출합니다. 대상, 대상 또는 데이터 흐름을 만들거나, 업데이트하거나, 활성화하거나, 삭제할 수 없습니다. | 쓰기 작업에는 Real-Time CDP UI 또는 AEP REST API를 사용하십시오. |
| **참여 또는 게재 지표 없음** | MCP 서버는 대상 플랫폼에서 다운스트림 게재 통계, 참여 또는 전환 지표를 반환하지 않습니다. | 참여 및 전환 데이터에 대상 플랫폼의 자체 보고, Customer Journey Analytics MCP 또는 Adobe Analytics MCP를 사용합니다. |
| **세그먼트 쿼리는 외부에서 작성해야 합니다** | `Preview Audience Membership`은(는) 올바른 PQL 또는 SDD 식을 입력해야 합니다. MCP 서버가 쿼리를 작성하지 않습니다. | 세그먼트 빌더 UI나 세그먼테이션 서비스 API를 통해 PQL/SDD 표현식을 작성한 다음 MCP 프롬프트에 붙여넣습니다. |
| **연속 토큰을 통한 페이지 매김** | 목록 도구는 페이지가 매겨진 결과를 반환합니다. 매우 큰 샌드박스에서 전체 열거형을 사용하려면 `continuationToken` 호출을 체인 처리해야 합니다. | 전체 목록을 열거하지 않고 필터(이름, 상태, 연결 사양, 시간 범위)를 사용하여 쿼리 범위를 좁힙니다. |
| **활성화 실행 필터링은 시간을 기반으로 합니다** | `Inspect Activation Runs`은(는) 상태 및 완료 타임스탬프(epoch ms UTC)별 필터링을 지원하지만 오류 유형 또는 대상 플랫폼별로는 지원하지 않습니다. | `List Configured Destinations`에서 가져온 `flowId`을(를) 기준으로 특정 대상에 대한 범위 실행을 필터링합니다. |
| **지역 구성이 필요합니다** | MCP 게이트웨이가 사용자 지역에 대해 구성되지 않은 경우 HTTP 403 &quot;사용자 지역이 누락되었습니다.&quot;로 도구 호출이 실패합니다. | 처음 사용하기 전에 Adobe 담당자에게 문의하여 지역에 맞게 게이트웨이가 구성되었는지 확인하십시오. |

## 자주 묻는 질문 {#mcp-faq}

+++지원되는 MCP 클라이언트는 무엇입니까?

Real-Time CDP MCP 서버는 Claude, ChatGPT, Claude Code, Codex, Cursor 및 VS Code를 포함하여 원격 MCP 서버 또는 사용자 지정 MCP 앱에 연결할 수 있는 지원되는 클라이언트와 연동합니다. 설정 흐름은 클라이언트에 따라 다릅니다. 일반적으로 UI 기반 클라이언트는 설정에서 서버를 추가하는 반면, 클라우드 코드 및 코드와 같은 기술 클라이언트는 명령줄 또는 구성 파일에서 추가할 수 있습니다.
+++

+++인증은 어떻게 작동합니까?

인증은 **브라우저 기반 로그인**&#x200B;을 통해 처리됩니다. MCP 클라이언트가 도구를 처음 호출하면 기본 브라우저에서 Adobe 로그인 페이지가 열립니다. 클라이언트를 인증하고 권한을 부여하면 세션이 설정되고 후속 도구 호출이 재사용됩니다. 클라이언트 구성에 API 키 또는 장기 자격 증명을 저장할 필요가 없습니다.
+++

+++MCP를 통해 액세스할 수 있는 Real-Time CDP 오브젝트는 무엇입니까?

대상자, 대상 유형, 구성된 대상 계정, 대상 데이터 흐름, 소스 및 타겟 연결, 활성화 실행 기록에 액세스할 수 있습니다. 작업은 읽기 전용(API 검색)이며 쓰기 작업은 현재 릴리스에서 지원되지 않습니다.
+++

+++Real-Time CDP MCP 서버를 사용하려면 개발자 액세스 권한이 필요합니까?

아니요. MCP 서버는 마케팅 및 기술 담당자 모두를 위해 설계되었습니다. 마케터는 지원되는 모든 MCP 클라이언트에서 자연어 프롬프트를 사용하여 상호 작용할 수 있으며, 데이터 엔지니어 및 개발자는 MCP를 지원하는 개발자 도구에서 사용할 수 있습니다.
+++

+++내 데이터가 MCP 클라이언트 공급자에게 전송됩니까?

프롬프트를 제출하면 MCP 클라이언트는 관련 컨텍스트(MCP 서버에서 반환된 Real-Time CDP 데이터 포함)를 처리를 위해 해당 모델에 보낼 수 있습니다. 프로덕션 데이터에 연결하기 전에 MCP 클라이언트 공급자의 개인정보 보호 및 데이터 처리 정책을 검토하십시오.
+++

+++Real-Time CDP에서 어떤 권한이 필요합니까?

쿼리할 개체(대상, 대상 및 흐름 서비스 엔터티)에 대해 최소 **보기** 권한이 필요합니다. MCP 서버는 읽기 작업만 수행하므로 쓰기 권한이 필요하지 않습니다. 현재 액세스 수준을 잘 모를 경우 [!DNL Adobe Experience Platform] 관리자에게 문의하십시오.
+++

+++샌드박스 환경에서 MCP 서버를 사용할 수 있습니까?

예. 모든 도구 호출에는 `sandboxName` 매개 변수가 필요하므로 MCP 서버는 항상 [!DNL Adobe Experience Platform] 샌드박스 구성을 준수합니다. 프롬프트에 샌드박스 이름을 지정하여 액세스 권한이 있는 모든 샌드박스를 쿼리할 수 있습니다.
+++

+++대상자 멤버십 미리보기 와 기존 대상자 검색 의 차이점은 무엇입니까?

`Search Existing Audiences`이(가) 이미 작성되어 샌드박스에 저장된 대상을 반환합니다. `Preview Audience Membership`은(는) 원시 PQL 또는 SDD 세그먼트 식을 가져와서 예상 크기를 반환합니다. 대상자로 저장하는 *이전* 쿼리 크기를 조정하는 데 유용합니다.
+++

+++프로필 대상뿐만 아니라 계정 대상도 쿼리할 수 있습니까?

예. `Search Existing Audiences`과(와) `Preview Audience Membership` 모두 엔터티 형식 매개 변수를 지원합니다. 프로필 대상은 PQL 또는 SDD로 표현할 수 있습니다. 계정 대상은 항상 SDD(관계형) 구문을 사용합니다.
+++
