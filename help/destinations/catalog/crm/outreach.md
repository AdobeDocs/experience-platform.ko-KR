---
keywords: crm;CRM;CRM 대상;도달 범위;CRM 대상 도달
title: 무선 연결
description: Outreach 대상을 사용하면 비즈니스 요구 사항에 맞게 계정 데이터를 내보내고 Outreach 내에서 활성화할 수 있습니다.
source-git-commit: 27da0f8d7896fd32e8a1b828630db7e5e08185c2
workflow-type: tm+mt
source-wordcount: '1714'
ht-degree: 1%

---


# [!DNL Outreach] 연결

## 개요 {#overview}

[[!DNL Outreach]](https://www.outreach.io/) 는 전 세계에서 가장 많은 B2B 구매자 상호 작용 데이터와 독점 AI 기술에 대한 상당한 투자를 보유한 판매 실행 플랫폼으로서 판매 데이터를 인텔리전스로 변환합니다. [!DNL Outreach] 영업 참여를 자동화하고 수익 인텔리전스를 활용하여 효율성, 예측 가능성 및 성장을 향상시킬 수 있습니다.

이 [!DNL Adobe Experience Platform] [대상](/help/destinations/home.md) 활용 [아웃바운드 업데이트 리소스 API](https://api.outreach.io/api/v2/docs#update-an-existing-resource): 의 잠재 고객에 해당하는 세그먼트 내에서 ID를 업데이트할 수 있습니다. [!DNL Outreach].

[!DNL Outreach] 는 와 통신하기 위해 인증 메커니즘으로 인증 부여와 함께 OAuth 2를 사용합니다 [!DNL Outreach] [!DNL Update Resource API]. 인증 지침 [!DNL Outreach] 인스턴스는 아래의, 내에서 [대상에 인증](#authenticate) 섹션을 참조하십시오.

## 사용 사례 {#use-cases}

마케터는 Adobe Experience Platform 프로필의 속성을 기반으로 개인화된 경험을 잠재 고객에게 제공할 수 있습니다. 오프라인 데이터에서 세그먼트를 작성하고 이러한 세그먼트를 [!DNL Outreach]: 세그먼트 및 프로필이 Adobe Experience Platform에서 업데이트되는 즉시 잠재 고객의 피드에 표시됩니다.

## 전제 조건 {#prerequisites}

### Experience Platform 사전 요구 사항 {#prerequisites-in-experience-platform}

데이터를 로 활성화하기 전에 [!DNL Outreach] 대상, [스키마](/help/xdm/schema/composition.md), [데이터 세트](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=en), 및 [세그먼트](https://experienceleague.adobe.com/docs/platform-learn/tutorials/segments/create-segments.html?lang=en) 에서 생성됨 [!DNL Experience Platform].

에 대한 Adobe 설명서를 참조하십시오. [세그먼트 멤버십 세부 정보 스키마 필드 그룹](/help/xdm/field-groups/profile/segmentation.md) 세그먼트 상태에 대한 지침이 필요한 경우.

### 도달 범위 사전 요구 사항 {#prerequisites-destination}

에서 다음 전제 조건을 확인합니다. [!DNL Outreach]를 입력하여 Platform에서 로 데이터를 [!DNL Outreach] 계정:

#### 도달 범위 계정이 있어야 합니다. {#prerequisites-account}

로 이동합니다. [!DNL Outreach] [로그인](https://accounts.outreach.io/users/sign_in) 계정을 아직 등록하지 않은 경우 페이지를 만들어 계정을 만듭니다. 자세한 내용은 [!DNL Outreach] 지원 [페이지](https://support.outreach.io/hc/en-us/articles/207238607-Claim-Your-Outreach-Account) 자세한 내용

를 인증하기 전에 아래 항목을 참고하십시오 [!DNL Outreach] CRM 대상:

| 자격 증명 | 설명 |
|---|---|
| 이메일 | 사용자 [!DNL Outreach] 계정 이메일 |
| 암호 | 사용자 [!DNL Outreach] 계정 암호 |

#### 사용자 지정 필드 레이블 설정 {#prerequisites-custom-fields}

[!DNL Outreach] 의 사용자 지정 필드 지원 [잠재 고객](https://support.outreach.io/hc/en-us/articles/360001557554-Outreach-Prospect-Profile-Overview). 을(를) 참조하십시오. [Outreach에서 사용자 지정 필드를 추가하는 방법](https://support.outreach.io/hc/en-us/articles/219124908-How-To-Add-a-Custom-Field-in-Outreach) 추가 지침 쉽게 식별할 수 있도록 기본값을 유지하는 대신 레이블을 해당 세그먼트 이름으로 수동으로 업데이트하는 것이 좋습니다. 예를 들면 다음과 같습니다.

[!DNL Outreach] 사용자 지정 필드를 표시하는 잠재 고객을 위한 설정 페이지입니다.
![설정 페이지의 사용자 지정 필드를 보여주는 Outreach UI 스크린샷입니다.](../../assets/catalog/crm/outreach/outreach-custom-fields.png)

[!DNL Outreach] 잠재 고객 설정 페이지에 *사용자에게 친숙한* 세그먼트 이름과 일치하는 레이블. 이 레이블에 대해 잠재 고객 페이지에서 세그먼트 상태를 볼 수 있습니다.
![설정 페이지에서 관련 레이블이 있는 사용자 지정 필드를 보여주는 아웃바운드 UI 스크린샷입니다.](../../assets/catalog/crm/outreach/outreach-custom-field-labels.png)

>[!NOTE]
>
> 레이블 이름은 쉽게 식별할 수 있습니다. 잠재 고객을 업데이트할 때는 사용되지 않습니다.

## 가드레일

다음 [!DNL Outreach] API는 사용자당 시간당 10,000개의 요청의 비율 제한이 있습니다. 이 한도에 도달하면 `429` 응답(다음 메시지 포함): `You have exceeded your permitted rate limit of 10,000; please try again at 2017-01-01T00:00:00.`.

이 메시지를 받은 경우 비율 임계값을 준수하도록 세그먼트 내보내기 일정을 업데이트해야 합니다.

자세한 내용은 [[!DNL Outreach] 설명서](https://api.outreach.io/api/v2/docs#rate-limiting) 추가 세부 정보.

## 지원되는 ID {#supported-identities}

[!DNL Outreach] 은 아래 표에 설명된 id 업데이트를 지원합니다. 추가 정보 [id](/help/identity-service/namespaces.md).

| Target ID | 설명 | 고려 사항 |
|---|---|---|
| `OutreachId` | <ul><li>[!DNL Outreach] 식별자. 잠재 고객 프로필에 해당하는 숫자 값입니다.</li><li>ID는 [!DNL Outreach] 업데이트 중인 잠재 고객의 URL.</li><li>자세한 내용은 [[!DNL Outreach] 설명서](https://api.outreach.io/api/v2/docs#update-an-existing-resource) 자세한 내용</li></ul> | 필수입니다 |

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | <ul><li> 원하는 스키마 필드와 함께 세그먼트의 모든 구성원을 내보냅니다 *(예: 이메일 주소, 전화 번호, 성)*: 사용자 필드 매핑에 따라 다릅니다.</li><li> 의 각 세그먼트 상태 [!DNL Outreach] 은(는) [!UICONTROL 매핑 ID] 다음 기간 동안 제공된 값 [세그먼트 예약](#schedule-segment-export-example) 단계.</li></ul> |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | <ul><li> 스트리밍 대상은 &quot;항상 설정&quot; API 기반 연결입니다. 세그먼트 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터는 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations).</li></ul> |

{style=&quot;table-layout:auto&quot;}

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
> 대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로우에서 아래 두 섹션에 나열된 필드를 채웁니다.

내 **[!UICONTROL 대상]** > **[!UICONTROL 카탈로그]** 검색 대상 [!DNL Outreach]. 또는 CRM 카테고리에서 찾을 수 있습니다.

### 대상에 인증 {#authenticate}

대상을 인증하려면 **[!UICONTROL 대상에 연결]**.

![Platform UI 스크린샷에서 Outreach에 대한 인증 방법을 보여 줍니다.](../../assets/catalog/crm/outreach/authenticate-destination.png)

이 표시됩니다. [!DNL Outreach] 로그인 페이지. 이메일을 제공합니다.

![Outreach에 인증할 이메일을 입력할 필드를 보여주는 Outreach UI 스크린샷입니다.](../../assets/catalog/crm/outreach/authenticate-destination-login-email.png)

다음에 암호를 입력합니다.

![아웃바운드 인증을 위한 암호 단계를 입력하는 필드를 보여주는 아웃바운드 UI 스크린샷입니다.](../../assets/catalog/crm/outreach/authenticate-destination-login-password.png)

* **[!UICONTROL 사용자 이름]**: 사용자 [!DNL Outreach] 계정 전자 메일.
* **[!UICONTROL 암호]**: 사용자 [!DNL Outreach] 계정 암호입니다.

제공된 세부 정보가 유효한 경우 UI에 **연결됨** 녹색 확인 표시가 있는 상태 그런 다음 다음 다음 단계로 진행할 수 있습니다.

### 대상 세부 사항 채우기 {#destination-details}

대상에 대한 세부 사항을 구성하려면 아래 필수 및 선택적 필드를 입력합니다. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.
![Experience Platform UI 스크린샷에서 Outreach 대상에 대한 세부 사항을 작성하는 방법을 보여 줍니다.](../../assets/catalog/crm/outreach/destination-details.png)

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식하는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상으로 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보 제공을 마치면 를 선택합니다 **[!UICONTROL 다음]**.

## 세그먼트를 이 대상에 활성화 {#activate}

>[!IMPORTANT]
> 
> 데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

읽기 [스트리밍 세그먼트 내보내기 대상으로 프로필 및 세그먼트를 활성화합니다](../../ui/activate-segment-streaming-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

### 매핑 고려 사항 및 예 {#mapping-considerations-example}

대상 데이터를 Adobe Experience Platform에서 로 올바로 보내려면 [!DNL Outreach] 대상, 필드 매핑 단계를 거쳐야 합니다. 매핑은 플랫폼 계정의 Experience Data Model(XDM) 스키마 필드와 대상 대상의 해당 상당 요소 간에 링크를 만드는 작업으로 이루어집니다. XDM 필드를 [!DNL Outreach] 대상 필드: 다음 단계를 수행합니다.

1. 에서 [!UICONTROL 매핑] step, **[!UICONTROL 새 매핑 추가]**. 화면에 새 매핑 행이 표시됩니다.
   ![새 매핑을 추가하는 방법을 보여주는 Platform UI 스크린샷](../../assets/catalog/crm/outreach/add-new-mapping.png)

1. 에서 [!UICONTROL 소스 필드 선택] 창에서 **[!UICONTROL ID 네임스페이스 선택]** 카테고리를 추가하고 원하는 매핑을 추가합니다.
   ![소스 매핑을 보여주는 Platform UI 스크린샷](../../assets/catalog/crm/outreach/source-mapping.png)

1. 에서 [!UICONTROL 대상 필드 선택] 창에서 소스 필드를 매핑할 대상 필드의 유형을 선택합니다.
   * **[!UICONTROL ID 네임스페이스 선택]**: 목록에서 소스 필드를 id 네임스페이스에 매핑하려면 이 옵션을 선택합니다.
      ![OutreachId를 사용한 Target 매핑을 보여주는 Platform UI 스크린샷입니다.](../../assets/catalog/crm/outreach/target-mapping.png)

   * XDM 프로필 스키마와 프로필 스키마 사이에 다음 매핑을 추가합니다 [!DNL Outreach] 인스턴스: |XDM 프로필 스키마|[!DNL Outreach] 인스턴스| 필수| |—|—|—| |`Oid`|`OutreachId`| 예 |

   * **[!UICONTROL 사용자 지정 속성 선택]**: 소스 필드를 [!UICONTROL 속성 이름] 필드. 을(를) 참조하십시오. [[!DNL Outreach] 잠재 고객 설명서](https://api.outreach.io/api/v2/docs#prospect) 를 참조하십시오.
      ![LastName을 사용한 Target 매핑을 보여주는 Platform UI 스크린샷입니다.](../../assets/catalog/crm/outreach/target-mapping-lastname.png)

   * 예를 들어 업데이트할 값에 따라 XDM 프로필 스키마와 프로필 스키마 사이에 다음 매핑을 추가합니다 [!DNL Outreach] 인스턴스: |XDM 프로필 스키마|[!DNL Outreach] 인스턴스| |—|—| |`person.name.firstName`|`firstName`| |`person.name.lastName`|`lastName`|

   * 이러한 매핑을 사용하는 예는 다음과 같습니다.
      ![Target 매핑을 보여주는 Platform UI 스크린샷 예입니다.](../../assets/catalog/crm/outreach/mappings.png)

### 세그먼트 내보내기 예약 및 예제 {#schedule-segment-export-example}

* 다음을 수행할 때 [세그먼트 내보내기 예약](../../ui/activate-segment-streaming-destinations.md) 단계는 Platform 세그먼트를 의 사용자 지정 필드 속성에 수동으로 매핑해야 합니다. [!DNL Outreach].

* 이렇게 하려면 각 세그먼트를 선택한 다음, *사용자 지정 필드 `N` 레이블* 필드 위치 [!DNL Outreach] 에서 **[!UICONTROL 매핑 ID]** 필드.

   >[!IMPORTANT]
   >
   > * 숫자 값 *(`N`)* 내에서 사용 [!UICONTROL 매핑 ID] 는 내에 숫자 값이 있는 사용자 지정 속성 키와 일치해야 합니다. [!DNL Outreach]. 예: *사용자 지정 필드 `N` 레이블*.
   > * 전체 사용자 지정 필드 레이블이 아니라 숫자 값만 지정해야 합니다.
   > * [!DNL Outreach] 은 최대 150개의 사용자 지정 레이블 필드를 지원합니다.
   > * 을(를) 참조하십시오. [[!DNL Outreach] 잠재 고객 설명서](https://api.outreach.io/api/v2/docs#prospect) 자세한 내용


   * 예:

      | [!DNL Outreach] 필드 | 플랫폼 매핑 ID |
      |---|---|
      | 사용자 지정 필드 `4` 레이블 | `4` |

      ![세그먼트 내보내기 예약 중 매핑 ID의 예를 보여주는 Platform UI 스크린샷입니다.](../../assets/catalog/crm/outreach/schedule-segment-export.png)

## 데이터 내보내기의 유효성 검사 {#exported-data}

대상을 올바르게 설정했는지 확인하려면 아래 단계를 수행하십시오.

1. 선택 **[!UICONTROL 대상]** > **[!UICONTROL 찾아보기]** 대상 목록으로 이동합니다.
   ![찾아보기 대상을 보여주는 Platform UI 스크린샷입니다.](../../assets/catalog/crm/outreach/browse-destinations.png)

1. 대상을 선택하고 상태가 맞는지 확인합니다 **[!UICONTROL 활성화됨]**.
   ![선택한 대상에 대한 대상 데이터 흐름 실행을 보여주는 플랫폼 UI 스크린샷입니다.](../../assets/catalog/crm/outreach/destination-dataflow-run.png)

1. 로 전환 **[!DNL Activation data]** 탭을 클릭한 다음 세그먼트 이름을 선택합니다.
   ![대상 활성화 데이터를 보여주는 Platform UI 스크린샷입니다.](../../assets/catalog/crm/outreach/destinations-activation-data.png)

1. 세그먼트 요약을 모니터링하고 프로필 수가 세그먼트 내에서 생성된 수에 해당하는지 확인합니다.
   ![세그먼트 요약을 보여주는 Platform UI 스크린샷.](../../assets/catalog/crm/outreach/segment.png)

1. 에 로그인합니다. [!DNL Outreach] 웹 사이트에서 [!DNL Apps] > [!DNL Contacts] 페이지를 방문하여 세그먼트의 프로필이 추가되었는지 확인합니다. 에서 각 세그먼트 상태를 확인할 수 있습니다. [!DNL Outreach] 이(가) [!UICONTROL 매핑 ID] 다음 기간 동안 제공된 값 [세그먼트 예약](#schedule-segment-export-example) 단계.

![업데이트된 세그먼트 상태가 있는 도달 범위 잠재 고객 페이지를 보여주는 도달 범위 UI 스크린샷입니다.](../../assets/catalog/crm/outreach/outreach-prospect.png)

## 데이터 사용 및 거버넌스 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스를 적용하는 경우 다음을 참조하십시오. [데이터 거버넌스 개요](/help/data-governance/home.md).

## 오류 및 문제 해결 {#errors-and-troubleshooting}

데이터 흐름 실행을 확인할 때 다음 오류 메시지가 표시될 수 있습니다. `Bad request reported while pushing events to the destination. Please contact the administrator and try again.`

![잘못된 요청 오류를 보여주는 Platform UI 스크린샷입니다.](../../assets/catalog/crm/outreach/error.png)

이 오류를 해결하려면 [!UICONTROL 매핑 ID] 을(를) 위해 플랫폼에서 제공한 [!DNL Outreach] 세그먼트가 유효하고 다음 위치에 있음 [!DNL Outreach].

## 추가 리소스 {#additional-resources}

다음 [[!DNL Outreach] 설명서](https://api.outreach.io/api/v2/docs/) 세부 사항이 있음 [오류 응답](https://api.outreach.io/api/v2/docs#error-responses) 문제를 디버깅하는 데 사용할 수 있습니다.
