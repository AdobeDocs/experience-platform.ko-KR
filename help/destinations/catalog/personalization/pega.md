---
title: Pega 고객 의사 결정 허브 연결
description: Adobe Experience Platform의 Pega Customer Decisioning Hub 대상을 사용하여 프로필 속성 및 세그먼트 멤버십 데이터를 Pega Customer Decisioning Hub로 전송하여 다음으로 좋은 작업 결정을 내릴 수 있습니다.
exl-id: 0546da5d-d50d-43ec-bbc2-9468a7db4d90
source-git-commit: f06afec31b7fa550a612280b8ad665b8393ee2e3
workflow-type: tm+mt
source-wordcount: '1003'
ht-degree: 1%

---

# Pega 고객 의사 결정 허브 연결

## 개요 {#overview}

를 사용하십시오 [!DNL Pega Customer Decision Hub] 프로필 속성 및 세그먼트 멤버십 데이터를 [!DNL Pega Customer Decision Hub] 다음으로 좋은 작업 의사 결정

Adobe Experience Platform의 프로필 세그먼트 멤버십에 로드된 경우 [!DNL Pega Customer Decision Hub]은 적응형 모델에서 예측자로 사용할 수 있으며, 다음으로 최상의 작업 의사 결정을 위한 올바른 컨텍스트 및 행동 데이터를 제공하는 데 도움이 됩니다.

>[!IMPORTANT]
>
>이 설명서 페이지는 Pegasystems에서 만들었습니다. 문의 사항이나 업데이트 요청이 있으면 Pega에 직접 문의하십시오 [여기](mailto:support@pega.com).

## 사용 사례

를 사용하는 방법과 시기를 더 잘 이해할 수 있도록 하기 위해 [!DNL Customer Decision Hub] 대상, Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례는 다음과 같습니다.

### 통신

마케터는 다음과 같이 데이터 과학 모델을 기반으로 다음 모범 사례를 통해 통찰력을 활용하려고 합니다. [!DNL Pega Customer Decision Hub] 고객 참여를 위한 것입니다. [!DNL Pega Customer Decision Hub] 는 고객 의도에 크게 의존합니다(예: &quot;Interest_In_5G&quot;, &quot;Interest_in_Unlimited_Dataplan&quot; 또는 &quot;Interest_in_iPhone_accessories&quot;).

### 금융 서비스

마케팅 담당자는 연금 제도 또는 퇴직 계획 뉴스레터를 구독하거나 구독 취소한 고객을 위해 오퍼를 최적화하려고 합니다. 금융 서비스 회사는 고유한 CRM에서 여러 고객 ID를 Adobe Experience Platform으로 수집하고, 고유한 오프라인 데이터에서 세그먼트를 작성하고, 세그먼트를 입력 및 종료하는 프로필을 로 보낼 수 있습니다 [!DNL Pega Customer Decision Hub] 아웃바운드 채널에서 다음으로 좋은 작업(NBA) 의사 결정을 위해.

## 전제 조건 {#prerequisites}

이 대상을 사용하여 Adobe Experience Platform에서 데이터를 내보내려면 먼저 의 다음 전제 조건을 완료해야 합니다. [!DNL Pega Customer Decision Hub]:

* 에서 Adobe 세그먼트 멤버십 구성 요소 구성 [!DNL Pega Customer Decision Hub] 인스턴스.
* OAuth 2.0 구성 [클라이언트 자격 증명을 사용한 클라이언트 등록](https://docs.pega.com/security/87/creating-and-configuring-oauth-20-client-registration) 권한 부여 [!DNL Pega Customer Decision Hub] 인스턴스.
* 구성 [실시간 실행 데이터 흐름](https://docs.pega.com/decision-management/87/creating-real-time-run-data-flows) 세그먼트 멤버십 Adobe 데이터 플로우에서 사용할 수 있습니다 [!DNL Pega Customer Decision Hub] 인스턴스.

## 지원되는 ID {#supported-identities}

[!DNL Pega Customer Decision Hub] 은 아래 표에 설명된 사용자 지정 사용자 ID의 활성화를 지원합니다. 자세한 내용은 [id](/help/identity-service/namespaces.md).

| Target ID | 설명 |
|---|---|
| *CustomerID* | 에서 프로필을 고유하게 식별하는 일반 사용자 식별자입니다 [!DNL Pega Customer Decision Hub] 및 Adobe Experience Platform |

{style=&quot;table-layout:auto&quot;}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | 식별자로 세그먼트의 모든 멤버 내보내기(*CustomerID*), 속성(성, 이름, 위치 등) 및 세그먼트 멤버십 데이터를 포함할 수 있습니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 항상 API 기반 연결입니다. Experience Platform에서 프로필이 업데이트되는 즉시, 세그먼트 평가를 기반으로 커넥터는 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. 자세한 내용은 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## 대상에 연결 {#connect}

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로우에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상에 인증 {#authenticate}

#### OAuth 2 클라이언트 자격 증명 인증 {#oauth-2-client-credentials-authentication}

![클라이언트 자격 증명 인증이 있는 OAuth 2를 사용하여 Pega CDH 대상에 연결할 수 있는 UI 화면의 이미지입니다](../../assets/catalog/personalization/pega/pega-api-authentication-oauth2-client-credentials.png)

아래 필드를 작성하고 을(를) 선택합니다 **[!UICONTROL 대상에 연결]**:

* **[!UICONTROL 액세스 토큰 URL]**: 사용자의 OAuth 2 액세스 토큰 URL입니다 [!DNL Pega Customer Decision Hub] 인스턴스.
* **[!UICONTROL 클라이언트 ID]**: OAuth 2 [!DNL client ID] ID를 생성할 때 [!DNL Pega Customer Decision Hub] 인스턴스.
* **[!UICONTROL 클라이언트 암호]**: OAuth 2 [!DNL client secret] ID를 생성할 때 [!DNL Pega Customer Decision Hub] 인스턴스.

### 대상 세부 사항 채우기 {#destination-details}

에 인증 연결을 설정한 후 [!DNL Pega Customer Decision Hub]를 채울 경우 대상에 대해 다음 정보를 제공합니다.

![Pega CDH 대상 세부 사항에 대해 완료된 필드를 보여주는 UI 화면의 이미지](../../assets/catalog/personalization/pega/pega-connect-destination.png)

대상에 대한 세부 사항을 구성하려면 필수 필드를 입력하고 을(를) 선택합니다 **[!UICONTROL 다음]**.

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식하는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 호스트 이름]**: 프로필을 json 데이터로 내보내는 Pega Customer Decision Hub 호스트 이름입니다.

## 세그먼트를 이 대상에 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

자세한 내용은 [스트리밍 프로필 내보내기 대상으로 대상 데이터 활성화](../../ui/activate-streaming-profile-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

### 대상 속성 {#attributes}

에서 [[!UICONTROL 속성 선택]](../../ui/activate-streaming-profile-destinations.md#select-attributes) Adobe은 사용자 지정 페이지에서 고유 식별자를 선택할 것을 권장합니다 [조합 스키마](../../../profile/home.md#profile-fragments-and-union-schemas). 대상으로 내보낼 고유 식별자 및 기타 모든 XDM 필드를 선택합니다.

### 매핑 예: 에서 프로필 업데이트 활성화 [!DNL Pega Customer Decision Hub]

아래는 프로필을 로 내보낼 때 올바른 ID 매핑의 예입니다 [!DNL Pega Customer Decision Hub].

소스 필드 선택:

* 식별자를 선택합니다(예: CustomerID) 를 Adobe Experience Platform 및 [!DNL Pega Customer Decision Hub].
* 내보내고 업데이트해야 하는 XDM 소스 프로필 속성 변경 사항을 선택합니다. [!DNL Pega Customer Decision Hub].

대상 필드 선택:

* 을(를) 선택합니다 `CustomerID` 네임스페이스 를 target id로 지정합니다.
* 해당 XDM 소스 프로필 속성에 매핑해야 하는 대상 프로필 속성 이름을 선택합니다.

![ID 매핑](../../assets/catalog/personalization/pega/pega-source-destination-mapping.png)

## 내보낸 데이터 / 데이터 내보내기 유효성 검사 {#exported-data}

프로필에 대한 성공적인 세그먼트 멤버십 업데이트는 Pega 마케팅 세그먼트 멤버십 데이터 저장소에 세그먼트 식별자, 이름 및 상태를 삽입합니다. 멤버십 데이터는 [!DNL Pega Customer Decision Hub]아래에 표시된 대로,
![고객 프로필 디자이너를 사용하여 Adobe 세그먼트 멤버십 데이터를 고객에 연결할 수 있는 UI 화면의 이미지](../../assets/catalog/personalization/pega/pega-profile-designer-associate.png)

세그먼트 멤버십 데이터는 아래 표시된 대로 Next-Best-Action Designer Engagement 정책에 사용됩니다.
![Pega Next-Best-Action Designer의 참여 정책에 조건으로 세그먼트 멤버십 필드를 추가할 수 있는 UI 화면의 이미지](../../assets/catalog/personalization/pega/pega-profile-designer-engagment.png)

고객 세그먼트 멤버십 데이터 필드는 아래와 같이 적응형 모델에 예측자로 추가됩니다.
![Prediction Studio를 사용하여 적응형 모델에서 세그먼트 멤버십 필드를 예측자로 추가할 수 있는 UI 화면의 이미지](../../assets/catalog/personalization/pega/pega-profile-designer-adaptivemodel.png)

## 추가 리소스 {#additional-resources}

자세한 내용은 [OAuth 2.0 클라이언트 등록 설정](https://docs.pega.com/security/87/creating-and-configuring-oauth-20-client-registration) in [!DNL Pega Customer Decision Hub].

자세한 내용은 [데이터 흐름에 대한 실시간 실행 만들기](https://docs.pega.com/decision-management/87/creating-real-time-run-data-flows) in [!DNL Pega Customer Decision Hub].

자세한 내용은 [고객 프로필 디자이너에서 고객 레코드 관리](https://docs.pega.com/whats-new-pega-platform/manage-customer-records-customer-profile-designer-86).

## 데이터 사용 및 거버넌스 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스를 적용하는 경우 다음을 참조하십시오. [데이터 거버넌스 개요](/help/data-governance/home.md).
