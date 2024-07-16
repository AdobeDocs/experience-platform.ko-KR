---
title: Mailchimp 관심 범주
description: Mailchimp(Intuit Mailchimp라고도 함)는 기업이 메일링 목록 및 이메일 마케팅 캠페인을 사용하여 연락처(고객, 고객 또는 기타 이해 당사자)를 관리하고 상담하는 데 사용하는 인기 있는 마케팅 자동화 플랫폼 및 이메일 마케팅 서비스입니다. 이 커넥터를 사용하여 관심사 및 선호도에 따라 연락처를 정렬합니다.
last-substantial-update: 2023-05-24T00:00:00Z
exl-id: bdce8295-7305-4d54-81c1-7fa3e580ce70
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '2299'
ht-degree: 2%

---

# [!DNL Mailchimp Interest Categories] 연결

[[!DNL Mailchimp]](https://mailchimp.com)은(는) 메일 목록 및 이메일 마케팅 캠페인을 사용하여 *(고객, 고객 또는 기타 이해 당사자)*&#x200B;을(를) 관리하고 연락하는 데 기업에서 사용하는 인기 있는 마케팅 자동화 플랫폼 및 이메일 마케팅 서비스입니다. 이 커넥터를 사용하여 관심사 및 선호도에 따라 연락처를 정렬합니다.

[!DNL Mailchimp Interest Categories]이(가) [대상](https://mailchimp.com/help/getting-started-audience/), [그룹](https://mailchimp.com/help/getting-started-with-groups/) 및 관심 범주 *(그룹 이름 또는 그룹 제목이라고도 함)*&#x200B;을(를) 사용합니다. 각 [!DNL Mailchimp] 그룹은 관심 범주 목록입니다. 연락처는 웹 사이트의 등록 양식을 통해 하나 이상의 관심 범주를 구독할 때 관심 범주와 연결됩니다. 또한 대상자 내에서 연락처를 그룹으로 구성하고 관심 카테고리와 연결할 수 있으며, 세그먼트를 만드는 데 이 연락처를 사용할 수 있습니다. 이러한 대상을 사용하여 타겟팅된 캠페인 이메일을 구독한 연락처에 브로드캐스트할 수 있습니다.

<!--
Compared to [!DNL Mailchimp Tags] which you would use for internal classification, [!DNL Mailchimp Interest Categories] is meant to manage subscriptions to topics of interest that your contacts might be interested in. *Note, Experience Platform also has a connection for [!DNL Mailchimp Tags], you can check it out on the [[!DNL Mailchimp Tags]](/help/destinations/catalog/email-marketing/mailchimp-tags.md) page.*
-->

이 [!DNL Adobe Experience Platform] [대상](/help/destinations/home.md)은(는) [[!DNL Mailchimp batch subscribe or unsubscribe API]](https://mailchimp.com/developer/marketing/api/lists/batch-subscribe-or-unsubscribe/) API를 사용하여 [관심 범주](https://mailchimp.com/developer/marketing/api/interest-categories/)을(를) 만든 다음 선택한 각 Platform 대상의 연락처를 해당 관심 범주에 추가합니다. 새 세그먼트 내에서 새 연락처를 활성화한 후 **새 연락처를 추가**&#x200B;하거나 **기존 [!DNL Mailchimp]개 연락처의 정보를 업데이트**&#x200B;한 다음 **원하는 그룹에서 추가 또는 제거**&#x200B;할 수 있습니다. [!DNL Mailchimp] [!DNL Mailchimp Interest Groups]은(는) 플랫폼에서 선택한 대상 이름을 [!DNL Mailchimp] 내의 관심 범주로 사용합니다.

## 사용 사례 {#use-cases}

[!DNL Mailchimp Interest Categories] 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례를 소개합니다.

### 마케팅 캠페인을 위해 연락처에 이메일 보내기 {#use-case-send-emails}

스포츠 용품 웹사이트의 판매부는 축구에 관심이 있다고 스스로 확인한 연락처 목록에 이메일 기반의 마케팅 캠페인을 방송하기를 원한다. 연락처 목록은 웹 사이트의 개발 팀으로부터 받은 데이터 내보내기의 배치로 분리되므로 추적해야 합니다. 팀은 기존 [!DNL Mailchimp]명의 대상을 식별하고 각 목록의 연락처가 추가되는 Experience Platform 대상을 빌드하기 시작합니다. 이 대상자를 [!DNL Mailchimp Interest Categories]에게 보낸 후 선택한 [!DNL Mailchimp] 대상자에 연락처가 없으면 해당 연락처가 속한 대상 이름을 가진 그룹에 추가됩니다. [!DNL Mailchimp] 대상자 또는 그룹에 이미 있는 연락처는 해당 정보가 업데이트됩니다. 데이터를 [!DNL Mailchimp Interest Categories]에게 보내면 영업 팀이 마케팅 캠페인 이메일을 선택하여 [!DNL Mailchimp] 대상자 내의 축구 관심 그룹에 보낼 수 있습니다.

## 전제 조건 {#prerequisites}

Experience Platform 및 [!DNL Mailchimp]에서 설정해야 하는 필수 구성 요소와 [!DNL Mailchimp Interest Categories] 대상으로 작업하기 전에 수집해야 하는 정보는 아래 섹션을 참조하십시오.

### Experience Platform의 사전 요구 사항 {#prerequisites-in-experience-platform}

[!DNL Mailchimp Interest Categories] 대상에 대한 데이터를 활성화하기 전에 [!DNL Experience Platform]에서 만든 [스키마](/help/xdm/schema/composition.md), [데이터 세트](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) 및 [세그먼트](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)가 있어야 합니다.

### [!DNL Mailchimp Interest Categories] 대상에 대한 필수 구성 요소 {#prerequisites-destination}

Platform에서 [!DNL Mailchimp] 계정으로 데이터를 내보내려면 다음 전제 조건을 참고하십시오.

#### [!DNL Mailchimp] 계정이 있어야 합니다. {#prerequisites-account}

[!DNL Mailchimp Interest Categories] 대상을 만들려면 먼저 [!DNL Mailchimp] 계정이 있는지 확인해야 합니다. 아직 계정이 없는 경우 [[!DNL Mailchimp] 등록 페이지](https://login.mailchimp.com/signup/)를 방문하여 계정을 등록하고 만드십시오.

#### [!DNL Mailchimp] API 키 수집 {#gather-credentials}

[!DNL Mailchimp] 계정에 대해 [!DNL Mailchimp Interest Categories] 대상을 인증하려면 [!DNL Mailchimp] **API 키**&#x200B;가 필요합니다. [대상을 인증](#authenticate)할 때 **API 키**&#x200B;이(가) **암호** 역할을 합니다.

**API 키**&#x200B;가 없는 경우 계정에 로그인하고 [[!DNL Mailchimp] API 키 생성](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key) 설명서를 참조하여 만드십시오.

API 키의 예는 `0123456789abcdef0123456789abcde-us14`입니다.

>[!IMPORTANT]
>
>**API 키**&#x200B;를 생성하는 경우 생성 후에는 액세스할 수 없으므로 기록하십시오.

#### [!DNL Mailchimp] 데이터 센터 식별 {#identify-data-center}

다음으로 [!DNL Mailchimp] 데이터 센터를 식별해야 합니다. 이렇게 하려면 [!DNL Mailchimp] 계정에 로그인하고 계정의 **API 키 섹션**(으)로 이동합니다.

값은 브라우저에 표시되는 URL의 첫 번째 부분입니다. URL이 *https://`us14`.mailchimp.com/account/api/*&#x200B;인 경우 데이터 센터는 `us14`입니다.

*key-dc* 형식의 API 키에도 추가됩니다. API 키가 `0123456789abcdef0123456789abcde-us14`이면 데이터 센터는 `us14`입니다.

데이터 센터 값 *(`us14` 이 예제에서는*)을(를) 기록하십시오. [대상 세부 정보를 채우기](#destination-details)할 때 이 값이 필요합니다.

추가 지침이 필요한 경우 [[!DNL Mailchimp] 기본 사항 설명서](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-structure)를 참조하세요.

### 가드레일 {#guardrails}

각 [!DNL Mailchimp] 대상에는 단일 그룹 또는 동일한 대상자 내의 여러 그룹에 최대 60개의 그룹 이름(또는 관심 범주)이 포함될 수 있습니다. 필요한 설명이 필요하면 [!DNL Mailchimp] [그룹](https://mailchimp.com/help/getting-started-with-groups/)을(를) 참조하십시오. 이 제한에 도달하면 [!DNL Mailchimp] API에서 오류 응답으로 `400 BAD_REQUEST Cannot have more than 60 interests per list (Across all categories)` 메시지가 표시됩니다.

또한 [!DNL Mailchimp] API에 의해 적용되는 제한에 대한 자세한 내용은 [!DNL Mailchimp] [속도 제한](https://mailchimp.com/developer/marketing/docs/fundamentals/#api-limits)을(를) 참조하십시오.

## 지원되는 ID {#supported-identities}

[!DNL Mailchimp]은(는) 아래 표에 설명된 ID 활성화를 지원합니다. [ID](/help/identity-service/features/namespaces.md)에 대해 자세히 알아보세요.

| 대상 ID | 설명 | 고려 사항 |
|---|---|---|
| 이메일 | 연락처 이메일 주소 | 필수 |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | <ul><li>필드 매핑에 따라 원하는 스키마 필드 *(예: 이메일 주소, 전화 번호, 성)*&#x200B;과(와) 함께 세그먼트의 모든 멤버를 내보냅니다.</li><li> 플랫폼에서 선택한 각 대상에 대해 해당 [!DNL Mailchimp Interest Categories] 세그먼트 상태가 Platform의 대상 상태로 업데이트됩니다.</li></ul> |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필을 업데이트하면 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
>
>대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

**[!UICONTROL 대상]** > **[!UICONTROL 카탈로그]** 내에서 [!DNL Mailchimp Interest Categories]을(를) 검색합니다. 또는 **[!UICONTROL 이메일 마케팅]** 범주에서 찾을 수 있습니다.

### 대상으로 인증 {#authenticate}

대상에 인증하려면 아래의 필수 필드를 입력한 다음 **[!UICONTROL 대상에 연결]**&#x200B;을(를) 선택하십시오.

| 필드 | 설명 |
| --- | --- |
| **[!UICONTROL 사용자 이름]** | [!DNL Mailchimp Interest Categories] 사용자 이름입니다. |
| **[!UICONTROL 암호]** | [수집 [!DNL Mailchimp] 자격 증명](#gather-credentials) 섹션에서 기록한 [!DNL Mailchimp] **API 키**.<br> API 키는 `{KEY}-{DC}` 형식을 사용합니다. 여기서 `{KEY}` 부분은 [[!DNL Mailchimp] API 키](#gather-credentials) 섹션에 언급된 값을 참조하고 `{DC}` 부분은 [[!DNL Mailchimp] 데이터 센터](#identify-data-center)를 참조합니다. <br>`{KEY}` 부분 또는 전체 양식을 제공할 수 있습니다.<br> 예를 들어 API 키가 <br>*`0123456789abcdef0123456789abcde-us14`*,<br>인 경우&#x200B;*`0123456789abcdef0123456789abcde`*또는&#x200B;*`0123456789abcdef0123456789abcde-us14`*을(를) 값으로 제공할 수 있습니다. |

{style="table-layout:auto"}

인증 방법을 보여 주는 ![플랫폼 UI 스크린샷입니다.](../../assets/catalog/email-marketing/mailchimp-interest-categories/authenticate-destination.png)

제공된 세부 정보가 유효하면 UI에 녹색 확인 표시와 함께 **[!UICONTROL 연결됨]** 상태가 표시됩니다. 그런 다음 다음 다음 단계로 진행할 수 있습니다.

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

![대상 세부 정보를 표시하는 플랫폼 UI 스크린샷입니다.](../../assets/catalog/email-marketing/mailchimp-interest-categories/destination-details.png)

| 필드 | 설명 |
| --- | --- |
| **[!UICONTROL 이름]** | 나중에 이 대상을 인식할 수 있는 이름입니다. |
| **[!UICONTROL 설명]** | 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다. |
| **[!UICONTROL 데이터 센터]** | [!DNL Mailchimp] 계정 `data center`입니다. 자세한 내용은 [데이터 센터 식별 [!DNL Mailchimp] 섹션](#identify-data-center)을 참조하세요. |
| **[!UICONTROL 대상 이름(먼저 데이터 센터를 선택하십시오)]** | **[!UICONTROL 데이터 센터]**&#x200B;를 선택하면 이 드롭다운이 [!DNL Mailchimp] 계정의 대상 이름으로 자동으로 채워집니다. Platform의 데이터로 업데이트할 대상을 선택합니다. |
| **[!UICONTROL 관심 범주(먼저 데이터 센터와 대상 이름을 선택하십시오)]** | **[!UICONTROL 대상 이름]**&#x200B;을 선택하면 이 드롭다운이 [!DNL Mailchimp] 계정의 관심 그룹 범주 이름으로 자동으로 채워집니다. Platform의 데이터로 업데이트할 카테고리 이름을 선택합니다. |

{style="table-layout:auto"}

>[!TIP]
>
> **[!UICONTROL 암호]** 필드 또는 **[!UICONTROL 데이터 센터]** 값에 제공한 API 키가 올바르지 않은 경우 UI에 아래와 같이 [!DNL Mailchimp] API 오류 응답 *`No options are available. Please verify the values selected for the following dependent fields: dataCenter`*&#x200B;이(가) 표시됩니다. 이 경우 **[!UICONTROL 대상 이름(먼저 데이터 센터를 선택하십시오)]** 필드에서 값을 선택할 수 없습니다. 이 오류를 해결하려면 올바른 값을 입력하십시오.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 모두 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

이 대상으로 대상을 활성화하는 방법에 대한 지침은 [프로필 및 대상을 스트리밍 대상 내보내기 대상으로 활성화](/help/destinations/ui/activate-segment-streaming-destinations.md)를 참조하십시오.

### 매핑 고려 사항 및 예제 {#mapping-considerations-example}

대상 데이터를 Adobe Experience Platform에서 [!DNL Mailchimp Interest Categories] 대상으로 올바르게 보내려면 필드 매핑 단계를 거쳐야 합니다. 매핑은 Platform 계정의 XDM(Experience Data Model) 스키마 필드와 대상 대상의 해당 필드 간에 링크를 만드는 것으로 구성됩니다.

XDM 필드를 [!DNL Mailchimp Interest Categories] 대상 필드에 올바르게 매핑하려면 아래 단계를 따르십시오.

1. **[!UICONTROL 매핑]** 단계에서 **[!UICONTROL 새 매핑 추가]**&#x200B;를 선택합니다. 이제 새 매핑 행이 화면에 표시됩니다.
1. **[!UICONTROL 소스 필드 선택]** 창에서 **[!UICONTROL 특성 선택]** 범주를 선택하고 XDM 특성을 선택하거나 **[!UICONTROL ID 네임스페이스 선택]**&#x200B;을 선택하고 ID를 선택합니다.
1. **[!UICONTROL 대상 필드 선택]** 창에서 **[!UICONTROL ID 네임스페이스 선택]**&#x200B;을(를) 선택하고 ID를 선택하거나 **[!UICONTROL 특성 선택]** 범주를 선택하고 [!DNL Mailchimp] API에서 채워진 특성 목록에서 선택하십시오. *선택한 [!DNL Mailchimp] 대상에 추가한 모든 사용자 지정 특성을 대상 필드로 선택할 수도 있습니다.*

   XDM 프로필 스키마와 [!DNL Mailchimp Interest Categories] 간에 사용할 수 있는 매핑은 다음과 같습니다.
| Source 필드 | 대상 필드 | 메모 |
| — | — | — |
|`IdentityMap: Email`|`Identity: email`| 필수: 예 |
|`xdm: person.name.firstName`|`Attribute: FNAME`| |
|`xdm: person.name.lastName`|`Attribute: LNAME`| |
|`xdm: person.birthDayAndMonth`|`Attribute: BIRTHDAY`| |

   또한 `ADDRESS`은(는) [!DNL Mailchimp] 대상 내에서 `merge field`(으)로 알려진 특수 대상 필드입니다. [[!DNL Mailchimp] 설명서](https://mailchimp.com/developer/marketing/docs/merge-fields/)은(는) 필수 키를 `addr1`, `city`, `state` 및 `zip`(으)로 정의하며 선택적 키 `addr2` 및 `country`을(를) 정의합니다. 이러한 필드의 값은 문자열이어야 합니다. `ADDRESS` 필드 매핑이 있는 경우 대상이 `ADDRESS` 개체를 [!DNL Mailchimp] API에 전달하여 업데이트합니다. 매핑되지 않은 `ADDRESS` 필드의 기본값은 `NULL`입니다. 단, 기본값은 `US`입니다.

   `ADDRESS` 필드에 사용할 수 있는 매핑은 다음과 같습니다.

   | 소스 필드 | 대상 필드 |
   | --- | --- |
   | `xdm: workAddress.street1` | `Attribute: ADDRESS.addr1` |
   | `xdm: workAddress.street2` | `Attribute: ADDRESS.addr2` |
   | `xdm: workAddress.city` | `Attribute: ADDRESS.city` |
   | `xdm: workAddress.state` | `Attribute: ADDRESS.state` |
   | `xdm: workAddress.postalCode` | `Attribute: ADDRESS.zip` |
   | `xdm: workAddress.country` | `Attribute: ADDRESS.country` |

   예를 들어 연락처의 기존 주소 필드 `addr1`, `city`, `state` 및 `zip` 값으로 `country`의 값을 `132, My Street, Kingston`, `New York`, `New York` 및 `12401`(으)로 업데이트하려고 합니다. `country`을(를) 업데이트하려면 변경 내용이 *(있는 경우)*&#x200B;인 기존 값과 새 국가 값을 전달해야 합니다. 따라서 데이터 집합의 값은 `132, My Street, Kingston`, `New York`, `New York`, `12401` 및 `US`이어야 합니다. 다시 말하면 `country`만 전달하고 `addr1`, `city`, `state` 및 `zip`에 대한 값을 제공하지 않으면 `NULL`이(가) 덮어씁니다.

   완료된 매핑의 예가 아래에 나와 있습니다.
   ![필드 매핑을 보여 주는 플랫폼 UI 스크린샷 예입니다.](../../assets/catalog/email-marketing/mailchimp-interest-categories/mappings.png)

대상 연결에 대한 매핑을 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

## 데이터 내보내기 유효성 검사 {#exported-data}

대상을 올바르게 설정했는지 확인하려면 아래 단계를 수행하십시오.

* [[!DNL Mailchimp]](https://login.mailchimp.com/) 계정에 로그인합니다. 그런 다음 **[!DNL Audience]** 페이지로 이동합니다. 그런 다음 **[!DNL Manage Contacts]** 메뉴를 확장하고 **[!DNL Groups]**&#x200B;을(를) 선택합니다.

대상 그룹 페이지를 표시하는 ![Mailchimp UI 스크린샷입니다.](../../assets/catalog/email-marketing/mailchimp-interest-categories/audience-groups.png)

* 그룹을 선택하고 선택한 대상이 플랫폼에서 대상 이름을 가진 카테고리로 만들어졌는지 확인합니다. 이 카테고리의 뒤에는 자동으로 생성된 접미사가 올 수 있습니다.
   * 이 대상은 선택한 세그먼트의 이름을 사용하여 [[!DNL Mailchimp] 관심 항목 추가 API](https://mailchimp.com/developer/marketing/api/interest-categories/add-interest-category/)를 사용하여 관심 항목을 만듭니다. 새 대상을 만들고 동일한 대상을 다시 활성화하는 경우 [!DNL Mailchimp]에서 접미사를 추가하여 기존 세그먼트와 새 세그먼트를 구별합니다.
* 그룹에 이메일이 없는 연락처는 새로 만든 카테고리에 추가됩니다.
* 그룹 내에 이미 존재하는 연락처의 경우 속성 필드 데이터가 업데이트되고, 연락처는 새로 생성된 카테고리에 추가됩니다.

대상 그룹 범주를 표시하는 ![Mailchimp UI 스크린샷입니다.](../../assets/catalog/email-marketing/mailchimp-interest-categories/audience-groups-category.png)

## 데이터 사용 및 관리 {#data-usage-governance}

데이터를 처리할 때 모든 [!DNL Adobe Experience Platform] 대상이 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](/help/data-governance/home.md)를 참조하십시오.

## 오류 및 문제 해결 {#errors-and-troubleshooting}

### [!DNL Mailchimp] API 키 또는 데이터 센터 값이 잘못된 경우 오류가 발생했습니다. {#incorrect-credentials-error}

**[!UICONTROL 암호]** 필드 또는 **[!UICONTROL 데이터 센터]** 값에 제공한 API 키가 올바르지 않은 경우 UI에 아래와 같이 [!DNL Mailchimp] API 오류 응답 *`No options are available. Please verify the values selected for the following dependent fields: dataCenter`*&#x200B;이(가) 표시됩니다. 이 경우 **[!UICONTROL 대상 이름(먼저 데이터 센터를 선택하십시오)]** 필드에서 값을 선택할 수 없습니다.

![Mailchimp API 키 또는 데이터 센터 값이 잘못된 경우 오류를 표시하는 Platform UI 스크린샷입니다.](../../assets/catalog/email-marketing/mailchimp-interest-categories/error.png)

이 오류를 수정하고 다음 단계로 진행하려면 올바른 값을 제공해야 합니다. [ID [!DNL Mailchimp] 데이터 센터](#identify-data-center)를 참조하고
지침이 필요한 경우 [API 키 [!DNL Mailchimp] 섹션 수집](#gather-credentials)합니다.

### [!DNL Mailchimp] 그룹 이름 제한을 초과하는 경우 오류가 발생했습니다. {#group-name-limits-error}

대상을 만들 때 다음 오류 메시지가 표시될 수 있습니다. *`Cannot have more than 60 interests per list (Across all categories)`* 또는 *`400 BAD_REQUEST`*. 이 문제는 [보호 기능](#guardrails) 섹션에 설명된 대로 단일 그룹 또는 동일한 대상 제한 내에 있는 여러 그룹에서 60개의 그룹 이름(또는 관심 범주)을 초과할 때 발생합니다. 이 오류를 해결하려면 [!DNL Mailchimp]에서 그룹 이름 제한을 초과하지 않도록 하십시오.

### [!DNL Mailchimp] 상태 및 오류 코드

설명과 함께 상태 및 오류 코드의 전체 목록을 보려면 [[!DNL Mailchimp] 오류 페이지](https://mailchimp.com/developer/marketing/docs/errors/)를 참조하세요.

## 추가 리소스 {#additional-resources}

[!DNL Mailchimp] 설명서의 추가 유용한 정보는 다음과 같습니다.
* [시작하기 [!DNL Mailchimp]](https://mailchimp.com/help/getting-started-with-mailchimp/)
* [대상자 시작](https://mailchimp.com/help/getting-started-audience/)
* [대상자 만들기](https://mailchimp.com/help/create-audience/)
* [그룹 시작](https://mailchimp.com/help/getting-started-with-groups/)
* [새 대상 그룹 만들기](https://mailchimp.com/help/create-new-audience-group/)
* [관심 범주](https://mailchimp.com/developer/marketing/api/interest-categories/)
* [마케팅 API](https://mailchimp.com/developer/marketing/api/)
