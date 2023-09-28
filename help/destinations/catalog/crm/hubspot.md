---
title: HubSpot 연결
description: HubSpot 대상을 사용하면 HubSpot 계정에서 연락처 레코드를 관리할 수 있습니다.
last-substantial-update: 2023-09-28T00:00:00Z
source-git-commit: 9a8668a81927f22b03fed424c8df346f589da544
workflow-type: tm+mt
source-wordcount: '1604'
ht-degree: 1%

---


# [!DNL HubSpot] 연결

[[!DNL HubSpot]](https://www.hubspot.com) 는 마케팅, 판매, 콘텐츠 관리 및 고객 서비스를 연결하는 데 필요한 모든 소프트웨어, 통합 및 리소스가 포함된 CRM 플랫폼입니다. 이를 통해 하나의 CRM 플랫폼에서 데이터, 팀 및 고객을 연결할 수 있습니다.

이 [!DNL Adobe Experience Platform] [대상](/help/destinations/home.md) 을 활용합니다. [[!DNL HubSpot] 연락처 API](https://developers.hubspot.com/docs/api/crm/contacts)을 클릭하여 연락처 업데이트 [!DNL HubSpot] 활성화 후 기존 Experience Platform 대상으로부터.

에 대한 인증 지침 [!DNL HubSpot] 인스턴스는 다음보다 아래에 있습니다. [대상에 인증](#authenticate) 섹션.

## 사용 사례 {#use-cases}

을(를) 사용하는 방법과 시기를 더 잘 이해할 수 있도록 [!DNL HubSpot] destination은 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례입니다.

[!DNL HubSpot] 연락처는 비즈니스와 상호 작용하는 개인에 대한 정보를 저장합니다. 내 팀에 있는 연락처 사용 [!DNL HubSpot] Experience Platform 대상자를 빌드합니다. 이 대상자를 (으)로 보낸 후 [!DNL HubSpot], 연락처의 정보가 업데이트되고, 각 연락처에는 연락처가 속한 대상을 나타내는 대상 이름으로서의 값이 있는 속성이 할당됩니다.

## 전제 조건 {#prerequisites}

Experience Platform 및 에서 설정해야 하는 사전 요구 사항에 대해서는 아래 섹션을 참조하십시오 [!DNL HubSpot] 및 를 사용하기 전에 수집해야 하는 정보의 경우 [!DNL HubSpot] 대상.

### Experience Platform 사전 요구 사항 {#prerequisites-in-experience-platform}

에 대한 데이터를 활성화하기 전에 [!DNL HubSpot] 대상, 다음 항목이 있어야 합니다. [스키마](/help/xdm/schema/composition.md), a [데이터 세트](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), 및 [대상](https://experienceleague.adobe.com/docs/platform-learn/tutorials/audiences/create-audiences.html?lang=en) 생성 위치 [!DNL Experience Platform].

다음에 대한 Experience Platform 설명서 참조: [대상자 멤버십 세부 정보 스키마 필드 그룹](/help/xdm/field-groups/profile/segmentation.md) 대상 상태에 대한 지침이 필요한 경우.

### 사전 요구 사항 [!DNL HubSpot] 대상 {#prerequisites-destination}

Platform에서 로 데이터를 내보내려면 다음 전제 조건을 참고하십시오. [!DNL HubSpot] 계정:

#### 다음 항목이 있어야 합니다. [!DNL HubSpot] account {#prerequisites-account}

Platform에서 로 데이터를 내보내려면 [!DNL Hubspot] 계정 보유가 필요합니다. [!DNL HubSpot] 계정입니다. 아직 없다면 다음을 방문하십시오. [HubSpot 계정 설정](https://knowledge.hubspot.com/get-started/set-up-your-account) 페이지를 만들고 지침에 따라 계정을 등록하고 만듭니다.

#### 다음을 수집합니다. [!DNL HubSpot] 비공개 앱 액세스 토큰 {#gather-credentials}

다음 항목이 필요합니다. [!DNL HubSpot] `Access token` 허용 [!DNL HubSpot] 을(를) 통해 API를 호출할 대상 [!DNL HubSpot] 내 비공개 앱 [!DNL HubSpot] 계정입니다. 다음 `Access token` 은(는) 다음 역할을 합니다. `Bearer token` 다음을 수행하는 경우 [대상 인증](#authenticate).

개인 앱이 없는 경우 다음 문서를 따르십시오. [에서 개인 앱 만들기 [!DNL HubSpot]](https://developers.hubspot.com/docs/api/private-apps).

>[!IMPORTANT]
>
> 비공개 앱에는 아래 범위를 할당해야 합니다.
> `crm.objects.contacts.write`, `crm.objects.contacts.read`
> `crm.schemas.contacts.write`, `crm.schemas.contacts.read`

| 자격 증명 | 설명 | 예 |
| --- | --- | --- |
| `Bearer token` | 다음 `Access token` / [!DNL HubSpot] 비공개 앱. <br>을(를) 가져오려면 [!DNL HubSpot] `Access token` 팔로우 [!DNL HubSpot] 에 대한 설명서 [앱의 액세스 토큰으로 API 호출 수행](https://developers.hubspot.com/docs/api/private-apps#make-api-calls-with-your-app-s-access-token). | `pat-na1-11223344-abcde-12345-9876-1234a1b23456` |

## 가드레일 {#guardrails}

[!DNL HubSpot] 비공개 앱의 적용 대상: [비율 제한](https://developers.hubspot.com/docs/api/usage-details). 비공개 앱에서 호출할 수 있는 호출 수는 다음을 기반으로 합니다. [!DNL HubSpot] 계정 구독 및 API 추가 기능을 구매했는지 여부. 또한 다음을 참조하십시오 [기타 제한](https://developers.hubspot.com/docs/api/usage-details#other-limits).

## 지원되는 ID {#supported-identities}

[!DNL HubSpot] 는 아래 표에 설명된 id 업데이트를 지원합니다. 자세히 알아보기 [id](/help/identity-service/namespaces.md).

| 대상 ID | 예 | 설명 | 고려 사항 |
|---|---|---|---|
| `email` | `test@test.com` | 연락처의 이메일 주소입니다. | 필수입니다 |

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 모든 대상에 대해 설명합니다.

이 대상은 Experience Platform을 통해 생성된 모든 대상의 활성화를 지원합니다 [세분화 서비스](../../../segmentation/home.md).

이 대상은 아래 표에 설명된 대상의 활성화도 지원합니다.

| 대상자 유형 | 설명 |
---------|----------|
| 사용자 정의 업로드 | 대상 [가져옴](../../../segmentation/ui/overview.md#import-audience) csv 파일에서 Experience Platform으로 변환했습니다. |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | <ul><li>원하는 스키마 필드와 함께 대상의 모든 구성원을 내보냅니다 *(예: 이메일 주소, 전화번호, 성)*&#x200B;를 입력합니다.</li><li> 또한 새 속성이에 만들어집니다. [!DNL HubSpot] 선택한 각 대상에 대해 대상 이름 및 해당 값을 사용하는 것은 플랫폼의 해당 대상 상태와 함께 사용됩니다.</li></ul> |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | <ul><li>스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
>
>대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

이 대상에 연결하려면 다음과같이 하십시오. [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

다음 범위 내 **[!UICONTROL 대상]** > **[!UICONTROL 카탈로그]** 검색 대상 [!DNL HubSpot]. 또는 아래에서 찾을 수 있습니다 **[!UICONTROL CRM]** 범주.

### 대상에 인증 {#authenticate}

아래의 필수 필드를 입력하십시오. 다음을 참조하십시오. [다음을 수집합니다. [!DNL HubSpot] 비공개 앱 액세스 토큰](#gather-credentials) 섹션에 자세히 설명되어 있습니다.
* **[!UICONTROL 전달자 토큰]**: 다음에 대한 액세스 토큰 [!DNL HubSpot] 비공개 앱.

대상에 인증하려면 다음을 선택합니다. **[!UICONTROL 대상에 연결]**.
![인증 방법을 보여 주는 플랫폼 UI 스크린샷입니다.](../../assets/catalog/crm/hubspot/authenticate-destination.png)

제공된 세부 정보가 유효한 경우 UI에 **[!UICONTROL 연결됨]** 녹색 확인 표시가 있는 상태. 그런 다음 다음 다음 단계로 진행할 수 있습니다.

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.
![대상 세부 사항을 보여주는 플랫폼 UI 스크린샷입니다.](../../assets/catalog/crm/hubspot/destination-details.png)

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 다음 안내서를 참조하십시오. [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보를 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.

## 이 대상에 대상자 활성화 {#activate}

>[!IMPORTANT]
>
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

읽기 [스트리밍 대상자 내보내기 대상으로 프로필 및 대상자 활성화](/help/destinations/ui/activate-segment-streaming-destinations.md) 이 대상에 대한 대상자 활성화에 대한 지침을 참조하십시오.

### 속성 및 ID 매핑 {#map}

대상 데이터를 Adobe Experience Platform에서 로 올바르게 보내려면 [!DNL HubSpot] 대상, 필드 매핑 단계를 거쳐야 합니다. 매핑은 Platform 계정의 XDM(Experience Data Model) 스키마 필드와 대상 대상의 해당 필드 간에 링크를 만드는 것으로 구성됩니다.

XDM 필드를 [!DNL HubSpot] 대상 필드에서 아래 단계를 수행합니다.

#### 매핑 `Email` 신원

다음 `Email` id는 이 대상의 필수 매핑입니다. 매핑하려면 아래 단계를 따르십시오.
1. 다음에서 **[!UICONTROL 매핑]** 단계, 선택 **[!UICONTROL 새 매핑 추가]**. 이제 새 매핑 행이 화면에 표시됩니다.
   ![새 매핑 추가 버튼이 강조 표시된 Platform UI 스크린샷](../../assets/catalog/crm/hubspot/mapping-add-new-mapping.png)
1. 다음에서 **[!UICONTROL 소스 필드 선택]** 창에서 다음을 선택합니다. **[!UICONTROL ID 네임스페이스 선택]** id를 선택합니다.
   ![ID로 매핑할 소스 속성으로 이메일을 선택하는 Platform UI 스크린샷입니다.](../../assets/catalog/crm/hubspot/mapping-select-source-identity.png)
1. 다음에서 **[!UICONTROL 대상 필드 선택]** 창에서 다음을 선택합니다. **[!UICONTROL 속성 선택]** 및 선택 `email`.
   ![ID로 매핑할 타겟 속성으로 이메일을 선택하는 Platform UI 스크린샷입니다.](../../assets/catalog/crm/hubspot/mapping-select-target-identity.png)

| 소스 필드 | 대상 필드 | 필수입니다 |
| --- | --- | --- |
| `IdentityMap: Email` | `Identity: email` | 예 |

다음은 ID 매핑의 예입니다.
![이메일 ID 매핑을 사용한 Platform UI 스크린샷 예입니다.](../../assets/catalog/crm/hubspot/mapping-identities.png)

#### 매핑 **선택 사항** 속성

XDM 프로필 스키마와 XDM 프로필 스키마 사이에 업데이트할 다른 속성을 추가하려면 [!DNL HubSpot] 계정 아래 단계를 반복합니다.
1. 다음에서 **[!UICONTROL 매핑]** 단계, 선택 **[!UICONTROL 새 매핑 추가]**. 이제 새 매핑 행이 화면에 표시됩니다.
   ![새 매핑 추가 버튼이 강조 표시된 Platform UI 스크린샷](../../assets/catalog/crm/hubspot/mapping-add-new-mapping.png)
1. 다음에서 **[!UICONTROL 소스 필드 선택]** 창에서 다음을 선택합니다. **[!UICONTROL 속성 선택]** 범주를 선택한 다음 XDM 속성을 선택합니다.
   ![소스 속성으로 이름 을 선택하는 플랫폼 UI 스크린샷입니다.](../../assets/catalog/crm/hubspot/mapping-select-source-attribute.png)
1. 다음에서 **[!UICONTROL 대상 필드 선택]** 창, 선택 **[!UICONTROL 속성 선택]** 범주별로 정렬되어 있고, [!DNL HubSpot] 계정입니다. 대상에서 다음을 사용합니다. [[!DNL HubSpot] 속성](https://developers.hubspot.com/docs/api/crm/properties) 이 정보를 검색하기 위한 API입니다. 모두 [!DNL HubSpot] [기본 속성](https://knowledge.hubspot.com/contacts/hubspots-default-contact-properties) 및 모든 사용자 지정 속성을 검색하여 대상 필드로 선택할 수 있습니다.
   ![대상 속성으로 이름 을 선택하는 플랫폼 UI 스크린샷입니다.](../../assets/catalog/crm/hubspot/mapping-select-target-attribute.png)

XDM 프로필 스키마와 간에 사용 가능한 몇 가지 매핑 [!DNL Hubspot] 아래를 참조하십시오.

| 소스 필드 | 대상 필드 |
| --- | --- |
| `xdm: person.name.firstName` | `Attribute: firstname` |
| `xdm: person.name.lastName` | `Attribute: lastname` |
| `xdm: workAddress.street1` | `Attribute: address` |
| `xdm: workAddress.city` | `Attribute: city` |
| `xdm: workAddress.country` | `Attribute: country` |

이러한 속성 매핑을 사용하는 예는 다음과 같습니다.
![속성 매핑이 포함된 Platform UI 스크린샷 예입니다.](../../assets/catalog/crm/hubspot/mapping-attributes.png)

대상 연결에 대한 매핑 제공을 마치면 을(를) 선택합니다 **[!UICONTROL 다음]**.

## 데이터 내보내기 유효성 검사 {#exported-data}

대상을 올바르게 설정했는지 확인하려면 아래 단계를 수행하십시오.

1. 에 로그인합니다 [!DNL HubSpot] 웹 사이트를 방문한 다음 **[!UICONTROL 연락처]** 대상자 상태를 확인할 페이지입니다. 이 목록은 대상 이름으로 만들어진 사용자 지정 속성에 대한 열을 표시하도록 구성할 수 있으며, 해당 값은 대상 상태입니다.
   ![대상자 이름 및 셀 대상자 상태를 보여 주는 열 헤더가 있는 연락처 페이지를 보여 주는 HubSpot UI 스크린샷](../../assets/catalog/crm/hubspot/contacts.png)

1. 또는 개인을 드릴다운할 수 있습니다 **[!UICONTROL 개인]** 대상 이름 및 대상 상태를 표시하는 속성을 페이지로 이동합니다.
   ![대상자 이름과 대상자 상태를 표시하는 사용자 지정 속성이 있는 연락처 페이지를 보여 주는 HubSpot UI 스크린샷입니다.](../../assets/catalog/crm/hubspot/contact.png)

## 데이터 사용 및 관리 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스 시행, 다음을 참조하십시오. [데이터 거버넌스 개요](/help/data-governance/home.md).

## 추가 리소스 {#additional-resources}

에서 제공하는 추가 유용한 정보 [!DNL HubSpot] 설명서는 아래에 있습니다.
* [HubSpot의 인증 방법](https://developers.hubspot.com/docs/api/intro-to-auth)
* [!DNL HubSpot] API 참조 [연락처](https://developers.hubspot.com/docs/api/crm/contacts) 및 [속성](https://developers.hubspot.com/docs/api/crm/properties) API.

### 변경 로그

이 섹션에서는 이 대상 커넥터에 대한 기능 및 중요 설명서 업데이트를 캡처합니다.

+++ 변경 로그 보기

| 릴리스 월 | 업데이트 유형 | 설명 |
|---|---|---|
| 2023년 9월 | 초기 릴리스 | 초기 대상 릴리스 및 설명서 게시. |

{style="table-layout:auto"}

+++