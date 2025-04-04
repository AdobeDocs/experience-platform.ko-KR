---
keywords: crm;CRM;CRM 대상;Outreach;Outreach crm 대상
title: 지원 연결
description: 전달 대상을 사용하면 계정 데이터를 내보내고 비즈니스 요구 사항에 맞게 전달 내에서 활성화할 수 있습니다.
exl-id: 7433933d-7a4e-441d-8629-a09cb77d5220
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1698'
ht-degree: 2%

---

# [!DNL Outreach] 연결

## 개요 {#overview}

[[!DNL Outreach]](https://www.outreach.io/)은(는) 세계에서 가장 많은 B2B 구매자-판매자 상호 작용 데이터와 판매 데이터를 인텔리전스로 변환하기 위한 독점 AI 기술에 대한 상당한 투자가 있는 판매 실행 플랫폼입니다. [!DNL Outreach]을(를) 사용하면 조직의 효율성, 예측 가능성 및 성장을 향상시키기 위해 영업 참여를 자동화하고 매출 인텔리전스를 수행할 수 있습니다.

이 [!DNL Adobe Experience Platform] [대상](/help/destinations/home.md)은(는) [!DNL Outreach]의 잠재 고객에 해당하는 대상 내에서 ID를 업데이트할 수 있는 [Outreach Update Resource API](https://api.outreach.io/api/v2/docs#update-an-existing-resource)를 활용합니다.

[!DNL Outreach]은(는) 인증 메커니즘으로 권한 부여가 있는 OAuth 2를 사용하여 [!DNL Outreach] [!DNL Update Resource API]과(와) 통신합니다. [!DNL Outreach] 인스턴스에 대한 인증 지침은 [대상에 대한 인증](#authenticate) 섹션 아래에 나와 있습니다.

## 사용 사례 {#use-cases}

마케터는 Adobe Experience Platform 프로필의 속성에 따라 잠재 고객에게 개인화된 경험을 제공할 수 있습니다. Adobe Experience Platform에서 대상 및 프로필이 업데이트되는 즉시 잠재 고객의 피드에 표시하기 위해 오프라인 데이터에서 대상을 작성하고 이 대상을 [!DNL Outreach]&#x200B;(으)로 보낼 수 있습니다.

## 전제 조건 {#prerequisites}

### Experience Platform 사전 요구 사항 {#prerequisites-in-experience-platform}

[!DNL Outreach] 대상에 대한 데이터를 활성화하기 전에 [!DNL Experience Platform]에서 만든 [스키마](/help/xdm/schema/composition.md), [데이터 세트](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html) 및 [세그먼트](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html)가 있어야 합니다.

대상 상태에 대한 지침이 필요한 경우 [대상 멤버십 세부 정보 스키마 필드 그룹](/help/xdm/field-groups/profile/segmentation.md)에 대한 Adobe 설명서를 참조하십시오.

### 지원 전제 조건 {#prerequisites-destination}

Experience Platform에서 [!DNL Outreach] 계정으로 데이터를 내보내려면 [!DNL Outreach]의 다음 필수 구성 요소를 참고하십시오.

#### 봉사 계정이 있어야 합니다. {#prerequisites-account}

아직 계정이 없는 경우 [!DNL Outreach] [로그인](https://accounts.outreach.io/users/sign_in) 페이지로 이동하여 계정을 등록하고 만드십시오. 자세한 내용은 [!DNL Outreach] 지원 [페이지](https://support.outreach.io/hc/en-us/articles/207238607-Claim-Your-Outreach-Account)도 참조하세요.

[!DNL Outreach] CRM 대상에 인증하기 전에 아래 항목을 적어 두십시오.

| 자격 증명 | 설명 |
|---|---|
| 이메일 | [!DNL Outreach] 계정 전자 메일 |
| 암호 | [!DNL Outreach] 계정 암호 |

#### 사용자 정의 필드 레이블 설정 {#prerequisites-custom-fields}

[!DNL Outreach]은(는) [잠재 고객](https://support.outreach.io/hc/en-us/articles/360001557554-Outreach-Prospect-Profile-Overview)에 대한 사용자 지정 필드를 지원합니다. 자세한 지침은 [Outreach에서 사용자 지정 필드를 추가하는 방법](https://support.outreach.io/hc/en-us/articles/219124908-How-To-Add-a-Custom-Field-in-Outreach)을 참조하세요. 쉽게 식별할 수 있도록 레이블을 기본값을 유지하는 대신 해당 대상 이름으로 수동으로 업데이트하는 것이 좋습니다. 예를 들어 다음과 같습니다.

잠재 고객의 [!DNL Outreach] 설정 페이지에 사용자 지정 필드가 표시됩니다.
![설정 페이지의 사용자 지정 필드를 표시하는 Outreach UI 스크린샷입니다.](../../assets/catalog/crm/outreach/outreach-custom-fields.png)

*사용자에게 친숙한* 레이블이 대상 이름과 일치하는 사용자 지정 필드를 표시하는 잠재 고객의 [!DNL Outreach] 설정 페이지입니다. 잠재 고객 페이지에서 이러한 레이블에 대한 대상 상태를 볼 수 있습니다.
![설정 페이지에 연결된 레이블이 있는 사용자 지정 필드를 표시하는 Outreach UI 스크린샷입니다.](../../assets/catalog/crm/outreach/outreach-custom-field-labels.png)

>[!NOTE]
>
> 레이블 이름은 쉽게 식별할 수 있습니다. 이 변수는 잠재 고객 업데이트 시 사용되지 않습니다.

## 가드레일

[!DNL Outreach] API의 속도 제한은 사용자당 시간당 10,000개의 요청입니다. 이 한도에 도달하면 `You have exceeded your permitted rate limit of 10,000; please try again at 2017-01-01T00:00:00.` 메시지와 함께 `429` 응답을 받게 됩니다.

이 메시지를 받은 경우 비율 임계값을 준수하도록 대상 내보내기 일정을 업데이트해야 합니다.

자세한 내용은 [[!DNL Outreach] 설명서](https://api.outreach.io/api/v2/docs#rate-limiting)를 참조하세요.

## 지원되는 ID {#supported-identities}

[!DNL Outreach]은(는) 아래 표에 설명된 ID 업데이트를 지원합니다. [ID](/help/identity-service/features/namespaces.md)에 대해 자세히 알아보세요.

| 타겟 ID | 설명 | 고려 사항 |
|---|---|---|
| `OutreachId` | <ul><li>[!DNL Outreach] 식별자. Prospect Profile에 해당하는 숫자 값입니다.</li><li>ID는 업데이트할 잠재 고객의 [!DNL Outreach] URL 내 ID와 일치해야 합니다.</li><li>자세한 내용은 [[!DNL Outreach] 설명서](https://api.outreach.io/api/v2/docs#update-an-existing-resource)를 참조하세요.</li></ul> | 필수 |

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | <ul><li> 필드 매핑에 따라 원하는 스키마 필드 *(예: 이메일 주소, 전화 번호, 성)*&#x200B;과(와) 함께 세그먼트의 모든 멤버를 내보냅니다.</li><li> [대상 예약](#schedule-segment-export-example) 단계 동안 제공된 [!UICONTROL 매핑 ID] 값을 기반으로 [!DNL Outreach]의 각 세그먼트 상태가 Experience Platform의 해당 대상 상태로 업데이트됩니다.</li></ul> |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | <ul><li> 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요.</li></ul> |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
> 대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

**[!UICONTROL 대상]** > **[!UICONTROL 카탈로그]** 내에서 [!DNL Outreach] 검색 또는 CRM 범주 아래에서 찾을 수 있습니다.

### 대상으로 인증 {#authenticate}

대상에 인증하려면 **[!UICONTROL 대상에 연결]**&#x200B;을 선택하세요.

![Outreach 인증 방법을 보여 주는 Experience Platform UI 스크린샷입니다.](../../assets/catalog/crm/outreach/authenticate-destination.png)

[!DNL Outreach] 로그인 페이지가 표시됩니다. 이메일을 입력합니다.

![Outreach에 인증하기 위해 전자 메일을 입력하는 필드를 표시하는 Outreach UI 스크린샷입니다.](../../assets/catalog/crm/outreach/authenticate-destination-login-email.png)

그런 다음 암호를 입력합니다.

![Outreach에 인증하기 위해 암호 단계를 입력하는 필드를 표시하는 Outreach UI 스크린샷입니다.](../../assets/catalog/crm/outreach/authenticate-destination-login-password.png)

* **[!UICONTROL 사용자 이름]**: [!DNL Outreach] 계정 전자 메일입니다.
* **[!UICONTROL 암호]**: [!DNL Outreach] 계정 암호입니다.

제공된 세부 정보가 유효하면 UI에 녹색 확인 표시와 함께 **연결됨** 상태가 표시됩니다. 그런 다음 다음 다음 단계로 진행할 수 있습니다.

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.
![Outreach 대상에 대한 세부 정보를 채우는 방법을 보여 주는 Experience Platform UI 스크린샷](../../assets/catalog/crm/outreach/destination-details.png)

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 모두 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

이 대상으로 대상을 활성화하는 방법에 대한 지침은 [프로필 및 대상을 스트리밍 대상 내보내기 대상으로 활성화](../../ui/activate-segment-streaming-destinations.md)를 참조하십시오.

### 매핑 고려 사항 및 예제 {#mapping-considerations-example}

대상 데이터를 Adobe Experience Platform에서 [!DNL Outreach] 대상으로 올바르게 보내려면 필드 매핑 단계를 거쳐야합니다. 매핑은 Experience Platform 계정의 XDM(Experience Data Model) 스키마 필드와 대상 대상의 해당 스키마 필드 간에 링크를 작성하는 것으로 구성됩니다. XDM 필드를 [!DNL Outreach] 대상 필드에 올바르게 매핑하려면 다음 단계를 따르십시오.

1. [!UICONTROL 매핑] 단계에서 **[!UICONTROL 새 매핑 추가]**를 클릭합니다. 화면에 새 매핑 행이 표시됩니다.
   ![새 매핑을 추가하는 방법을 보여주는 Experience Platform UI 스크린샷](../../assets/catalog/crm/outreach/add-new-mapping.png)

1. [!UICONTROL 원본 필드 선택] 창에서 **[!UICONTROL ID 네임스페이스 선택]** 범주를 선택하고 원하는 매핑을 추가합니다.
   ![Source 매핑을 보여 주는 Experience Platform UI 스크린샷](../../assets/catalog/crm/outreach/source-mapping.png)

1. [!UICONTROL 대상 필드 선택] 창에서 원본 필드를 매핑할 대상 필드 유형을 선택합니다.
   * **[!UICONTROL ID 네임스페이스 선택]**: 소스 필드를 목록의 ID 네임스페이스에 매핑하려면 이 옵션을 선택하십시오.
     ![OutreachId를 사용한 Target 매핑을 보여 주는 Experience Platform UI 스크린샷](../../assets/catalog/crm/outreach/target-mapping.png)

   * XDM 프로필 스키마와 [!DNL Outreach] 인스턴스 간에 다음 매핑을 추가합니다.

     | XDM 프로필 스키마 | [!DNL Outreach] 인스턴스 | 필수 |
     |---|---|---|
     | `Oid` | `OutreachId` | 예 |

   * **[!UICONTROL 사용자 지정 특성 선택]**: 소스 필드를 [!UICONTROL 특성 이름] 필드에 정의한 사용자 지정 특성에 매핑하려면 이 옵션을 선택하십시오. 지원되는 속성의 전체 목록은 [[!DNL Outreach] 잠재 고객 설명서](https://api.outreach.io/api/v2/docs#prospect)를 참조하십시오.
     ![LastName을 사용한 대상 매핑을 보여 주는 Experience Platform UI 스크린샷](../../assets/catalog/crm/outreach/target-mapping-lastname.png)

   * 예를 들어 업데이트할 값에 따라 XDM 프로필 스키마와 [!DNL Outreach] 인스턴스 사이에 다음 매핑을 추가합니다.

     | XDM 프로필 스키마 | [!DNL Outreach] 인스턴스 |
     |---|---|
     | `person.name.firstName` | `firstName` |
     | `person.name.lastName` | `lastName` |

   * 이러한 매핑을 사용하는 예는 다음과 같습니다.
     ![Target 매핑을 보여 주는 Experience Platform UI 스크린샷 예입니다.](../../assets/catalog/crm/outreach/mappings.png)

### 대상자 내보내기 예약 및 예제 {#schedule-segment-export-example}

* [대상 내보내기 예약](../../ui/activate-segment-streaming-destinations.md) 단계를 수행할 때 Experience Platform 대상을 [!DNL Outreach]의 사용자 지정 필드 특성에 수동으로 매핑해야 합니다.

* 이렇게 하려면 각 세그먼트를 선택한 다음 **[!UICONTROL 매핑 ID]** 필드의 [!DNL Outreach]에서 *사용자 지정 필드 `N` 레이블* 필드에 해당하는 숫자 값을 입력하십시오.

  >[!IMPORTANT]
  >
  > * [!UICONTROL 매핑 ID] 내에서 사용된 숫자 값 *(`N`)*&#x200B;은(는) [!DNL Outreach] 내의 숫자 값으로 대체된 사용자 지정 특성 키와 일치해야 합니다. 예: *사용자 지정 필드 `N` 레이블*.
  > * 전체 사용자 정의 필드 레이블이 아닌 숫자 값만 지정해야 합니다.
  > * [!DNL Outreach]은(는) 최대 150개의 사용자 지정 레이블 필드를 지원합니다.
  > * 자세한 내용은 [[!DNL Outreach] 잠재 고객 설명서](https://api.outreach.io/api/v2/docs#prospect)를 참조하세요.

   * 예:

     | [!DNL Outreach] 필드 | Experience Platform 매핑 ID |
     |---|---|
     | 사용자 지정 필드 `4` 레이블 | `4` |

     ![대상자 내보내기를 예약하는 동안 예제 매핑 ID를 보여 주는 Experience Platform UI 스크린샷입니다.](../../assets/catalog/crm/outreach/schedule-segment-export.png)

## 데이터 내보내기 유효성 검사 {#exported-data}

대상을 올바르게 설정했는지 확인하려면 아래 단계를 수행하십시오.

1. 대상 목록으로 이동하려면 **[!UICONTROL 대상]** > **[!UICONTROL 찾아보기]**를 선택하십시오.
   ![찾아보기 대상을 표시하는 Experience Platform UI 스크린샷입니다.](../../assets/catalog/crm/outreach/browse-destinations.png)

1. 대상을 선택하고 상태가 **[!UICONTROL 활성화됨]**인지 확인하십시오.
   ![선택한 대상에 대해 데이터 흐름이 실행되는 대상을 보여 주는 Experience Platform UI 스크린샷입니다.](../../assets/catalog/crm/outreach/destination-dataflow-run.png)

1. **[!DNL Activation data]** 탭으로 전환한 다음 대상 이름을 선택합니다.
   ![대상 활성화 데이터를 보여주는 Experience Platform UI 스크린샷입니다.](../../assets/catalog/crm/outreach/destinations-activation-data.png)

1. 대상자 요약을 모니터링하고 프로필 수가 세그먼트 내에서 만든 수에 해당하는지 확인합니다.
   ![세그먼트 요약을 보여 주는 Experience Platform UI 스크린샷입니다.](../../assets/catalog/crm/outreach/segment.png)

1. [!DNL Outreach] 웹 사이트에 로그인한 다음 [!DNL Apps] > [!DNL Contacts] 페이지로 이동하여 대상자의 프로필이 추가되었는지 확인합니다. [대상 예약](#schedule-segment-export-example) 단계 동안 제공된 [!UICONTROL 매핑 ID] 값을 기반으로 [!DNL Outreach]의 각 대상 상태가 Experience Platform의 해당 대상 상태로 업데이트되었음을 확인할 수 있습니다.

![대상자 상태가 업데이트된 [전달 전망] 페이지를 표시하는 [전달 UI] 스크린샷.](../../assets/catalog/crm/outreach/outreach-prospect.png)

## 데이터 사용 및 관리 {#data-usage-governance}

데이터를 처리할 때 모든 [!DNL Adobe Experience Platform] 대상이 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](/help/data-governance/home.md)를 참조하십시오.

## 오류 및 문제 해결 {#errors-and-troubleshooting}

데이터 흐름 실행을 확인할 때 다음 오류 메시지가 표시될 수 있습니다. `Bad request reported while pushing events to the destination. Please contact the administrator and try again.`

![잘못된 요청 오류를 표시하는 Experience Platform UI 스크린샷입니다.](../../assets/catalog/crm/outreach/error.png)

이 오류를 수정하려면 [!DNL Outreach] 대상에 대해 Experience Platform에서 제공한 [!UICONTROL 매핑 ID]이(가) 유효하고 [!DNL Outreach]에 있는지 확인하십시오.

## 추가 리소스 {#additional-resources}

[[!DNL Outreach] 설명서](https://api.outreach.io/api/v2/docs/)에는 문제를 디버깅하는 데 사용할 수 있는 [오류 응답](https://api.outreach.io/api/v2/docs#error-responses)에 대한 세부 정보가 있습니다.
