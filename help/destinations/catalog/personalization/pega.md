---
title: Pega 고객 의사 결정 허브 연결
description: Adobe Experience Platform의 Pega Customer Decision Hub 대상을 사용하여 프로필 속성 및 대상자 멤버십 데이터를 Pega Customer Decision Hub로 전송하여 다음 모범 조치 결정을 내릴 수 있습니다.
exl-id: 0546da5d-d50d-43ec-bbc2-9468a7db4d90
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '1025'
ht-degree: 2%

---

# Pega 고객 의사 결정 허브 연결

## 개요 {#overview}

사용 [!DNL Pega Customer Decision Hub] 프로필 속성 및 대상자 멤버십 데이터를 보낼 Adobe Experience Platform의 대상 [!DNL Pega Customer Decision Hub] 을 참조하십시오.

Adobe Experience Platform의 프로필 대상 멤버십( 로 로드됨) [!DNL Pega Customer Decision Hub]는 적응형 모델에서 예측 변수로 사용할 수 있으며, 차후 최선의 행동 결정을 위해 올바른 컨텍스트 및 행동 데이터를 제공하는 데 도움이 됩니다.

>[!IMPORTANT]
>
>이 대상 커넥터 및 설명서 페이지는 Pegasystem에서 만들고 유지 관리합니다. 문의 사항이나 업데이트 요청은 페가에게 직접 문의하시기 바랍니다 [여기](mailto:support@pega.com).

## 사용 사례

을(를) 사용하는 방법과 시기를 더 잘 이해할 수 있도록 [!DNL Customer Decision Hub] 대상: 다음은 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례입니다.

### 전기 통신

마케터는 에서 제공한 대로 데이터 과학 모델 기반 다음 모범 사례에서 인사이트를 활용하려고 합니다. [!DNL Pega Customer Decision Hub] 고객 참여용. [!DNL Pega Customer Decision Hub] 는 고객 의도에 크게 의존합니다. 예를 들어 &quot;Interest_In_5G&quot;, &quot;Interest_in_Unlimited_Dataplan&quot; 또는 &quot;Interest_in_iPhone_accessories&quot;와 같습니다.

### 금융 서비스

마케터는 연금 제도 또는 퇴직 연금 제도 뉴스레터를 구독하거나 구독 취소한 고객을 위해 오퍼를 최적화하려고 합니다. 금융 서비스 회사는 자체 CRM에서 여러 고객 ID를 Adobe Experience Platform으로 수집하고, 자체 오프라인 데이터에서 대상을 작성하고, 대상을 입력 및 종료하는 프로필을 로 보낼 수 있습니다. [!DNL Pega Customer Decision Hub] 아웃바운드 채널의 다음 베스트 액션(NBA) 의사 결정용.

## 전제 조건 {#prerequisites}

이 대상을 사용하여 Adobe Experience Platform에서 데이터를 내보내려면 먼저 의 다음 사전 요구 사항을 완료해야 합니다. [!DNL Pega Customer Decision Hub]:

* 구성 [Adobe Experience Platform 프로필 및 대상 멤버십 통합 구성 요소](https://docs.pega.com/component/customer-decision-hub/adobe-experience-platform-profile-and-segment-membership-integration-component) (으)로 [!DNL Pega Customer Decision Hub] 인스턴스.
* OAuth 2.0 구성 [클라이언트 자격 증명을 사용한 클라이언트 등록](https://docs.pega.com/security/87/creating-and-configuring-oauth-20-client-registration) 에 유형 부여 [!DNL Pega Customer Decision Hub] 인스턴스.
* 구성 [실시간 실행 데이터 흐름](https://docs.pega.com/decision-management/87/creating-real-time-run-data-flows) 의 Adobe 대상 멤버십 데이터 흐름용 [!DNL Pega Customer Decision Hub] 인스턴스.

## 지원되는 ID {#supported-identities}

[!DNL Pega Customer Decision Hub] 는 아래 표에 설명된 사용자 지정 사용자 ID의 활성화를 지원합니다. 자세한 내용은 [id](/help/identity-service/namespaces.md).

| 대상 ID | 설명 |
|---|---|
| *고객 ID* | 에서 프로필을 고유하게 식별하는 공통 사용자 식별자 [!DNL Pega Customer Decision Hub] 및 Adobe Experience Platform |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | 식별자를 사용하여 대상자의 모든 구성원 내보내기(*고객 ID*), 속성(성, 이름, 위치 등) 및 대상 멤버십 데이터입니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 항상 API 기반 연결입니다. Experience Platform에서 대상 평가를 기반으로 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. 자세한 내용은 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

이 대상에 연결하려면 다음과같이 하십시오. [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

#### OAuth 2 클라이언트 자격 증명 인증 {#oauth-2-client-credentials-authentication}

![클라이언트 자격 증명 인증이 있는 OAuth 2를 사용하여 페가 CDH 대상에 연결할 수 있는 UI 화면의 이미지](../../assets/catalog/personalization/pega/pega-api-authentication-oauth2-client-credentials.png)

아래 필드를 입력한 다음 선택 **[!UICONTROL 대상에 연결]**:

* **[!UICONTROL 토큰 URL 액세스]**: 의 OAuth 2 액세스 토큰 URL [!DNL Pega Customer Decision Hub] 인스턴스.
* **[!UICONTROL 클라이언트 ID]**: OAuth 2 [!DNL client ID] 에서 생성한 항목 [!DNL Pega Customer Decision Hub] 인스턴스.
* **[!UICONTROL 클라이언트 암호]**: OAuth 2 [!DNL client secret] 에서 생성한 항목 [!DNL Pega Customer Decision Hub] 인스턴스.

### 대상 세부 정보 입력 {#destination-details}

에 대한 인증 연결 설정 후 [!DNL Pega Customer Decision Hub]에 대상에 대해 다음 정보를 제공합니다.

![페가 CDH 대상 세부 사항에 대해 완료된 필드를 표시하는 UI 화면 이미지](../../assets/catalog/personalization/pega/pega-connect-destination.png)

대상에 대한 세부 정보를 구성하려면 필수 필드를 입력한 다음 을(를) 선택합니다 **[!UICONTROL 다음]**.

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 호스트 이름]**: 프로필을 json 데이터로 내보내는 Pega 고객 의사 결정 허브 호스트 이름입니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.
>* 내보내려면 *id*, 다음이 필요합니다. **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). <br> ![워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다.](/help/destinations/assets/overview/export-identities-to-destination.png "워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다."){width="100" zoomable="yes"}

다음을 참조하십시오 [대상자 데이터를 스트리밍 프로필 내보내기 대상으로 활성화](../../ui/activate-streaming-profile-destinations.md) 이 대상에 대한 대상자 활성화에 대한 지침을 참조하십시오.

### 대상 속성 {#attributes}

다음에서 [[!UICONTROL 속성 선택]](../../ui/activate-streaming-profile-destinations.md#select-attributes) Adobe은 다음 단계에서 고유 식별자를 선택할 것을 권장합니다. [유니온 스키마](../../../profile/home.md#profile-fragments-and-union-schemas). 대상으로 내보낼 고유 식별자 및 기타 XDM 필드를 선택합니다.

### 매핑 예:에서 프로필 업데이트 활성화 [!DNL Pega Customer Decision Hub] {#mapping-example}

다음은 프로필을 로 내보낼 때 올바른 ID 매핑의 예입니다 [!DNL Pega Customer Decision Hub].

소스 필드 선택:

* Adobe Experience Platform에서 프로필을 고유하게 식별하는 소스 ID로 식별자(예: CustomerID)를 선택하고 [!DNL Pega Customer Decision Hub].
* 에서 내보내고 업데이트해야 하는 XDM 소스 프로필 속성 변경 사항을 선택합니다. [!DNL Pega Customer Decision Hub].

대상 필드 선택:

* 다음 항목 선택 `CustomerID` 네임스페이스를 대상 ID로 사용합니다.
* 해당 XDM 소스 프로필 속성에 매핑해야 하는 대상 프로필 속성 이름을 선택합니다.

![ID 매핑](../../assets/catalog/personalization/pega/pega-source-destination-mapping.png)

## 내보낸 데이터/데이터 내보내기 유효성 검사 {#exported-data}

프로필에 대한 대상 멤버십을 성공적으로 업데이트하면 페가 마케팅 대상 멤버십 데이터 저장소에 대상 식별자, 이름 및 상태가 삽입됩니다. 멤버십 데이터는 의 고객 프로필 디자이너를 사용하여 고객과 연결됩니다. [!DNL Pega Customer Decision Hub]아래에 표시된 대로 를 클릭합니다.
![고객 프로필 디자이너를 사용하여 Adobe 대상 멤버십 데이터를 고객에 연결할 수 있는 UI 화면의 이미지](../../assets/catalog/personalization/pega/pega-profile-designer-associate.png)

대상 멤버십 데이터는 아래와 같이 다음으로 가장 적합한 작업을 결정하기 위해 Pega 다음으로 적합한 작업 디자이너 참여 정책에 사용됩니다.
![Pega Next-Best-Action Designer의 참여 정책에 조건으로 대상 멤버십 필드를 추가할 수 있는 UI 화면의 이미지](../../assets/catalog/personalization/pega/pega-profile-designer-engagment.png)

고객 대상 멤버십 데이터 필드는 아래와 같이 적응형 모델에 예측 변수로 추가됩니다.
![Prediction Studio를 사용하여 적응형 모델에서 대상자 멤버십 필드를 예측자로 추가할 수 있는 UI 화면의 이미지](../../assets/catalog/personalization/pega/pega-profile-designer-adaptivemodel.png)

## 추가 리소스 {#additional-resources}

다음을 참조하십시오 [OAuth 2.0 클라이언트 등록 설정](https://docs.pega.com/security/87/creating-and-configuring-oauth-20-client-registration) 위치: [!DNL Pega Customer Decision Hub].

다음을 참조하십시오 [데이터 흐름에 대한 실시간 실행 만들기](https://docs.pega.com/decision-management/87/creating-real-time-run-data-flows) 위치: [!DNL Pega Customer Decision Hub].

다음을 참조하십시오 [고객 프로필 디자이너에서 고객 레코드 관리](https://docs.pega.com/whats-new-pega-platform/manage-customer-records-customer-profile-designer-86).

## 데이터 사용 및 관리 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스 시행, 다음을 참조하십시오. [데이터 거버넌스 개요](/help/data-governance/home.md).
