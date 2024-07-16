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

[[!DNL LinkedIn Conversions API]](https://learn.microsoft.com/en-us/linkedin/marketing/integrations/ads-reporting/conversions-api)은(는) 광고주 서버의 마케팅 데이터와 [!DNL LinkedIn] 간에 직접 연결을 만드는 전환 추적 도구입니다. 이를 통해 광고주는 전환 위치에 관계없이 [!DNL LinkedIn] 마케팅 캠페인의 효과를 평가하고 이 정보를 활용하여 캠페인 최적화를 추진할 수 있습니다. [!DNL LinkedIn Conversions API] 확장을 사용하면 보다 완벽한 속성, 향상된 데이터 안정성 및 더 나은 최적화 전달을 통해 성능을 강화하고 작업당 비용을 절감할 수 있습니다.

## 전제 조건 {#prerequisites}

[!DNL LinkedIn Campaign Manager] 계정에 [전환 규칙을 만들기](https://www.linkedin.com/help/lms/answer/a1657171)해야 합니다. [!DNL Adobe]은(는) 대화 규칙 이름의 시작 부분에 &quot;CAPI&quot;를 포함하여 구성할 수 있는 다른 전환 규칙 유형과 구분하도록 설정할 것을 권장합니다.

### 암호 및 데이터 요소 만들기

새 [!DNL LinkedIn] [이벤트 전달 암호](../../../ui/event-forwarding/secrets.md)를 만들고 인증 멤버를 나타내는 고유한 이름을 제공합니다. 값을 안전하게 유지하면서 계정에 대한 연결을 인증하는 데 사용됩니다.

그런 다음 [!UICONTROL Core] 확장 및 [!UICONTROL Secret] 데이터 요소 형식을 사용하여 [데이터 요소를 만듭니다](../../../ui/managing-resources/data-elements.md#create-a-data-element). 방금 만든 `LinkedIn` 암호를 참조합니다.

## [!DNL LinkedIn] 확장 설치 및 구성 {#install}

확장을 설치하려면 [이벤트 전달 속성을 만들거나](../../../ui/event-forwarding/overview.md#properties) 편집할 기존 속성을 선택하십시오.

왼쪽 탐색에서 **[!UICONTROL 확장]**&#x200B;을 선택합니다. **[!UICONTROL 카탈로그]** 탭에서 **[!UICONTROL LinkedIn]** 확장을 선택한 다음 **[!UICONTROL 설치]**&#x200B;를 선택합니다.

![설치를 강조 표시하는 [!DNL LinkedIn] 확장 카드를 표시하는 확장 카탈로그입니다.](../../../images/extensions/server/linkedin/install-extension.png)

다음 화면에서는 `Access Token` 필드에 이전에 만든 데이터 요소 암호를 입력합니다. 데이터 요소 암호에 [!DNL LinkedIn] OAuth 2 토큰이 포함됩니다. 완료되면 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

![액세스 토큰] 필드와 [!UICONTROL 저장]이 강조 표시된 [!DNL LinkedIn] 확장 구성 페이지입니다.](../../../images/extensions/server/linkedin/configure-extension.png)[!UICONTROL 

## [!DNL Send Conversion] 규칙 만들기 {#tracking-rule}

모든 데이터 요소가 설정되면 이벤트가 [!DNL LinkedIn]에 전송되는 시기와 방법을 결정하는 이벤트 전달 규칙을 만들 수 있습니다.

이벤트 전달 속성에 새 이벤트 전달 [규칙](../../../ui/managing-resources/rules.md)을(를) 만듭니다. **[!UICONTROL 작업]**&#x200B;에서 새 작업을 추가하고 확장을 **[!UICONTROL LinkedIn]**(으)로 설정합니다. 그런 다음 **[!UICONTROL 작업 유형]**&#x200B;에 대해 **[!UICONTROL 전환 보내기]**&#x200B;를 선택합니다.

![이벤트 전달 규칙 작업 구성을 추가하는 데 필요한 필드가 강조 표시된 이벤트 전달 속성 규칙 보기입니다.](../../../images/extensions/server/linkedin/linkedin-event-action.png)

선택 후 이벤트를 추가로 구성하는 추가 컨트롤이 나타납니다. **[!UICONTROL 변경 내용 유지]**&#x200B;를 선택하여 규칙을 저장합니다.

**[!UICONTROL 사용자 데이터]**

| 입력 | 설명 |
| --- | --- |
| [!UICONTROL 이메일] | 전환 이벤트와 연계된 연락처의 이메일 주소. 제공된 값이 이미 SHA256 문자열인 경우가 아니면 이메일 값은 SHA256의 확장 코드에 의해 인코딩됩니다. |
| [!UICONTROL LinkedIn 자사 광고 추적 UUID] | 자사 쿠키 ID입니다. 광고주가 클릭 URL에 클릭 ID 매개 변수 `li_fat_id`을(를) 추가하는 자사 쿠키를 활성화하려면 [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/help/lms/answer/a423304/enable-first-party-cookies-on-a-linkedin-insight-tag)에서 향상된 전환 추적을 활성화해야 합니다. |
| [!UICONTROL 고객 정보 데이터] | 이 필드에는 메시지와 함께 전송될 추가 속성이 있는 JSON 오브젝트가 포함됩니다.<br><br>**[!UICONTROL 원본]** 옵션에서 JSON 개체를 제공된 텍스트 필드에 직접 붙여넣거나 데이터 요소 아이콘(![데이터 집합 아이콘](../../../images/extensions/server/aws/data-element-icon.png))을 선택하여 기존 데이터 요소 목록에서 데이터를 나타낼 수 있습니다.<br><br>UI 편집기를 통해 각 키-값 쌍을 수동으로 추가하려면 **[!UICONTROL JSON 키-값 쌍 편집기]** 옵션을 사용할 수도 있습니다. 각 값은 원시 입력으로 나타내거나 데이터 요소를 대신 선택할 수 있습니다. 허용되는 키 값은 `firstName`, `lastName`, `companyName`, `title` 및 `country`입니다. |

{style="table-layout:auto"}

![필드에 입력된 데이터 예제를 보여 주는 [!DNL User Data] 섹션입니다.](../../../images/extensions/server/linkedin/configure-extension-user-data.png)

**[!UICONTROL 전환 데이터]**

| 입력 | 설명 |
| --- | --- |
| [!UICONTROL 전환] | [LinkedIn 캠페인 관리자](https://www.linkedin.com/help/lms/answer/a1657171)에서 만든 전환 규칙의 ID입니다. 변환 규칙을 선택하여 ID를 가져온 다음, 브라우저 URL의 ID(예: `/campaignmanager/accounts/508111232/conversions/15588877`)를 `/conversions/<id>`(으)로 복사합니다. |
| [!UICONTROL 전환 시간] | 전환 이벤트가 발생한 각 타임스탬프(밀리초). <br><br> 참고: 원본에서 전환 타임스탬프를 초 단위로 기록하는 경우 끝에 000을 삽입하여 밀리초로 변환하십시오. |
| [!UICONTROL 통화] | ISO 형식의 통화 코드. |
| [!UICONTROL 금액] | 변환 값(소수점 문자열: &quot;100.05&quot;). |
| [!UICONTROL 이벤트 ID] | 광고주가 각 이벤트를 표시하기 위해 생성한 고유 ID. 선택적 필드이며 [중복 제거](https://learn.microsoft.com/en-us/linkedin/marketing/conversions/deduplication?view=li-lms-2024-02)에 사용됩니다. |

{style="table-layout:auto"}

![필드에 예제 데이터를 표시하는 [!DNL Conversion Data] 섹션입니다.](../../../images/extensions/server/linkedin/configure-extension-conversions-data.png)

**[!UICONTROL 구성 재정의]**

>참고
>
>[!UICONTROL 구성 재정의] 필드를 사용하면 사용자가 모든 규칙에서 다른 [!DNL LinkedIn] 액세스 토큰을 설정할 수 있으므로, 각 규칙은 다른 [!DNL LinkedIn] 광고 계정에 액세스할 수 있는 액세스 토큰을 사용할 수 있습니다.

| 입력 | 설명 |
| --- | --- |
| [!UICONTROL 액세스 토큰] | [!DNL LinkedIn] 액세스 토큰입니다. |

![필드에 입력된 데이터 예제를 보여 주는 [!DNL Configuration Overrides] 섹션입니다.](../../../images/extensions/server/linkedin/configure-extension-configuration-override.png)

## 다음 단계

이 안내서에서는 [!DNL LinkedIn Conversions API] 이벤트 전달 확장을 사용하여 [!DNL LinkedIn]에 데이터를 보내는 방법을 다룹니다. [!DNL Adobe Experience Platform]의 이벤트 전달 기능에 대한 자세한 내용은 [이벤트 전달 개요](../../../ui/event-forwarding/overview.md)를 참조하십시오.

Experience Platform 디버거 및 이벤트 전달 Adobe Experience Platform Debugger 도구를 사용하여 구현을 디버깅하는 방법에 대한 자세한 내용은 [모니터링 개요](../../../../debugger/home.md) 및 [이벤트 전달에서 활동 모니터링](../../../ui/event-forwarding/monitoring.md)을 참조하십시오.
