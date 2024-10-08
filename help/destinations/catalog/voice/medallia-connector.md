---
title: 메달리아 연결
description: 타겟팅된 Medallia 설문 조사 및 피드백 수집을 위한 프로필을 활성화하여 고객의 요구 사항과 기대치를 보다 잘 이해할 수 있습니다.
exl-id: 2c2766eb-7be1-418c-bf17-d119d244de92
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1135'
ht-degree: 2%

---

# 메달리아 연결

## 개요 {#overview}

타겟팅된 Medallia 설문 조사 및 피드백 수집을 위한 프로필을 활성화하여 고객의 요구 사항과 기대치를 보다 잘 이해할 수 있습니다.

>[!IMPORTANT]
>
>이 대상 커넥터 및 설명서 페이지는 Medallia 팀에서 만들고 관리합니다. 문의 사항이나 업데이트 요청은 adobe-integrations@medallia.com으로 직접 문의하시기 바랍니다.

## 사용 사례 {#use-cases}

Medallia 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례를 소개합니다.

### 사용 사례 #1

B2B 브랜드는 온보딩 프로그램을 평가하고 간소화하려고 합니다. 온보딩 프로세스를 완료한 고객에게 실시간으로 개인화된 설문 조사를 보내려고 합니다.

### 사용 사례 #2

소매업체는 주문 이행에 대한 고객 선호도를 더 잘 이해하고자 합니다. 지난 한 달 동안 온라인 및 매장 내에서 구매한 고객에게 간단한 1문 SMS 설문 조사를 보내려고 합니다.

## 전제 조건 {#prerequisites}

Medallia 연결을 설정하려면 다음 정보가 필요합니다.
* **OAuth 토큰 끝점 URL**
* **클라이언트 ID**
* **클라이언트 암호**
* **API 게이트웨이 URL**
* **API 이름 가져오기**

이러한 세부 정보를 얻으려면 Medallia 게재 팀과 협력하십시오.

## 지원되는 ID {#supported-identities}

Medallia는 아래 표에 설명된 ID 활성화를 지원합니다. [ID](/help/identity-service/features/namespaces.md)에 대해 자세히 알아보세요.

| 대상 ID | 설명 | 고려 사항 |
|---|---|---|
| 이메일 | 이메일 주소 | 전자 메일 초대장 설문을 보내려면 전자 메일 대상 ID를 선택합니다. 프로필이 여러 이메일 주소와 연결된 경우 Medallia는 첫 번째 이메일에 대한 초대장만 트리거합니다. |
| 전화 | E.164 포맷으로 해시된 전화번호 | SMS 기반 설문 조사를 전송하려면 전화 대상 ID를 선택합니다. 전화번호는 플러스 기호(+), 국제 국가 전화 코드, 지역 번호 및 전화번호가 포함된 E.164 형식이어야 합니다. 예: (+)(국가 코드)(지역 코드)(전화 번호). 프로필이 여러 전화번호와 연결된 경우 Medallia는 첫 번째 전화번호에 대한 초대만 트리거합니다. |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | [대상 활성화 워크플로](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes)의 프로필 특성 선택 화면에서 선택한 대로 원하는 스키마 필드(예: 이메일 주소, 전화번호, 성)와 함께 새로 자격을 갖춘 모든 구성원을 내보내고 있습니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

대상에 인증하려면 필수 필드를 입력한 다음 **[!UICONTROL 대상에 연결]**&#x200B;을(를) 선택하십시오.

* **[!UICONTROL OAuth 토큰 끝점 URL]**: 일반적으로 https://instance.medallia.tld/oauth/tenant/token 형식을 사용합니다.
* **[!UICONTROL 클라이언트 ID]**: Medallia 배달 팀에서 가져옵니다.
* **[!UICONTROL 클라이언트 암호]**: Medallia 배달 팀에서 가져옵니다.

![이 대상에 대한 인증 화면을 표시하는 이미지입니다.](/help/destinations/assets/catalog/voice/medallia-destination-oauth.png)

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL API 게이트웨이 URL]**: Medallia 배달 팀에서 가져옵니다. 일반적으로 https://instance-tenant.apis.medallia.com 형식을 사용합니다.
* **[!UICONTROL API 이름 가져오기]**: Medallia 배달 팀에서 가져옵니다. 이 연결에 사용할 Medallia 가져오기 API(웹 피드라고도 함)의 이름입니다. 서로 다른 대상을 서로 다른 가져오기 API로 활성화하여 서로 다른 설문 조사 프로그램을 트리거할 수 있습니다.

![이 대상에 대한 대상 세부 정보 화면을 표시하는 이미지.](/help/destinations/assets/catalog/voice/medallia-destination-details.png)

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 모두 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

이 대상으로 대상을 활성화하는 방법에 대한 지침은 [프로필 및 대상을 스트리밍 대상 내보내기 대상으로 활성화](/help/destinations/ui/activate-segment-streaming-destinations.md)를 참조하십시오.

### 속성 및 ID 매핑 {#map}

사용 사례에 따라 다음 대상 ID 네임스페이스를 매핑해야 합니다.
* 전자 메일 기반 설문 조사의 경우 **전자 메일**&#x200B;은(는) **대상 필드** > **ID 네임스페이스 선택** > **전자 메일**&#x200B;을(를) 사용하여 대상 필드로 매핑되어야 합니다.
* SMS 기반 설문 조사의 경우 **phone**&#x200B;은(는) **대상 필드** > **ID 네임스페이스 선택** > **phone**&#x200B;을(를) 사용하여 대상 필드로 매핑되어야 합니다. 전화번호는 플러스 기호(+), 국제 국가 전화 코드, 지역 번호 및 전화 번호를 포함하는 E.164 형식이어야 합니다

또한 추가적인 target 사용자 지정 특성을 매핑하여 개인화된 설문 조사를 만들고 고객에 대한 추가 정보를 설문 조사 레코드에 추가하는 것이 좋습니다.

* 개인화된 설문 조사는 일반적으로 고객의 이름을 기준으로 합니다
   * 고객의 이름을 **대상 필드** > **사용자 지정 특성 선택** > **특성 이름** > **이름**&#x200B;에 매핑합니다.
   * 고객의 성을 **대상 필드** > **사용자 지정 특성 선택** > **특성 이름** > **성**&#x200B;에 매핑합니다.
* 원하는 대로 다른 타겟 사용자 지정 속성에 대한 매핑을 추가합니다

![ID 및 특성에 대한 샘플 매핑을 보여 주는 이미지입니다.](/help/destinations/assets/catalog/voice/medallia-destination-mapping.png)

>[!IMPORTANT]
> 
> **대상 필드** > **사용자 지정 특성 선택** > **특성 이름**&#x200B;을 사용하여 매핑하는 모든 대상 사용자 지정 특성에 대해 정확한 **특성 이름**&#x200B;을(를) Medallia 배달 팀과 공유합니다. 직접 공유할 매핑 페이지의 스크린샷을 캡처할 수 있습니다.

## 내보낸 데이터 {#exported-data}

대상으로 세그먼트를 활성화하면 Adobe Experience Platform에서 Medallia로 내보낸 데이터의 유효성을 검사할 수 있는 Medallia 제공 팀에 알립니다. 성공적인 데이터 확인 후에만 Medallia 내에서만 설문 조사를 활성화할 수 있습니다. 이 전에 데이터가 Medallia로 내보내지지만 고객에게 설문 조사가 트리거되지 않습니다.

내보내진 데이터의 샘플 JSON이 아래에 제공됩니다. 이 예제 매핑은 **특성 및 ID 매핑** 섹션에서 위의 스크린샷의 매핑을 사용합니다.

```json
[
    {
        "profile_raw_encoded": "eyJhdHRyaWJ1dGVzIjp7ImZpcnN",
        "email": "johnsmith@example.com",
        "aep_segments_new": ["c1c3edcc-07cb-4f66-b5dd-aff485148aba"],
        "aep_segments_existing": [],
        "aep_segments_removed": [],
        "firstname":  "John" ,
        "lastname":  "Smith",
        "contactId": "jsmith120002",
    }
]
```

## 데이터 사용 및 관리 {#data-usage-governance}

데이터를 처리할 때 모든 [!DNL Adobe Experience Platform] 대상이 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](/help/data-governance/home.md)를 참조하십시오.
