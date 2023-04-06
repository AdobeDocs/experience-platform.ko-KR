---
title: (API) Oracle Eloqua 연결
description: (API) Oracle Eloqua 대상을 사용하면 비즈니스 요구 사항에 맞게 Oracle Eloqua 내에서 계정 데이터를 내보내고 활성화할 수 있습니다.
last-substantial-update: 2023-03-14T00:00:00Z
source-git-commit: e8aa09545c95595e98b4730188bd8a528ca299a9
workflow-type: tm+mt
source-wordcount: '1642'
ht-degree: 0%

---


# [!DNL (API) Oracle Eloqua] 연결

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) 은 마케터가 잠재 고객을 위해 개인화된 고객 경험을 제공하면서 캠페인을 계획 및 실행할 수 있도록 해줍니다. 통합된 리드 관리 및 쉬운 캠페인 만들기 기능을 통해 마케터는 구매자의 여정에서 적시에 올바른 대상을 참여시킬 수 있고 이메일, 디스플레이 검색, 비디오 및 모바일을 포함한 다양한 채널에서 대상에게 우아한 규모로 이동할 수 있습니다. 영업 팀은 더 많은 거래를 더 빠른 비율로 종결할 수 있으므로 실시간 통찰력을 통해 마케팅 ROI를 높일 수 있습니다.

이 [!DNL Adobe Experience Platform] [대상](/help/destinations/home.md) 활용 [연락처 업데이트](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-id-put.html) 작업 [!DNL Oracle Eloqua] REST API. **id 업데이트** 세그먼트 내에서 [!DNL Oracle Eloqua].

[!DNL Oracle Eloqua] 사용 [기본 인증](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html) 와 통신하다 [!DNL Oracle Eloqua] REST API. 인증 지침 [!DNL Oracle Eloqua] 인스턴스는 아래에 있습니다. [대상에 인증](#authenticate) 섹션을 참조하십시오.

## 사용 사례 {#use-cases}

온라인 플랫폼의 마케팅 부서에서 선별된 리드 대상으로 이메일 기반 마케팅 캠페인을 브로드캐스트하려고 합니다. 플랫폼의 마케팅 팀은 Adobe Experience Platform을 통해 기존 리드 정보를 업데이트하고, 오프라인 데이터에서 세그먼트를 작성하고, 이러한 세그먼트를 로 보낼 수 있습니다 [!DNL Oracle Eloqua]: 마케팅 캠페인 이메일을 전송하는 데 사용할 수 있습니다.

## 사전 요구 사항 {#prerequisites}

### Experience Platform 사전 요구 사항 {#prerequisites-in-experience-platform}

데이터를 로 활성화하기 전에 [!DNL Oracle Eloqua] 대상, [스키마](/help/xdm/schema/composition.md), [데이터 세트](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), 및 [세그먼트](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 에서 생성됨 [!DNL Experience Platform].

에 대한 Experience Platform 설명서를 참조하십시오. [세그먼트 멤버십 세부 정보 스키마 필드 그룹](/help/xdm/field-groups/profile/segmentation.md) 세그먼트 상태에 대한 지침이 필요한 경우.

### [!DNL Oracle Eloqua] 전제 조건 {#prerequisites-destination}

Platform에서 로 데이터를 내보내려면 [!DNL Oracle Eloqua] 계정이 있어야 합니다. [!DNL Oracle Eloqua] 계정이 필요합니다.

#### 수집 [!DNL Oracle Eloqua] 자격 증명 {#gather-credentials}

를 인증하기 전에 아래 항목을 참고하십시오 [!DNL Oracle Eloqua] 대상:

| 자격 증명 | 설명 |
| --- | --- |
| `Username` | 사용자 이름 [!DNL Oracle Eloqua] 계정이 필요합니다. |
| `Password` | 사용자의 암호 [!DNL Oracle Eloqua] 계정이 필요합니다. |

## 가드레일 {#guardrails}

>[!NOTE]
>
>* [!DNL Oracle Eloqua] 사용자 지정 연락처 필드는 **[!UICONTROL 세그먼트 선택]** 단계.


* [!DNL Oracle Eloqua] 에는 사용자 지정 연락처 필드가 최대 250개로 제한됩니다.
* 새 세그먼트를 내보내기 전에 Platform 세그먼트 수와 내에 있는 기존 세그먼트 수를 확인하십시오 [!DNL Oracle Eloqua] 이 제한을 초과하지 마십시오.
* 이 제한을 초과하는 경우 Experience Platform 오류가 발생합니다. 이것은 [!DNL Oracle Eloqua] API가 요청의 유효성을 검사하지 못하며, -에 응답합니다. *400: 유효성 검사 오류가 발생했습니다.* - 문제를 설명하는 오류 메시지.
* 위에 지정된 제한에 도달한 경우 대상에서 기존 매핑을 제거하고 대상에서 해당 사용자 지정 연락처 필드를 삭제해야 합니다 [!DNL Oracle Eloqua] 더 많은 세그먼트를 내보내기 전에 계정을 사용하십시오.

* 자세한 내용은 [[!DNL Oracle Eloqua] 연락처 필드 만들기](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/ContactFields/Tasks/CreatingContactFields.htm) 추가 제한에 대한 자세한 내용은 페이지를 참조하십시오.

## 지원되는 ID {#supported-identities}

[!DNL Oracle Eloqua] 은 아래 표에 설명된 id 업데이트를 지원합니다. 추가 정보 [id](/help/identity-service/namespaces.md).

| Target ID | 설명 | 필수입니다 |
|---|---|---|
| `EloquaId` | 연락처의 고유 식별자입니다. | 예 |

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | <ul><li>원하는 스키마 필드와 함께 세그먼트의 모든 구성원을 내보냅니다 *(예: 이메일 주소, 전화 번호, 성)*: 사용자 필드 매핑에 따라 다릅니다.</li><li> Platform에서 선택한 각 세그먼트에 대해 해당 [!DNL Oracle Eloqua] 세그먼트 상태는 Platform의 세그먼트 상태로 업데이트됩니다.</li></ul> |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | <ul><li>스트리밍 대상은 &quot;항상 설정&quot; API 기반 연결입니다. 세그먼트 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터는 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
>
>대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로우에서 아래 두 섹션에 나열된 필드를 채웁니다.

내 **[!UICONTROL 대상]** > **[!UICONTROL 카탈로그]** 검색 대상 [!DNL (API) Oracle Eloqua]. 또는 **[!UICONTROL 이메일 마케팅]** 카테고리.

### 대상에 인증 {#authenticate}

아래 필수 필드를 입력합니다. 자세한 내용은 [수집 [!DNL Oracle Eloqua] 자격 증명](#gather-credentials) 섹션을 참조하십시오.
* **[!UICONTROL 암호]**: 사용자의 암호 [!DNL Oracle Eloqua] 계정이 필요합니다.
* **[!UICONTROL 사용자 이름]**: 사용자 이름 [!DNL Oracle Eloqua] 계정이 필요합니다.

대상을 인증하려면 **[!UICONTROL 대상에 연결]**.
![인증 방법을 보여주는 Platform UI 스크린샷입니다.](../../assets/catalog/email-marketing/oracle-eloqua-api/authenticate-destination.png)

제공된 세부 정보가 유효한 경우 UI에 **[!UICONTROL 연결됨]** 녹색 확인 표시가 있는 상태 그런 다음 다음 다음 단계로 진행할 수 있습니다.

### 대상 세부 사항 채우기 {#destination-details}

대상에 대한 세부 사항을 구성하려면 아래 필수 및 선택적 필드를 입력합니다. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.
![대상 세부 사항을 보여주는 Platform UI 스크린샷.](../../assets/catalog/email-marketing/oracle-eloqua-api/destination-details.png)

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

대상 데이터를 Adobe Experience Platform에서 로 올바로 보내려면 [!DNL Oracle Eloqua] 대상, 필드 매핑 단계를 거쳐야 합니다. 매핑은 플랫폼 계정의 Experience Data Model(XDM) 스키마 필드와 대상 대상의 해당 상당 요소 간에 링크를 만드는 작업으로 이루어집니다.

XDM 필드를 [!DNL Oracle Eloqua] 대상 필드: 다음 단계를 수행합니다.

1. 에서 **[!UICONTROL 매핑]** 단계, 선택 **[!UICONTROL 새 매핑 추가]**. 화면에 새 매핑 행이 표시됩니다.
1. 에서 **[!UICONTROL 소스 필드 선택]** 창에서 **[!UICONTROL 속성 선택]** 카테고리를 선택하고 XDM 속성을 선택하거나 **[!UICONTROL ID 네임스페이스 선택]** id를 선택합니다.
1. 에서 **[!UICONTROL 대상 필드 선택]** 창, **[!UICONTROL ID 네임스페이스 선택]** ID를 선택하거나 **[!UICONTROL 사용자 지정 속성 선택]** 을 입력하고 **[!UICONTROL 속성 이름]** 필드. 제공하는 속성 이름은 의 기존 연락처 속성과 일치해야 합니다 [!DNL Oracle Eloqua]. 자세한 내용은 [[!DNL create a contact]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html) 에 사용할 수 있는 정확한 속성 이름 [!DNL Oracle Eloqua].
   * 다음 단계를 반복하여 XDM 프로필 스키마와 [!DNL Oracle Eloqua]: | 소스 필드 | Target 필드 | 필수 | |—|—|—| |`IdentityMap: Eid`|`Identity: EloquaId`| 예 | |`xdm: personalEmail.address`|`Attribute: emailAddress`| 예 | |`xdm: personName.firstName`|`Attribute: firstName`| | |`xdm: personName.lastName`|`Attribute: lastName`| | |`xdm: workAddress.street1`|`Attribute: address1`| | |`xdm: workAddress.street2`|`Attribute: address2`| | |`xdm: workAddress.street3`|`Attribute: address3`| | |`xdm: workAddress.postalCode`|`Attribute: postalCode`| | |`xdm: workAddress.country`|`Attribute: country`| | |`xdm: workAddress.city`|`Attribute: city`| |

   * 위의 매핑에 대한 예는 다음과 같습니다.
      ![속성 매핑이 있는 Platform UI 스크린샷 예.](../../assets/catalog/email-marketing/oracle-eloqua-api/mappings.png)

>[!IMPORTANT]
>
>* 에 지정된 속성 **[!UICONTROL Target 필드]** 는 [[!DNL Create a contact]](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-post.html) 이러한 특성이 요청 본문을 형성할 수 있습니다.
>* 에 지정된 속성 **[!UICONTROL 소스 필드]** 그러한 제한 사항을 따르지 마십시오. 필요에 따라 매핑할 수 있지만 데이터 형식이 올바르지 않은 경우 [!DNL Oracle Eloqua] 오류가 발생합니다. 예를 들어 **[!UICONTROL 소스 필드]** id 네임스페이스 `contact key`, `ABC ID` 등. to **[!UICONTROL Target 필드]** : `EloquaId` ID 값이 [!DNL Oracle Eloqua].
>* 다음 `EloquaID` 매핑은 id에 해당하는 속성을 업데이트하는 데 필수입니다.
>* 다음 `emailAddress` 매핑이 필요합니다. 없는 경우, API에 아래와 같이 오류가 발생합니다.
>
>```json
>{
>     "type":"ObjectValidationError",
>     "container":{
>           "type":"ObjectKey",
>           "objectType":"Contact"
>     },
>     "property":"emailAddress",
>     "requirement":{
>           "type":"EmailAddressRequirement"
>     },
>     "value":"<null>"
>}
>```

대상 연결에 대한 매핑 제공을 마치면 를 선택합니다 **[!UICONTROL 다음]**.

>[!NOTE]
>
>대상에 연락처 필드 정보를 보낼 때 각 실행에서 선택한 세그먼트 이름에 대한 고유 식별자가 자동으로 전달됩니다 [!DNL Oracle Eloqua]. 이렇게 하면 세그먼트 이름에 해당하는 연락처 필드 이름이 겹치지 않습니다. 자세한 내용은 [데이터 내보내기의 유효성 검사](#exported-data) 섹션 스크린샷 예제 [!DNL Oracle Eloqua] 세그먼트 이름을 사용하여 만든 사용자 지정 연락처 필드가 있는 연락처 세부 정보 페이지에 문의하십시오.

## 데이터 내보내기의 유효성 검사 {#exported-data}

대상을 올바르게 설정했는지 확인하려면 아래 단계를 수행하십시오.

1. 선택 **[!UICONTROL 대상]** > **[!UICONTROL 찾아보기]** 대상 목록으로 이동합니다.
1. 다음으로 대상을 선택하고 로 전환합니다. **[!UICONTROL 활성화 데이터]** 탭을 클릭한 다음 세그먼트 이름을 선택합니다.
   ![대상 활성화 데이터를 보여주는 Platform UI 스크린샷 예입니다.](../../assets/catalog/email-marketing/oracle-eloqua-api/destinations-activation-data.png)

1. 세그먼트 요약을 모니터링하고 프로필 수가 세그먼트 내의 카운트와 일치하는지 확인합니다.
   ![세그먼트를 보여주는 Platform UI 스크린샷 예.](../../assets/catalog/email-marketing/oracle-eloqua-api/segment.png)

1. 에 로그인합니다. [!DNL Oracle Eloqua] 웹 사이트에서 **[!UICONTROL 연락처 개요]** 페이지에서 세그먼트의 프로필이 추가되었는지 확인합니다. 세그먼트 상태를 보려면 **[!UICONTROL 연락처 세부 정보]** 페이지에서 선택한 세그먼트 이름을 접두사로 사용하는 연락처 필드를 만들었는지 확인합니다.

![Oracle 세그먼트 이름으로 만든 사용자 지정 연락처 필드가 있는 연락처 세부 정보 페이지를 보여주는 Eloqua UI 스크린샷입니다.](../../assets/catalog/email-marketing/oracle-eloqua-api/contact.png)

## 데이터 사용 및 거버넌스 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스를 적용하는 경우 다음을 참조하십시오. [데이터 거버넌스 개요](/help/data-governance/home.md).

## 오류 및 문제 해결 {#errors-and-troubleshooting}

대상을 만들 때 다음 오류 메시지 중 하나를 받을 수 있습니다. `400: There was a validation error` 또는 `400 BAD_REQUEST`. 다음에 설명된 대로 사용자 지정 연락처 필드 제한을 250개를 초과할 때 발생합니다 [가드 레일](#guardrails) 섹션을 참조하십시오. 이 오류를 해결하려면 의 사용자 지정 연락처 필드 제한을 초과하지 않는지 확인합니다. [!DNL Oracle Eloqua].
![오류를 보여주는 Platform UI 스크린샷입니다.](../../assets/catalog/email-marketing/oracle-eloqua-api/error.png)

자세한 내용은 [[!DNL Oracle Eloqua] HTTP 상태 코드](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPStatusCodes.html) 및 [[!DNL Oracle Eloqua] 유효성 검사 오류](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPValidationErrors.html) 설명이 있는 상태 및 오류 코드의 전체 목록에 대한 페이지입니다.

## 추가 리소스 {#additional-resources}

자세한 내용은 [!DNL Oracle Eloqua] 설명서:

* [Eloqua Marketing Automation oracle](https://docs.oracle.com/en/cloud/saas/marketing/eloqua.html)
* [oracle Eloqua Marketing Cloud 서비스를 위한 REST API](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/rest-endpoints.html)