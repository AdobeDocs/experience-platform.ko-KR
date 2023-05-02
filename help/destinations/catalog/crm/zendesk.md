---
title: Zendesk 연결
description: Zendesk 대상을 사용하면 비즈니스 요구 사항에 맞게 Zendesk 내에서 계정 데이터를 내보내고 활성화할 수 있습니다.
last-substantial-update: 2023-03-14T00:00:00Z
source-git-commit: 55f1eafa68124b044d20f8f909f6238766076a7a
workflow-type: tm+mt
source-wordcount: '1471'
ht-degree: 1%

---

# [!DNL Zendesk] 연결

[[!DNL Zendesk]](https://www.zendesk.com) 는 고객 서비스 솔루션 및 영업 툴입니다.

이 [!DNL Adobe Experience Platform] [대상](/help/destinations/home.md) 활용 [[!DNL Zendesk] 연락처 API](https://developer.zendesk.com/api-reference/sales-crm/resources/contacts/)에 대해 **id 만들기 및 업데이트** 세그먼트 내에서 [!DNL Zendesk].

[!DNL Zendesk] 는 bearer 토큰을 인증 메커니즘으로 사용하여 와 통신합니다 [!DNL Zendesk] 연락처 API. 인증 지침 [!DNL Zendesk] 인스턴스는 아래에 있습니다. [대상에 인증](#authenticate) 섹션을 참조하십시오.

## 사용 사례 {#use-cases}

멀티채널 B2C 플랫폼의 고객 서비스 부서는 고객에게 개인화된 원활한 경험을 제공하고자 합니다. 부서는 고유한 오프라인 데이터에서 세그먼트를 작성하여 새 사용자 프로필을 만들거나 다른 상호 작용(예: 구매, 반환 등)에서 기존 프로필 정보를 업데이트할 수 있습니다. 세그먼트를 Adobe Experience Platform에서 로 보내기 [!DNL Zendesk]. 에 업데이트된 정보 있음 [!DNL Zendesk] 고객 서비스 에이전트가 고객의 최신 정보를 즉시 사용할 수 있도록 하여 응답 및 해결 시간을 단축합니다.

## 사전 요구 사항 {#prerequisites}

### Experience Platform 사전 요구 사항 {#prerequisites-in-experience-platform}

데이터를 로 활성화하기 전에 [!DNL Zendesk] 대상, [스키마](/help/xdm/schema/composition.md), [데이터 세트](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), 및 [세그먼트](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 에서 생성됨 [!DNL Experience Platform].

에 대한 Experience Platform 설명서를 참조하십시오. [세그먼트 멤버십 세부 정보 스키마 필드 그룹](/help/xdm/field-groups/profile/segmentation.md) 세그먼트 상태에 대한 지침이 필요한 경우.

### [!DNL Zendesk] 전제 조건 {#prerequisites-destination}

Platform에서 로 데이터를 내보내려면 [!DNL Zendesk] 계정이 있어야 합니다. [!DNL Zendesk] 계정이 필요합니다.

#### 수집 [!DNL Zendesk] 자격 증명 {#gather-credentials}

를 인증하기 전에 아래 항목을 참고하십시오 [!DNL Zendesk] 대상:

| 자격 증명 | 설명 | 예 |
| --- | --- | --- |
| `Bearer token` | 에서 생성한 액세스 토큰 [!DNL Zendesk] 계정이 필요합니다. <br> 설명서에 따라 다음을 수행합니다 [생성 [!DNL Zendesk] 액세스 토큰](https://developer.zendesk.com/documentation/sales-crm/first-call/#1-generate-an-access-token) 없는 경우 | `a0b1c2d3e4...v20w21x22y23z` |

## 가드레일 {#guardrails}

다음 [가격 및 비율 제한](https://developer.zendesk.com/api-reference/sales-crm/rate-limits/#pricing) 페이지 세부 사항 [!DNL Zendesk] 계정과 연결된 API 제한. 데이터와 페이로드가 이러한 제한 내에 있는지 확인해야 합니다.

## 지원되는 ID {#supported-identities}

[!DNL Zendesk] 은 아래 표에 설명된 id 업데이트를 지원합니다. 추가 정보 [id](/help/identity-service/namespaces.md).

| Target ID | 예 | 설명 | 필수입니다 |
|---|---|---|---|
| `email` | `test@test.com` | 연락처의 이메일 주소입니다. | 예 |

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | <ul><li>원하는 스키마 필드와 함께 세그먼트의 모든 구성원을 내보냅니다 *(예: 이메일 주소, 전화 번호, 성)*: 사용자 필드 매핑에 따라 다릅니다.</li><li> 의 각 세그먼트 상태 [!DNL Zendesk] 은(는) **[!UICONTROL 매핑 ID]** 다음 기간 동안 제공된 값 [세그먼트 예약](#schedule-segment-export-example) 단계.</li></ul> |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | <ul><li>스트리밍 대상은 &quot;항상 설정&quot; API 기반 연결입니다. 세그먼트 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터는 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
>
>대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로우에서 아래 두 섹션에 나열된 필드를 채웁니다.

내 **[!UICONTROL 대상]** > **[!UICONTROL 카탈로그]** 검색 대상 [!DNL Zendesk]. 또는 **[!UICONTROL CRM]** 카테고리.

### 대상에 인증 {#authenticate}

아래 필수 필드를 입력합니다. 자세한 내용은 [수집 [!DNL Zendesk] 자격 증명](#gather-credentials) 섹션을 참조하십시오.
* **[!UICONTROL 베어러 토큰]**: 에서 생성한 액세스 토큰 [!DNL Zendesk] 계정이 필요합니다.

대상을 인증하려면 **[!UICONTROL 대상에 연결]**.
![인증 방법을 보여주는 Platform UI 스크린샷입니다.](../../assets/catalog/crm/zendesk/authenticate-destination.png)

제공된 세부 정보가 유효한 경우 UI에 **[!UICONTROL 연결됨]** 녹색 확인 표시가 있는 상태 그런 다음 다음 다음 단계로 진행할 수 있습니다.

### 대상 세부 사항 채우기 {#destination-details}

대상에 대한 세부 사항을 구성하려면 아래 필수 및 선택적 필드를 입력합니다. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.
![대상 세부 사항을 보여주는 Platform UI 스크린샷.](../../assets/catalog/crm/zendesk/destination-details.png)

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식하는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상으로 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보 제공을 마치면 를 선택합니다 **[!UICONTROL 다음]**.

## 세그먼트를 이 대상에 활성화 {#activate}

>[!IMPORTANT]
>
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

읽기 [스트리밍 세그먼트 내보내기 대상으로 프로필 및 세그먼트를 활성화합니다](/help/destinations/ui/activate-segment-streaming-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

### 매핑 고려 사항 및 예 {#mapping-considerations-example}

대상 데이터를 Adobe Experience Platform에서 로 올바로 보내려면 [!DNL Zendesk] 대상, 필드 매핑 단계를 거쳐야 합니다. 매핑은 플랫폼 계정의 Experience Data Model(XDM) 스키마 필드와 대상 대상의 해당 상당 요소 간에 링크를 만드는 작업으로 이루어집니다.

에 지정된 속성 **[!UICONTROL Target 필드]** 이 속성은 요청 본문을 형성하므로 속성 매핑 테이블에 설명된 대로 이름을 정확히 지정해야 합니다.

에 지정된 속성 **[!UICONTROL 소스 필드]** 그러한 제한 사항을 따르지 마십시오. 필요에 따라 매핑할 수 있지만 데이터 형식이 올바르지 않은 경우 [!DNL Zendesk] 오류가 발생합니다.

XDM 필드를 [!DNL Zendesk] 대상 필드: 다음 단계를 수행합니다.

1. 에서 **[!UICONTROL 매핑]** 단계, 선택 **[!UICONTROL 새 매핑 추가]**. 화면에 새 매핑 행이 표시됩니다.
1. 에서 **[!UICONTROL 소스 필드 선택]** 창에서 **[!UICONTROL 속성 선택]** 카테고리를 선택하고 XDM 속성을 선택하거나 **[!UICONTROL ID 네임스페이스 선택]** id를 선택합니다.
1. 에서 **[!UICONTROL 대상 필드 선택]** 창에서 **[!UICONTROL ID 네임스페이스 선택]** 카테고리를 선택하고 대상 ID를 선택하거나 **[!UICONTROL 속성 선택]** 카테고리를 선택하고 지원되는 스키마 속성 중 하나를 선택합니다.
   * 다음 단계를 반복하여 다음 필수 매핑을 추가하고 XDM 프로필 스키마와 사용자 간에 업데이트할 다른 속성을 추가할 수도 있습니다 [!DNL Zendesk] 인스턴스: |원본 필드|Target 필드| 필수| |—|—|—| |`xdm: person.name.lastName`|`xdm: last_name`| 예 | |`IdentityMap: Email`|`Identity: email`| 예 | |`xdm: person.name.firstName`|`xdm: first_name`| |

   * 이러한 매핑을 사용하는 예는 다음과 같습니다.
      ![속성 매핑이 있는 Platform UI 스크린샷 예.](../../assets/catalog/crm/zendesk/mappings.png)

>[!IMPORTANT]
>
>다음 `Attribute: last_name` 및 `Identity: email` 대상 매핑은 이 대상에 대해 필수입니다. 이러한 매핑이 누락되면 다른 매핑은 무시되고 로 전송되지 않습니다 [!DNL Zendesk].

대상 연결에 대한 매핑 제공을 마치면 를 선택합니다 **[!UICONTROL 다음]**.

### 세그먼트 내보내기 예약 및 예제 {#schedule-segment-export-example}

에서 [[!UICONTROL 세그먼트 내보내기 예약]](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 활성화 작업 과정의 단계에서는 Platform 세그먼트를 의 사용자 지정 필드 속성에 수동으로 매핑해야 합니다 [!DNL Zendesk].

이렇게 하려면 각 세그먼트를 선택한 다음 해당 사용자 지정 필드 속성을 입력합니다. [!DNL Zendesk] 에서 **[!UICONTROL 매핑 ID]** 필드.

예는 다음과 같습니다.
![Platform UI 스크린샷 예 - 세그먼트 내보내기 예약](../../assets/catalog/crm/zendesk/schedule-segment-export.png)

## 데이터 내보내기의 유효성 검사 {#exported-data}

대상을 올바르게 설정했는지 확인하려면 아래 단계를 수행하십시오.

1. 선택 **[!UICONTROL 대상]** > **[!UICONTROL 찾아보기]** 대상 목록으로 이동합니다.
1. 다음으로 대상을 선택하고 로 전환합니다. **[!UICONTROL 활성화 데이터]** 탭을 클릭한 다음 세그먼트 이름을 선택합니다.
   ![대상 활성화 데이터를 보여주는 Platform UI 스크린샷 예입니다.](../../assets/catalog/crm/zendesk/destinations-activation-data.png)

1. 세그먼트 요약을 모니터링하고 프로필 수가 세그먼트 내의 카운트와 일치하는지 확인합니다.
   ![세그먼트를 보여주는 Platform UI 스크린샷 예.](../../assets/catalog/crm/zendesk/segment.png)

1. 에 로그인합니다. [!DNL Zendesk] 웹 사이트에서 **[!UICONTROL 연락처]** 페이지에서 세그먼트의 프로필이 추가되었는지 확인합니다. 이 목록은 세그먼트로 만든 추가 필드에 대한 열을 표시하도록 구성할 수 있습니다 **[!UICONTROL 매핑 ID]** 및 세그먼트 상태.
   ![세그먼트 이름으로 만든 추가 필드가 있는 연락처 페이지를 보여주는 Zendesk UI 스크린샷입니다.](../../assets/catalog/crm/zendesk/contacts.png)

1. 또는 개별 페이지로 드릴다운할 수 있습니다 **[!UICONTROL 개인]** 페이지를 확인하고 **[!UICONTROL 추가 필드]** 세그먼트 이름 및 세그먼트 상태를 표시하는 섹션.
   ![세그먼트 이름 및 세그먼트 상태를 표시하는 추가 필드 섹션이 있는 개인 페이지를 보여주는 Zendesk UI 스크린샷입니다.](../../assets/catalog/crm/zendesk/contact.png)

## 데이터 사용 및 거버넌스 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스를 적용하는 경우 다음을 참조하십시오. [데이터 거버넌스 개요](/help/data-governance/home.md).

## 추가 리소스 {#additional-resources}

유용한 추가 정보는 [!DNL Zendesk] 설명서는 아래와 같습니다.
* [첫 번째 호출 만들기](https://developer.zendesk.com/documentation/sales-crm/first-call/)
* [사용자 지정 필드](https://developer.zendesk.com/api-reference/sales-crm/requests/#custom-fields)

### 창로그

이 섹션에서는 이 대상 커넥터에 대한 기능 및 중요한 설명서 업데이트를 캡처합니다.

+++ 변경 로그 보기

| 릴리스 시기 | 업데이트 유형 | 설명 |
|---|---|---|
| 2023년 4월 | 설명서 업데이트 | <ul><li>Adobe는 [사용 사례](#use-cases) 고객이 이 대상을 사용할 수 있는 이점이 있는 경우를 보다 명확하게 보여주는 예입니다.</li> <li>Adobe는 [매핑](#mapping-considerations-example) 섹션에 올바른 필수 매핑을 반영했습니다. 다음 `Attribute: last_name` 및 `Identity: email` 대상 매핑은 이 대상에 대해 필수입니다. 이러한 매핑이 누락되면 다른 매핑은 무시되고 로 전송되지 않습니다 [!DNL Zendesk].</li> <li>Adobe는 [매핑](#mapping-considerations-example) 필수 및 선택적 매핑에 대한 명확한 예가 있는 섹션.</li></ul> |
| 2023년 3월 | 초기 릴리스 | 초기 대상 릴리스 및 설명서 게시. |

{style="table-layout:auto"}

+++