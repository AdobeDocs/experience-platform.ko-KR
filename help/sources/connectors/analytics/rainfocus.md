---
title: RainFocus 소스 개요
description: RainFocus 계정의 이벤트 관리 및 분석 데이터를 Experience Platform으로 가져오는 방법에 대해 알아봅니다
badge: 베타
hide: true
hidefromtoc: true
source-git-commit: e9728e1e673a4018d1d776a9d9ddad023ad1393e
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 5%

---

# [!DNL RainFocus]

>[!NOTE]
>
>다음 [!DNL RainFocus] 소스는 베타 버전입니다. 다음을 읽으십시오. [소스 개요](../../home.md#terms-and-conditions) beta 레이블 소스를 사용하는 방법에 대한 자세한 내용.

[!DNL RainFocus] 는 이벤트를 홍보하고 대상을 구축하는 데 사용할 수 있는 플랫폼입니다. 다음을 사용할 수 있습니다. [!DNL RainFocus] 아름다운 홍보 페이지를 만들고, 캠페인 성과를 추적하고, 등록 전환을 최적화합니다.

사용 [!DNL RainFocus] 실시간으로 참석자 경험 이벤트를 통해 고객 데이터 프로필을 자동으로 보강하는 Adobe Experience Platform 및 Real-time Customer Data Platform 소스. 활성화되면 경험 여정이 자동으로 Real-Time CDP으로 스트리밍되어 강력한 대상 세분화, 데이터 분석 및 Customer Journey Analytics 및 Adobe Journey Optimizer과 같은 다운스트림 대상 및 애플리케이션으로 참석자 이벤트를 활성화할 수 있습니다.

>[!IMPORTANT]
>
>이 설명서 페이지는 다음 사용자가 만들었습니다. [!DNL RainFocus] 팀. 문의 사항이나 업데이트 요청은 클라이언트 지원팀에 직접 문의하십시오.<span>@rainfocus.com 또는 [[!DNL RainFocus] 도움말 센터](https://help.rainfocus.com/hc/en-us)

## 사전 요구 사항

다음을 활성화하려면 먼저 전제 조건을 완료해야 합니다. [!DNL RainFocus] Experience Platform 통합:

[Adobe Developer 포털에서 Adobe 서비스 계정(JWT) 만들기](https://developer.adobe.com/developer-console/docs/guides/authentication/ServiceAccountIntegration/)

>[!IMPORTANT]
>
>Adobe은 최근 OAuth를 위해 JWT 토큰의 사용 중단을 발표했습니다. 이 변경 사항을 수용하기 위해 [!DNL RainFocus] 소스는 가까운 미래에 OAuth로 마이그레이션됩니다.

### 필요한 자격 증명 수집

연결하려면 [!DNL RainFocus] Experience Platform을 수행하려면 다음 연결 속성에 대한 값을 제공해야 합니다. [!DNL RainFocus]:

| 자격 증명 | 설명 | 예 |
| --- | --- | --- |
| 클라이언트 ID | 클라이언트 ID는 Adobe Developer 포털의 Adobe 서비스 계정에서 가져올 수 있습니다. | `b9c32a63e7d41a0f87d3e8b52a16e7a2` |
| 클라이언트 암호 | 클라이언트 암호는 Adobe Developer 포털의 Adobe 서비스 계정에서 가져올 수 있습니다. | `k1b-p-umplcjtg_arnw-R-Bx44bybu` |
| 기술 계정 ID | 기술 계정 ID는 Adobe Developer 포털의 Adobe 서비스 계정에서 가져올 수 있습니다. | `B3F9D2E8A64C573D21ABFE97@techacct.adobe.com` |
| 조직 ID | 조직 ID는 Adobe Developer 포털의 Adobe 서비스 계정에서 가져올 수 있습니다 | `D9A6F3BCE82FD147C50E3A19@techacct.adobe.com` |

### XDM 스키마 만들기 및 ID 필드 정의 {#create-an-xdm-schema-and-define-the-identity-field}

에서 경험 이벤트를 저장하기 위해 [!DNL RainFocus] Experience Platform에서 전송될 수 있는 필드 및 데이터 유형을 저장할 수 있는 데이터 세트를 설명하는 XDM(경험 데이터 모델) 스키마를 만들어야 합니다 [!DNL RainFocus].

[!DNL RainFocus] 는 기본적으로 전송되는 모든 가능한 데이터를 다루는 다음 필드를 권장합니다.

또한 다음 필드 그룹이 권장됩니다(접두사로 표시).

* 참석자
* 전시자
* 리드
* Session
* 세션 시간

**스키마에는 다음 필드가 포함되어야 합니다.**

| 필드 | 유형 | 예 | 설명 |
| --- | --- | --- | --- |
| `attendee.registered` | 문자열 | 예 | 참석자가 등록된 것으로 간주되는지 여부를 결정하는 플래그입니다. |
| `attendee.attendeeId` | 문자열 | 1619119968857001fvLB | 의 참석자 ID [!DNL RainFocus]. |
| `attendee.externalId` | 문자열 | 1666809456617001wyPj | 조직에서 지정한 외부 ID. |
| `attendee.clientId` | 문자열 | 8EFC1F57631CAFE70A495ECB@8f3f1f5c631caf3e495fd8.e | 참석자 SSO 클라이언트 ID. |
| `attendee.email` | 문자열 | 사용자<span>@company.com | 참석자의 이메일 주소입니다. |
| `transmissionId` | 문자열 | 1680309557133001YHhz | 데이터 푸시에 사용되는 고유 식별자입니다. |
| `eventType` | 문자열 | 세션 예약됨 | 참석자 경험 이벤트의 이름입니다. |
| `timestamp` | DateTime | 2023-04-01T:41:57.000Z | 데이터 푸시의 타임스탬프입니다. |
| `event.name` | 문자열 | Adobe Summit 2023 | 전송이 발생한 이벤트의 이름입니다. |
| `exhibitor.exhibitorId` | 문자열 | 1680309557133001YHhz | 다음 [!DNL RainFocus] 방문자 식별자. |
| `exhibitor.externalId` | 문자열 | 1666809514105001lSJN | 클라이언트 시스템의 전시자에 대한 식별자. |
| `exhibitor.name` | 문자열 | IBM | 전시자의 이름. |
| `lead.leadId` | 문자열 | 1666809456617001wyPj | 다음 [!DNL RainFocus] 잠재 고객 식별자. |
| `lead.note` | 문자열 | | |
| `session.sessionId` | 문자열 | 1666809373585001t4aV | 다음 [!DNL RainFocus] 세션의 식별자입니다. |
| `session.externalId` | 문자열 | 1666809456617001wyPj | 클라이언트 시스템의 세션에 대한 식별자입니다. |
| `session.code` | 문자열 | GS3 | 세션에 대한 코드입니다. |
| `session.title` | 문자열 | Inspiration Keynote | 세션의 제목입니다. |
| `session.length` | 정수 | 90 | 세션 길이입니다. |
| `sessiontime.sessiontimeId` | 문자열 | 1673033149739001OJLZ | 다음 [!DNL RainFocus] 세션 시간 식별자. |
| `sessiontime.startTime` | 문자열 | 2023-03-22 10:00:00 | 세션의 시작 시간입니다. |
| `sessiontime.endTime` | 문자열 | 2023-03-22 10:00:00 | 세션의 종료 시간입니다. |
| `sessiontime.room` | 문자열 | B32 | 세션에 사용되는 룸입니다. |

{style="table-layout:auto"}

에 대한 스키마를 생성하려면 [!DNL RainFocus] API 또는 UI를 사용하여 스키마를 만드는 방법에 대한 단계는 다음 설명서를 참조하십시오.

* [UI를 사용하여 스키마 만들기](../../../xdm/tutorials/create-schema-ui.md)
* [API를 사용하여 스키마 만들기](../../../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>* 스키마가 를 확장해야 함 **XDM ExperienceEvent 클래스.**
>* 스키마에 가 포함되어 있는지 확인해야 합니다. **기본 ID**, 및 **프로필에 대해 활성화됨**. 자세한 내용은 의 안내서를 참조하십시오. [ui에서 id 필드 정의](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/fields/identity.html)
>* sha256 이메일 또는 ECID와 같은 다른 적절한 식별자로 예제 ID(이메일)를 대체할 수 있습니다.

### RainFocus에서 통합 프로필 만들기 {#create-an-integration-profile-in-rainfocus}

서비스 계정 및 XDM 스키마가 준비되면 이제 를 활성화할 수 있습니다. [!DNL Integration Profile] 다음을 통해 [!DNL RainFocus] 플랫폼. 다음 [!DNL Integration Profile] 은(는) Experience Platform으로 데이터 스트리밍을 담당합니다.

에 로그인합니다 [[!DNL RainFocus] platform](https://app.rainfocus.com). 기본 탐색에서 을 선택합니다. **[!DNL Libraries]** 다음을 선택합니다. **[!DNL Integration Profiles]**

![라이브러리 및 통합 프로필이 선택된 RainFocus UI](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile.png)

새 프로필을 만들려면 **(`+`)** 아이콘. 그런 다음 을 선택합니다. **Adobe Real-time Customer Data Platform** 다음을 선택합니다. **확인**.

![RainFocus UI의 통합 프로필 만들기 창.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-select.png)

그런 다음 Adobe Developer 포털 프로젝트에서 검색한 자격 증명을 제공합니다.

* **클라이언트 ID**
* **클라이언트 암호**
* **기술 계정 ID**
* **조직 ID**

자격 증명이 제공되면 을(를) 선택합니다. **[!DNL Save]**.이제 새 항목이 표시됩니다 [!DNL Integration Profile] 다음에 나열됨: [!DNL RainFocus] 대시보드입니다.

다음 항목 선택 [!DNL Integration Profile] 미리 정의된 목록을 보기 위해 방금 만든 **푸시 유형** 이미 구성되었습니다. 다음 항목이 [경험 이벤트](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/experienceevent.html) 발생할 때 Experience Platform으로 전송됩니다.

![RainFocus 대시보드에 사전 정의된 푸시 유형 목록입니다.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-setup.png)

샘플 JSON 페이로드의 사본을 검색하려면 다음을 선택합니다. **[!DNL Sample JSON Payload]**. 그런 다음 샘플 JSON 페이로드를 강조 표시하고 복사합니다. **확장명이 .json인 새 파일에 저장합니다.**. 이 값은 나중에 의 Experience Platform에서 사용됩니다. [매핑 구성](../../tutorials/ui/create/analytics/rainfocus.md#mapping).

![RainFocus 대시보드의 샘플 JSON 페이로드.](/help/sources/images/tutorials/create/rainfocus/rainfocus_integration-profile-json.png)

>[!TIP]
>
>**설정이 아직 완료되지 않았습니다.**: 데이터 흐름이 만들어지면 다음으로 돌아와야 합니다. [!DNL RainFocus] 을(를) 완료하는 대시보드 [!DNL Integration Profile] 을(를) 제공하여 **스트리밍 끝점 URL** 및 **데이터 흐름 ID**.

## 다음 단계

이 문서를 읽으면 의 데이터를 스트리밍하는 데 필요한 사전 요구 사항 설정을 완료한 것입니다. [!DNL RainFocus] Experience Platform 계정. 이제 의 안내서로 진행할 수 있습니다. [연결 중 [!DNL RainFocus] 사용자 인터페이스를 사용하여 Experience Platform](../../tutorials/ui/create/analytics/rainfocus.md).