---
title: Linkedin 전환 API 이벤트 전달 확장
description: 이 Adobe Experience Platform 이벤트 전달 확장을 사용하면 Linkedin 마케팅 캠페인의 성능을 측정할 수 있습니다.
last-substantial-update: 2023-10-25T00:00:00Z
exl-id: 411e7b77-081e-4139-ba34-04468e519ea5
source-git-commit: 0d6ade1a0b6c00a4f87395d476dd7e7915489ea5
workflow-type: tm+mt
source-wordcount: '790'
ht-degree: 1%

---

# [!DNL LinkedIn] 전환 API 확장 기능

[[!DNL LinkedIn Conversions API]](https://learn.microsoft.com/en-us/linkedin/marketing/integrations/ads-reporting/conversions-api) 는 광고주 서버의 마케팅 데이터와 광고 데이터 간에 직접 연결을 만드는 전환 추적 도구입니다. [!DNL LinkedIn]. 이를 통해 광고주는 광고의 효과를 평가할 수 있습니다 [!DNL LinkedIn] 전환 위치에 상관없이 마케팅 캠페인을 진행하고 이 정보를 활용하여 캠페인 최적화를 촉진합니다. 다음 [!DNL LinkedIn Conversions API] 확장은 보다 완벽한 속성, 향상된 데이터 안정성 및 더 나은 최적화 제공을 통해 성능을 강화하고 작업당 비용을 줄이는 데 도움이 될 수 있습니다.

## 전제 조건 {#prerequisites}

다음을 수행해야 합니다. [전환 규칙 만들기](https://www.linkedin.com/help/lms/answer/a1657171) (으)로 [!DNL LinkedIn Campaign Manager] 계정입니다. [!DNL Adobe] 는 대화 규칙 이름의 시작 부분에 &quot;CAPI&quot;를 포함하여 구성할 수 있는 다른 전환 규칙 유형과 구분하도록 권장합니다.

### 암호 및 데이터 요소 만들기

새로 만들기 [!DNL LinkedIn] [이벤트 전달 암호](../../../ui/event-forwarding/secrets.md) 인증 멤버를 나타내는 고유한 이름을 제공합니다. 값을 안전하게 유지하면서 계정에 대한 연결을 인증하는 데 사용됩니다.

다음, [데이터 요소 만들기](../../../ui/managing-resources/data-elements.md#create-a-data-element) 사용 [!UICONTROL 코어] 확장 및 a [!UICONTROL 암호] 참조할 데이터 요소 유형 `LinkedIn` 방금 생성한 암호.

## 설치 및 구성 [!DNL LinkedIn] 확장 {#install}

확장을 설치하려면 [이벤트 전달 속성 만들기](../../../ui/event-forwarding/overview.md#properties) 또는 편집할 기존 속성을 선택합니다.

선택 **[!UICONTROL 확장]** 왼쪽 탐색. 다음에서 **[!UICONTROL 카탈로그]** 탭에서 **[!UICONTROL LinkedIn]** 확장을 마우스로 가리킨 다음 **[!UICONTROL 설치]**.

![다음을 표시하는 확장 카탈로그 [!DNL LinkedIn] 확장 카드 강조 표시 설치.](../../../images/extensions/server/linkedin/install-extension.png)

다음 화면에서는 이전에 만든 데이터 요소 암호를 `Access Token` 필드. 데이터 요소 암호에 [!DNL LinkedIn] OAuth 2 토큰. 선택 **[!UICONTROL 저장]** 완료 시.

![다음 [!DNL LinkedIn] 확장 구성 페이지 [!UICONTROL 액세스 토큰] 필드 및 [!UICONTROL 저장] 강조 표시됨.](../../../images/extensions/server/linkedin/configure-extension.png)

## 만들기 [!DNL Send Conversion] 규칙 {#tracking-rule}

모든 데이터 요소가 설정되면 이벤트가 전송되는 시기와 방법을 결정하는 이벤트 전달 규칙 만들기를 시작할 수 있습니다 [!DNL LinkedIn].

새 이벤트 전달 만들기 [규칙](../../../ui/managing-resources/rules.md) 이벤트 전달 속성에서 다음을 수행합니다. 아래 **[!UICONTROL 작업]**, 새 작업을 추가하고 확장을 로 설정합니다. **[!UICONTROL LinkedIn]**. 그런 다음 을 선택합니다. **[!UICONTROL 변환 전송]** 대상: **[!UICONTROL 작업 유형]**.

![이벤트 전달 규칙 작업 구성을 추가하는 데 필요한 필드가 강조 표시된 이벤트 전달 속성 규칙 보기.](../../../images/extensions/server/linkedin/linkedin-event-action.png)

선택 후 이벤트를 추가로 구성하는 추가 컨트롤이 나타납니다. 선택 **[!UICONTROL 변경 내용 유지]** 을 눌러 규칙을 저장합니다.

**[!UICONTROL 사용자 데이터]**

| 입력 | 설명 |
| --- | --- |
| [!UICONTROL 이메일] | 전환 이벤트와 연계된 연락처의 이메일 주소. 제공된 값이 이미 SHA256 문자열인 경우가 아니면 이메일 값은 SHA256의 확장 코드에 의해 인코딩됩니다. |
| [!UICONTROL LinkedIn 자사 광고 추적 UUID] | 자사 쿠키 ID입니다. 광고주는에서 향상된 전환 추적을 활성화해야 합니다. [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/help/lms/answer/a423304/enable-first-party-cookies-on-a-linkedin-insight-tag) 클릭 ID 매개 변수를 추가하는 자사 쿠키를 활성화하려면 `li_fat_id` 을 클릭하여 URL을 검색합니다. |
| [!UICONTROL 고객 정보 데이터] | 이 필드에는 메시지와 함께 전송될 추가 속성이 있는 JSON 오브젝트가 포함됩니다.<br><br>아래 **[!UICONTROL Raw]** 옵션을 사용하면 JSON 개체를 제공된 텍스트 필드에 직접 붙여넣거나 데이터 요소 아이콘(![데이터 세트 아이콘](../../../images/extensions/server/aws/data-element-icon.png))를 클릭하여 기존 데이터 요소 목록에서 데이터를 나타낼 수 있습니다.<br><br>다음을 사용할 수도 있습니다 **[!UICONTROL JSON 키-값 쌍 편집기]** ui 편집기를 통해 각 키-값 쌍을 수동으로 추가하는 옵션. 각 값은 원시 입력으로 나타내거나 데이터 요소를 대신 선택할 수 있습니다. 허용되는 키 값은 다음과 같습니다. `firstName`, `lastName`, `companyName`, `title` 및 `country`. |

{style="table-layout:auto"}

![다음 [!DNL User Data] 필드로의 데이터 입력 예를 보여 주는 섹션입니다.](../../../images/extensions/server/linkedin/configure-extension-user-data.png)

**[!UICONTROL 전환 데이터]**

| 입력 | 설명 |
| --- | --- |
| [!UICONTROL 전환] | 에서 생성된 전환 규칙의 ID [LinkedIn 캠페인 관리자](https://www.linkedin.com/help/lms/answer/a1657171). 변환 규칙을 선택하여 ID를 가져온 다음 브라우저 URL에서 ID를 복사합니다(예: `/campaignmanager/accounts/508111232/conversions/15588877`) as `/conversions/<id>`. |
| [!UICONTROL 전환 시간] | 전환 이벤트가 발생한 각 타임스탬프(밀리초). <br><br> 참고: 소스에서 전환 타임스탬프를 초 단위로 기록하는 경우 끝에 000을 삽입하여 밀리초로 변환하십시오. |
| [!UICONTROL 통화] | ISO 형식의 통화 코드. |
| [!UICONTROL 금액] | 변환 값(소수점 문자열: &quot;100.05&quot;). |
| [!UICONTROL 이벤트 ID] | 광고주가 각 이벤트를 표시하기 위해 생성한 고유 ID. 이 필드는 선택 사항이며 다음에 사용됩니다. [중복 제거](https://learn.microsoft.com/en-us/linkedin/marketing/conversions/deduplication?view=li-lms-2024-02). |

{style="table-layout:auto"}

![다음 [!DNL Conversion Data] 필드의 예제 데이터를 보여 주는 섹션입니다.](../../../images/extensions/server/linkedin/configure-extension-conversions-data.png)

**[!UICONTROL 구성 재정의]**

>참고
>
>다음 [!UICONTROL 구성 재정의] 필드를 사용하면 사용자가 다른 항목을 설정할 수 있습니다 [!DNL LinkedIn] 모든 규칙의 액세스 토큰을 사용하여 각 규칙이 서로 다른 규칙에 액세스할 수 있는 액세스 토큰을 사용할 수 있습니다. [!DNL LinkedIn] 광고 계정입니다.

| 입력 | 설명 |
| --- | --- |
| [!UICONTROL 액세스 토큰] | 다음 [!DNL LinkedIn] 액세스 토큰입니다. |

![다음 [!DNL Configuration Overrides] 필드에 입력된 데이터 예제를 보여 주는 섹션입니다.](../../../images/extensions/server/linkedin/configure-extension-configuration-override.png)

## 다음 단계

이 안내서에서는 로 데이터를 보내는 방법을 다룹니다 [!DNL LinkedIn] 사용 [!DNL LinkedIn Conversions API] 이벤트 전달 확장. 의 이벤트 전달 기능에 대한 자세한 내용 [!DNL Adobe Experience Platform], 다음을 읽습니다 [이벤트 전달 개요](../../../ui/event-forwarding/overview.md).

Experience Platform 디버거 및 이벤트 전달 모니터링 도구를 사용하여 구현을 디버깅하는 방법에 대한 자세한 내용은 [Adobe Experience Platform Debugger 개요](../../../../debugger/home.md) 및 [이벤트 전달 시 활동 모니터링](../../../ui/event-forwarding/monitoring.md).
