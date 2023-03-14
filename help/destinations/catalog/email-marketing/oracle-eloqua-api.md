---
title: (API) Oracle Eloqua 연결
description: (API) Oracle Eloqua 대상을 사용하면 계정 데이터를 내보내고 비즈니스 요구 사항에 맞게 Oracle Eloqua 내에서 활성화할 수 있습니다.
last-substantial-update: 2023-03-14T00:00:00Z
source-git-commit: 3197eddcf9fef2870589fdf9f09276a333f30cd1
workflow-type: tm+mt
source-wordcount: '1494'
ht-degree: 0%

---

# [!DNL (API) Oracle Eloqua] 연결

[[!DNL Oracle Eloqua]](https://www.oracle.com/cx/marketing/automation/) 을 통해 마케터는 캠페인을 계획 및 실행하면서 잠재 고객을 위한 개인화된 고객 경험을 제공할 수 있습니다. 통합된 리드 관리와 손쉬운 캠페인 생성을 통해 마케터는 구매자의 여정에서 적시에 적절한 대상자를 참여시킬 수 있도록 지원하고 이메일, 디스플레이 검색, 비디오 및 모바일을 비롯한 다양한 채널에서 대상자에게 도달하도록 우아하게 확장할 수 있습니다. 영업 팀은 더 많은 거래를 더 빠른 속도로 마감할 수 있으므로 실시간 통찰력을 통해 마케팅 ROI를 높일 수 있습니다.

이 [!DNL Adobe Experience Platform] [대상](/help/destinations/home.md) 을 활용합니다. [연락처 업데이트](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/op-api-rest-1.0-data-contact-id-put.html) 에서 작업 [!DNL Oracle Eloqua] 세그먼트 내의 ID를 로 업데이트할 수 있는 REST API [!DNL Oracle Eloqua].

[!DNL Oracle Eloqua] 사용 [기본 인증](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html) 을(를) 통해 [!DNL Oracle Eloqua] REST API. 에 대한 인증 지침 [!DNL Oracle Eloqua] 인스턴스는 다음보다 아래에 있습니다. [대상에 인증](#authenticate) 섹션.

## 사용 사례 {#use-cases}

마케터는 Adobe Experience Platform 프로필의 속성에 따라 개인화된 경험을 사용자에게 제공할 수 있습니다. 오프라인 데이터에서 세그먼트를 작성하고 이러한 세그먼트를 로 보낼 수 있습니다. [!DNL Oracle Eloqua]: Adobe Experience Platform에서 세그먼트 및 프로필이 업데이트되는 즉시 사용자의 피드에 표시합니다.

## 전제 조건 {#prerequisites}

### Experience Platform 사전 요구 사항 {#prerequisites-in-experience-platform}

에 대한 데이터를 활성화하기 전에 [!DNL Oracle Eloqua] 대상, 다음 항목이 있어야 합니다. [스키마](/help/xdm/schema/composition.md), a [데이터 세트](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), 및 [세그먼트](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 생성 위치 [!DNL Experience Platform].

다음에 대한 Experience Platform 설명서 참조: [세그먼트 멤버십 세부 정보 스키마 필드 그룹](/help/xdm/field-groups/profile/segmentation.md) 세그먼트 상태에 대한 지침이 필요한 경우.

### [!DNL Oracle Eloqua] 전제 조건 {#prerequisites-destination}

Platform에서 로 데이터를 내보내려면 [!DNL Oracle Eloqua] 계정 이(가) 있어야 함 [!DNL Oracle Eloqua] 계정입니다.

#### 수집 [!DNL Oracle Eloqua] 자격 증명 {#gather-credentials}

에 인증하기 전에 아래 항목을 적어 두십시오. [!DNL Oracle Eloqua] 대상:

| 자격 증명 | 설명 |
| --- | --- |
| `Username` | 의 사용자 이름 [!DNL Oracle Eloqua] 계정입니다. |
| `Password` | 의 암호 [!DNL Oracle Eloqua] 계정입니다. |

## 가드레일 {#guardrails}

>[!NOTE]
>
>* [!DNL Oracle Eloqua] 사용자 지정 연락처 필드는 다음 작업 중에 선택한 세그먼트의 이름을 사용하여 자동으로 만들어집니다. **[!UICONTROL 세그먼트 선택]** 단계.


* [!DNL Oracle Eloqua] 에는 최대 250개의 사용자 지정 연락처 필드 제한이 있습니다.
* 새 세그먼트를 내보내기 전에 Platform 세그먼트 수와 내의 기존 세그먼트 수를 확인해야 합니다 [!DNL Oracle Eloqua] 이 한도를 초과하지 마십시오.
* 이 한도를 초과하면 Experience Platform 시 오류가 발생합니다. 이유는 다음과 같습니다. [!DNL Oracle Eloqua] API가 요청의 유효성을 검사하지 못하고 -으로 응답합니다. *400: 유효성 검사 오류가 있습니다.* - 문제를 설명하는 오류 메시지.
* 위에서 지정한 제한에 도달한 경우 대상에서 기존 매핑을 제거하고 의 해당 사용자 지정 연락처 필드를 삭제해야 합니다 [!DNL Oracle Eloqua] 계정을 만든 후에 더 많은 세그먼트를 내보낼 수 있습니다.

* 다음을 참조하십시오. [Oracle Eloqua 연락처 필드 만들기](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-user/Help/ContactFields/Tasks/CreatingContactFields.htm) 추가 제한에 대한 자세한 내용은 페이지를 참조하십시오.

## 지원되는 ID {#supported-identities}

[!DNL Oracle Eloqua] 는 아래 표에 설명된 id 업데이트를 지원합니다. 자세히 알아보기 [id](/help/identity-service/namespaces.md).

| TARGET ID | 예 | 설명 | 필수입니다 |
|---|---|---|---|
| `EloquaId` | `111111` | 연락처에 대한 고유 식별자. | 예 |

## 대상에 연결 {#connect}

>[!IMPORTANT]
>
>대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

이 대상에 연결하려면 다음과같이 하십시오. [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

다음 범위 내 **[!UICONTROL 대상]** > **[!UICONTROL 카탈로그]** 검색 대상 [!DNL (API) Oracle Eloqua]. 또는 아래에서 찾을 수 있습니다 **[!UICONTROL 이메일 마케팅]** 범주.

### 대상에 인증 {#authenticate}

아래의 필수 필드를 입력하십시오. 다음을 참조하십시오. [수집 [!DNL Oracle Eloqua] 자격 증명](#gather-credentials) 섹션에 자세히 설명되어 있습니다.
* **[!UICONTROL 암호]**: 의 암호 [!DNL Oracle Eloqua] 계정입니다.
* **[!UICONTROL 사용자 이름]**: 의 사용자 이름 [!DNL Oracle Eloqua] 계정입니다.

대상에 인증하려면 다음을 선택합니다. **[!UICONTROL 대상에 연결]**.
![인증 방법을 보여 주는 플랫폼 UI 스크린샷입니다.](../../assets/catalog/email-marketing/oracle-eloqua-api/authenticate-destination.png)

제공된 세부 정보가 유효한 경우 UI에 **[!UICONTROL 연결됨]** 녹색 확인 표시가 있는 상태. 그런 다음 다음 다음 단계로 진행할 수 있습니다.

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.
![대상 세부 사항을 보여주는 플랫폼 UI 스크린샷입니다.](../../assets/catalog/email-marketing/oracle-eloqua-api/destination-details.png)

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 다음 안내서를 참조하십시오. [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보를 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.

## 이 대상에 대한 세그먼트 활성화 {#activate}

>[!IMPORTANT]
>
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

읽기 [프로필 및 세그먼트를 스트리밍 세그먼트 내보내기 대상으로 활성화](/help/destinations/ui/activate-segment-streaming-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침

### 매핑 고려 사항 및 예제 {#mapping-considerations-example}

대상 데이터를 Adobe Experience Platform에서 로 올바르게 보내려면 [!DNL Oracle Eloqua] 대상, 필드 매핑 단계를 거쳐야 합니다. 매핑은 Platform 계정의 XDM(Experience Data Model) 스키마 필드와 대상 대상의 해당 필드 간에 링크를 만드는 것으로 구성됩니다.

`EloquaID` ID에 해당하는 속성을 업데이트하는 데 필요합니다. 다음 `emailAddress` 또한 API가 없는 경우 아래에 표시된 대로 오류가 발생합니다.

```json
{
   "type":"ObjectValidationError",
   "container":{
      "type":"ObjectKey",
      "objectType":"Contact"
   },
   "property":"emailAddress",
   "requirement":{
      "type":"EmailAddressRequirement"
   },
   "value":"<null>"
}
```

에 지정된 속성 **[!UICONTROL Target 필드]** 이러한 속성은 요청 본문을 형성하므로 속성 매핑 테이블에 설명된 것과 정확히 동일하게 이름이 지정되어야 합니다.

에 지정된 속성 **[!UICONTROL 소스 필드]** 이러한 제한 사항을 따르지 마십시오. 필요에 따라 매핑할 수 있지만 로 푸시할 때 데이터 형식이 올바르지 않은 경우 [!DNL Oracle Eloqua] 그러면 오류가 발생합니다.

예를 들어 를 매핑할 수 있습니다 **[!UICONTROL 소스 필드]** id 네임스페이스 `contact key`, `ABC ID` 등 끝 **[!UICONTROL Target 필드]** : `EloquaID` 에서 허용하는 형식을 ID 값이 준수하는지 확인한 후 [!DNL Oracle Eloqua].

XDM 필드를 [!DNL Oracle Eloqua] 대상 필드에서 다음 단계를 수행합니다.

1. 다음에서 **[!UICONTROL 매핑]** 단계, 선택 **[!UICONTROL 새 매핑 추가]**. 화면에 새 매핑 행이 표시됩니다.
1. 다음에서 **[!UICONTROL 소스 필드 선택]** 창에서 다음을 선택합니다. **[!UICONTROL 속성 선택]** 범주를 선택한 다음 XDM 속성을 선택하거나 **[!UICONTROL ID 네임스페이스 선택]** id를 선택합니다.
1. 다음에서 **[!UICONTROL 대상 필드 선택]** 창에서 다음을 선택합니다. **[!UICONTROL ID 네임스페이스 선택]** id를 선택하거나 **[!UICONTROL 사용자 지정 속성 선택]** 범주를 선택한 다음 필요에 따라 속성을 선택합니다.
   * XDM 프로필 스키마와 프로필 간에 다음 매핑을 추가하려면 다음 단계를 반복합니다 [!DNL Oracle Eloqua] 인스턴스: |소스 필드|Target 필드| 필수| |—|—| |`xdm: personalEmail.address`|`Attribute: emailAddress`| 예 | |`IdentityMap: Eid`|`Identity: EloquaId`| 예 |

   * 이러한 매핑을 사용하는 예는 다음과 같습니다.
      ![속성 매핑이 포함된 Platform UI 스크린샷 예입니다.](../../assets/catalog/email-marketing/oracle-eloqua-api/mappings.png)

      >[!IMPORTANT]
      >
      >두 가지 모두 `emailAddress` 및 `EloquaId` 대상 속성 매핑은 필수입니다.

대상 연결에 대한 매핑 제공을 마치면 을(를) 선택합니다 **[!UICONTROL 다음]**.

>[!NOTE]
>
>연락처 필드 정보를 로 보낼 때 대상은 각 실행 시 선택한 세그먼트 이름에 고유 식별자를 자동으로 추가합니다. [!DNL Oracle Eloqua]. 이렇게 하면 세그먼트 이름에 해당하는 연락처 필드 이름이 겹치지 않습니다. 다음을 참조하십시오. [데이터 내보내기 유효성 검사](#exported-data) 섹션 스크린샷의 예 [!DNL Oracle Eloqua] 세그먼트 이름을 사용하여 생성된 사용자 지정 연락처 필드가 있는 연락처 세부 정보 페이지.

## 데이터 내보내기 유효성 검사 {#exported-data}

대상을 올바르게 설정했는지 확인하려면 아래 단계를 수행하십시오.

1. 선택 **[!UICONTROL 대상]** > **[!UICONTROL 찾아보기]** 대상 목록으로 이동합니다.
1. 그런 다음 대상을 선택하고 **[!UICONTROL 활성화 데이터]** 탭을 누른 다음 세그먼트 이름을 선택합니다.
   ![대상 활성화 데이터를 보여주는 Platform UI 스크린샷 예입니다.](../../assets/catalog/email-marketing/oracle-eloqua-api/destinations-activation-data.png)

1. 세그먼트 요약을 모니터링하고 프로필 수가 세그먼트 내의 수와 일치하는지 확인합니다.
   ![세그먼트를 보여주는 플랫폼 UI 스크린샷 예입니다.](../../assets/catalog/email-marketing/oracle-eloqua-api/segment.png)

1. 에 로그인합니다 [!DNL Oracle Eloqua] 웹 사이트를 방문한 다음 **[!UICONTROL 연락처 개요]** 세그먼트의 프로필이 추가되었는지 확인할 페이지입니다. 세그먼트 상태를 보려면 다음을 드릴다운하십시오. **[!UICONTROL 연락처 세부 정보]** 선택한 세그먼트 이름을 접두사로 사용하는 연락처 필드를 만들었는지 확인합니다.

![세그먼트 이름으로 생성된 사용자 지정 연락처 필드가 있는 연락처 세부 정보 페이지를 보여주는 oracle Eloqua UI 스크린샷입니다.](../../assets/catalog/email-marketing/oracle-eloqua-api/contact.png)

## 데이터 사용 및 관리 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스 시행, 다음을 참조하십시오. [데이터 거버넌스 개요](/help/data-governance/home.md).

## 오류 및 문제 해결 {#errors-and-troubleshooting}

대상을 만들 때 다음 오류 메시지 중 하나를 받을 수 있습니다. `400: There was a validation error` 또는 `400 BAD_REQUEST`. 이 문제는 다음에 설명된 대로 250개의 사용자 정의 연락처 필드 제한을 초과할 때 발생합니다. [보호 기능](#guardrails) 섹션. 이 오류를 수정하려면 의 사용자 정의 연락처 필드 제한을 초과하지 않도록 하십시오. [!DNL Oracle Eloqua].
![오류를 표시하는 플랫폼 UI 스크린샷입니다.](../../assets/catalog/email-marketing/oracle-eloqua-api/error.png)

다음을 참조하십시오. [[!DNL Oracle Eloqua] HTTP 상태 코드](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPStatusCodes.html) 및 [[!DNL Oracle Eloqua] 유효성 검사 오류](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/APIRequests_HTTPValidationErrors.html) 설명이 포함된 상태 및 오류 코드의 전체 목록을 보여 주는 페이지입니다.

## 추가 리소스 {#additional-resources}

에서 제공하는 추가 유용한 정보 [!DNL Oracle ELoqua] 설명서는 아래에 있습니다.
* [Oracle Eloqua 마케팅 자동화](https://docs.oracle.com/en/cloud/saas/marketing/eloqua.html)
* [oracle Eloqua Marketing Cloud 서비스를 위한 REST API](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/rest-endpoints.html)