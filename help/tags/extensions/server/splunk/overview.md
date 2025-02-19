---
title: Splunk 확장 개요
description: Adobe Experience Platform의 이벤트 전달을 위한 Splunk 확장에 대해 알아봅니다.
exl-id: 653b5897-493b-44f2-aeea-be492da2b108
source-git-commit: 0d98183838125fac66768b94bc1993bde9a374b5
workflow-type: tm+mt
source-wordcount: '976'
ht-degree: 1%

---

# Splunk 확장 개요

[Splunk](https://www.splunk.com)은(는) 데이터에 대한 실행 가능한 통찰력을 위한 검색, 분석 및 시각화를 제공하는 가시성 플랫폼입니다. Splunk [이벤트 전달](../../../ui/event-forwarding/overview.md) 확장은 [Splunk HTTP 이벤트 수집기 REST API](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/HECRESTendpoints)를 활용하여 Adobe Experience Platform Edge Network에서 [Splunk HTTP 이벤트 수집기](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/UsetheHTTPEventCollector)로 이벤트를 전송합니다.

Splunk는 전달자 토큰을 인증 메커니즘으로 사용하여 Splunk 이벤트 수집기 API와 통신합니다.

## 사용 사례 {#use-cases}

마케팅 팀은 다음 사용 사례에 대해 확장을 사용할 수 있습니다.

| 활용 사례 | 설명 |
| --- | --- |
| 고객 행동 분석 | 조직은 웹 사이트에서 고객 상호 작용 이벤트 데이터를 캡처하고 관련 이벤트를 Splunk에 전달할 수 있습니다. 그런 다음 마케팅 및 분석 팀은 Splunk 플랫폼 내에서 후속 분석을 수행하여 주요 사용자 상호 작용 및 행동을 이해할 수 있습니다. Splunk 플랫폼은 그래프, 대시보드 또는 비즈니스 이해 당사자에게 알릴 수 있는 기타 시각화를 생성하는 데 사용할 수 있습니다. |
| 대규모 데이터 세트에서 확장 가능한 검색 | 조직은 웹 사이트에서 트랜잭션 또는 대화 입력을 이벤트 데이터로 캡처하고 이벤트를 Splunk에 전달할 수 있습니다. 그런 다음 Analytics 팀은 Splunk의 확장 가능한 인덱싱 기능을 활용하여 대규모 데이터 세트를 필터링 및 처리하여 비즈니스 통찰력을 도출하고 정보에 입각한 결정을 내릴 수 있습니다. |

{style="table-layout:auto"}

## 전제 조건 {#prerequisites}

이 확장을 사용하려면 Splunk 계정이 있어야 합니다. [Splunk 홈 페이지](https://www.splunk.com/page/sign_up)에서 Splunk 계정에 등록할 수 있습니다.

>[!NOTE]
>
> Splunk 확장은 Splunk Cloud 및 Splunk 엔터프라이즈 인스턴스를 모두 지원합니다. 이 안내서에서는 [Splunk Cloud](https://www.splunk.com/en_us/products/splunk-cloud-platform.html)를 참조로 사용하는 구현을 설명합니다. [Splunk Enterprise](https://www.splunk.com/en_us/products/splunk-enterprise.html)의 구성 프로세스는 비슷하지만 Splunk Enterprise 관리자의 특정 지침이 필요합니다.

확장을 구성하려면 다음 기술 값도 있어야 합니다.

* [이벤트 수집기 토큰](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/UsetheHTTPEventCollector#Create_an_Event_Collector_token_on_Splunk_Cloud_Platform). 토큰은 일반적으로 다음과 같은 UUIDv4 형식입니다. `12345678-1234-1234-1234-1234567890AB`.
* 조직의 Splunk 플랫폼 인스턴스 주소 및 포트입니다. 플랫폼 인스턴스 주소 및 포트는 일반적으로 `mysplunkserver.example.com:443` 형식을 갖습니다.

  >[!IMPORTANT]
  >
  > 이벤트 전달 내에서 참조된 splunk 끝점은 `443` 포트만 사용해야 합니다. 비표준 포트는 현재 이벤트 전달 구현에서 지원되지 않습니다.

## Splunk 확장 설치 {#install}

UI에 Splunk 이벤트 수집기 확장을 설치하려면 **이벤트 전달**(으)로 이동하여 확장을 추가할 속성을 선택하거나 대신 새 속성을 만듭니다.

원하는 속성을 선택하거나 만든 후에는 **확장** > **카탈로그**(으)로 이동합니다. &quot;[!DNL Splunk]&quot;을(를) 검색한 다음 Splunk 확장에서 **[!DNL Install]**&#x200B;을(를) 선택합니다.

![UI에서 Splunk 확장에 대한 설치 단추 선택 중](../../../images/extensions/server/splunk/install.png)

## Splunk 확장 구성 {#configure_extension}

>[!IMPORTANT]
>
>구현 요구 사항에 따라 확장을 구성하기 전에 스키마, 데이터 요소 및 데이터 세트를 만들어야 할 수 있습니다. 사용 사례에 대해 설정해야 하는 엔터티를 결정하려면 시작하기 전에 모든 구성 단계를 검토하십시오.

왼쪽 탐색에서 **확장**&#x200B;을 선택합니다. **설치됨**&#x200B;에서 Splunk 확장의 **구성**&#x200B;을 선택합니다.

![UI에서 Splunk 확장에 대한 구성 단추를 선택하고 있습니다](../../../images/extensions/server/splunk/configure.png)

**[!UICONTROL HTTP 이벤트 수집기 URL]**&#x200B;에 Splunk 플랫폼 인스턴스 주소와 포트를 입력하십시오. **[!UICONTROL 액세스 토큰]**&#x200B;에서 [!DNL Event Collector Token] 값을 입력하십시오. 완료되면 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

![UI에 구성 옵션이 입력됨](../../../images/extensions/server/splunk/input.png)

## 이벤트 전달 규칙 구성 {#config_rule}

새 이벤트 전달 규칙 [규칙](../../../ui/managing-resources/rules.md)을(를) 만들고 원하는 대로 조건을 구성하십시오. 규칙에 대한 작업을 선택할 때 [!UICONTROL Splunk] 확장을 선택한 다음 [!UICONTROL 이벤트 만들기] 작업 유형을 선택합니다. Splunk 이벤트를 추가로 구성하는 추가 컨트롤이 나타납니다.

![작업 구성 정의](../../../images/extensions/server/splunk/action-configurations.png)

다음 단계는 Splunk 이벤트 속성을 이전에 만든 데이터 요소에 매핑하는 것입니다. 설정할 수 있는 입력 이벤트 데이터를 기반으로 지원되는 선택적 매핑은 아래에 나와 있습니다. 자세한 내용은 [Splunk 설명서](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/FormateventsforHTTPEventCollector#Event_metadata)를 참조하세요.

| 필드 이름 | 설명 |
| --- | --- |
| [!UICONTROL 이벤트&#x200B;]<br><br>**(필수)** | 이벤트 데이터를 제공할 방법을 지정합니다. 이벤트 데이터는 HTTP 요청에서 JSON 개체 내의 `event` 키에 할당되거나 원시 텍스트일 수 있습니다. `event` 키가 JSON 이벤트 패킷 내의 메타데이터 키와 동일한 수준에 있습니다. `event` 키-값 중괄호 내에서 데이터는 문자열, 숫자, 다른 JSON 개체 등 필요한 모든 형식일 수 있습니다. |
| [!UICONTROL 호스트] | 데이터를 보내는 클라이언트의 호스트 이름입니다. |
| [!UICONTROL Source 유형] | 이벤트 데이터에 할당할 소스 유형입니다. |
| [!UICONTROL Source] | 이벤트 데이터에 지정할 소스 값입니다. 예를 들어 개발 중인 앱에서 데이터를 전송하는 경우 이 키를 앱 이름으로 설정합니다. |
| [!UICONTROL 인덱스] | 이벤트 데이터 인덱스의 이름입니다. 토큰에 index 매개 변수가 설정된 경우 여기서 지정하는 인덱스는 허용된 인덱스 목록 내에 있어야 합니다. |
| [!UICONTROL 시간] | 이벤트 시간. 기본 시간 형식은 UNIX 시간(`<sec>.<ms>` 형식)이며 로컬 시간대에 따라 다릅니다. 예를 들어 `1433188255.500`은(는) 에포크 후 1433188255초 및 500밀리초 또는 2015년 6월 1일 월요일 오후 7시:50:55분 GMT를 나타냅니다. |
| [!UICONTROL 필드] | 인덱스 시간에 정의할 명시적 사용자 지정 필드가 포함된 원시 JSON 개체 또는 키-값 쌍 집합을 지정합니다.  `fields` 키는 원시 데이터에 적용할 수 없습니다.`fields` 속성이 포함된 <br><br>요청을 `/collector/event` 끝점으로 보내야 합니다. 그렇지 않으면 인덱싱되지 않습니다. 자세한 내용은 [인덱싱된 필드 추출](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/IFXandHEC)에 대한 Splunk 설명서를 참조하십시오. |

### Splunk 내의 데이터 유효성 검사 {#validate}

이벤트 전달 규칙을 만들고 실행한 후 Splunk API로 전송된 이벤트가 Splunk UI에 예상대로 표시되는지 확인합니다. 이벤트 컬렉션 및 Experience Platform 통합이 성공하면 다음과 같이 Splunk 콘솔 내에 이벤트가 표시됩니다.

![유효성 검사 중에 Splunk UI에 표시되는 이벤트 데이터](../../../images/extensions/server/splunk/splunk-data.png)

## 다음 단계

이 문서에서는 UI에서 Splunk 이벤트 전달 확장 기능을 설치하고 구성하는 방법에 대해 다룹니다. Splunk에서 이벤트 데이터를 수집하는 방법에 대한 자세한 내용은 공식 설명서를 참조하십시오.

* [Splunk Web에서 HTTP 이벤트 수집기 설정 및 사용](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/UsetheHTTPEventCollector)
* [토큰을 사용하여 인증 설정](https://docs.splunk.com/Documentation/Splunk/8.2.5/Security/Setupauthenticationwithtokens#Prerequisites_for_activating_tokens)
* [HTTP 이벤트 수집기 문제 해결](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/TroubleshootHTTPEventCollector)&#x200B;(또한 [가능한 오류 코드 ](https://docs.splunk.com/Documentation/Splunk/8.2.5/Data/TroubleshootHTTPEventCollector#Possible_error_codes)의 표준 목록)
