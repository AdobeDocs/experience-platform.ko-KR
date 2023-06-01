---
title: (베타) Experience Cloud 대상
description: Experience Platform에서 다양한 Experience Platform 솔루션으로 세그먼트를 공유하는 방법을 알아봅니다.
last-substantial-update: 2023-01-25T00:00:00Z
exl-id: 2bdbcda3-2efb-4a4e-9702-4fd9991e9461
source-git-commit: 017c8bbc19845c0f60040ba2995b5dd2b0299a8b
workflow-type: tm+mt
source-wordcount: '1576'
ht-degree: 2%

---

# (베타) [!UICONTROL Experience Cloud 대상] 연결

이 대상을 사용하면 Experience Platform에서 Audience Manager, Analytics, Advertising Cloud, Adobe Campaign, Target 또는 Marketo과 같은 다양한 Experience Cloud 솔루션으로 세그먼트를 공유할 수 있습니다.

![대상 카탈로그에서 강조 표시된 Experience Cloud 대상.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-destination-catalog.png)

>[!IMPORTANT]
>
>* 이 대상은 [이전 세그먼트 공유 통합](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-in-aam) Experience Platform에서 다양한 Experience Cloud 솔루션으로 마이그레이션되었습니다.
>* 이 대상은 현재 베타 버전입니다. 설명서 및 기능은 변경될 수 있습니다.


## 사용 사례 및 이점 {#use-cases}

을(를) 사용하는 방법과 시기를 더 잘 이해할 수 있도록 [!UICONTROL Experience Cloud 대상] 대상: 다음은 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례입니다.

### 데이터 관리 플랫폼 사용 사례 활성화 {#dmp-use-cases}

Audience Manager에서 다음과 같은 데이터 관리 플랫폼 사용 사례에 Experience Platform 세그먼트를 사용할 수 있습니다.

* 추가 [타사 데이터](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-types-collected.html?lang=en#third-party-data) 세그먼트 연결;
* [알고리즘 모델링](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/algorithmic-models/look-alike-modeling/understanding-models.html?lang=en);
* Experience Platform 대상 카탈로그에서 아직 지원되지 않는 쿠키 기반 대상에 대한 세그먼트를 활성화합니다.

### 내보낸 세그먼트에 대한 세분화된 제어 {#segments-control}

Experience Cloud 대상 대상을 통해 새로운 셀프서비스 세그먼트 공유 통합을 사용하여 Audience Manager 및 그 이상으로 내보낼 세그먼트를 선택합니다. 이렇게 하면 다른 Experience Cloud 솔루션과 공유할 세그먼트와 Experience Platform에 독점적으로 보관할 세그먼트를 결정할 수 있습니다.

기존 세그먼트 공유 통합에서는 Audience Manager 및 그 이상으로 내보낼 세그먼트를 세부적으로 제어할 수 없었습니다.

### 추가 Experience Cloud 솔루션과 Experience Platform 세그먼트 공유 {#share-segments-with-other-solutions}

Audience Manager과 세그먼트를 공유하는 것 외에도 Experience Platform 대상 카드를 사용하면 다음을 포함하여 프로비저닝된 다른 Experience Cloud 솔루션과 세그먼트를 공유할 수 있습니다.

* Adobe Campaign
* Adobe Target
* Advertising Cloud
* Analytics
* Marketo

<!--

Note: briefly talk about when to share segments to these destinations using the existing destination cards and when to share using the new Experience Cloud Audiences destination. 

-->

## 사전 요구 사항 {#prerequisites}

>[!IMPORTANT]
>
> * 이 대상은 다음 경우에 사용할 수 있습니다. [Adobe Real-time Customer Data Platform Prime 및 Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) 고객.
> * 을(를) 활성화하려면 Audience Manager 라이선스가 필요합니다. [데이터 관리 플랫폼 사용 사례](#dmp-use-cases) 위에서 더 언급했습니다.
> * 본인 *필요 없음* Adobe Advertising Cloud, Adobe Target, Marketo 및 기타 Experience Cloud 솔루션과 Experience Platform 세그먼트를 공유할 수 있는 Audience Manager 라이선스입니다. [위의 섹션](#share-segments-with-other-solutions).


### 기존 세그먼트 공유 솔루션을 사용하는 고객의 경우

를 통해 이미 Experience Platform에서 Audience Manager 및 기타 Experience Cloud 솔루션으로 세그먼트를 공유하고 있는 경우 [이전 세그먼트 공유 통합](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html#aep-segments-in-aam), 기존 통합을 비활성화하려면 고객 지원 센터 또는 Adobe 계정 팀에 문의해야 합니다. 통합을 비활성화하려면 고객 지원 센터 및 Adobe 계정 팀이 Jira 티켓을 제출해야 합니다(템플릿 티켓 AAM-52354 참조).

Beta 고객의 프로비저닝 취소 티켓을 해결하는 데 걸리는 시간은 영업일 기준으로 6일 이내입니다. 기존 레거시 통합을 비활성화한 후 다음 작업을 진행할 수 있습니다. [연결 만들기](#connect) 셀프서비스 대상 카드를 통해

>[!IMPORTANT]
>
>Experience Platform에서 다른 솔루션으로 세그먼트 내보내기는 Jira 티켓 확인과 대상 카드를 통해 새 연결이 설정되는 시간 사이에 중지됩니다. Jira 티켓이 종료되는 즉시 대상 카드를 통해 연결을 생성하여 이 가동 중지 시간을 최소화할 수 있습니다.

## 알려진 제한 사항 및 설명선 {#known-limitations}

Experience Cloud 대상 카드의 베타 릴리스에 있는 다음 알려진 제한 사항 및 중요 콜아웃을 참고하십시오.

* [데이터 흐름 모니터링](/help/dataflows/ui/monitor-destinations.md) 은(는) 지원되지 않습니다.
* 대상에 연결할 때 다음 옵션을 볼 수 있습니다. [데이터 흐름 경고 활성화](#enable-alerts). UI에 표시되지만 **경고 활성화 옵션은 지원되지 않습니다.** 를 참조하십시오.
* **다시 채우기는 지원되지 않습니다.**. Audience Manager 또는 기타 Experience Cloud 솔루션으로 첫 번째 내보내기에는 세그먼트의 과거 모집단이 포함되지 않습니다.
* 베타 릴리스에서 다음을 만들 수 있습니다. **Experience Cloud 대상 대상에 대한 단일 대상 연결**, Experience Platform 조직에 속한 모든 샌드박스 간에 매핑됩니다.

### 대상자를 활성화할 때 대기 시간 {#audience-activation-latency}

Experience Platform에서 대상이 처음 활성화되는 시간과 특정 사용 사례에 대한 Audience Manager 및 기타 Experience Cloud 솔루션에서 사용될 준비가 된 시간 사이에 4시간 지연이 있습니다.

모든 사용 사례에 대해 Audience Manager에서 대상을 완전히 사용할 수 있도록 하는 데 최대 24시간이 소요될 수 있으며, Experience Cloud 대상의 대상이 Audience Manager 보고서에 나타나도록 하는 데 최대 48시간이 걸릴 수 있습니다.

세그먼트 이름과 같은 메타데이터는 Experience Cloud 대상 대상으로 내보내기를 설정한 후 몇 분 안에 Audience Manager에서 사용할 수 있습니다.

## 지원되는 ID {#supported-identities}

로 내보내는 프로필 [!UICONTROL Experience Cloud 대상] 대상은 아래 표에 설명된 id에 매핑됩니다. 자세히 알아보기 [id](/help/identity-service/namespaces.md).

| TARGET ID | 설명 | 고려 사항 |
|---|---|---|
| ECID | Experience Cloud ID | ECID를 나타내는 네임스페이스입니다. 이 네임스페이스는 &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot; 별칭으로도 참조할 수 있습니다. 에 대한 다음 문서를 참조하십시오. [ECID](/help/identity-service/ecid.md) 추가 정보. |
| GAID | Google 광고 ID | 기본 ID(Google Advertising ID)를 사용하여 Experience Platform에 수집된 프로필을 이 대상으로 내보낼 수 있습니다. |
| IDFA | 광고주용 Apple ID | IDFA(Apple ID for Advertisers)의 기본 ID를 사용하여 Experience Platform에 수집된 프로필을 이 대상으로 내보낼 수 있습니다. |
| email_lc_sha256 | SHA256 알고리즘으로 해시된 이메일 주소 | 해시된 이메일 주소의 기본 ID를 사용하여 Experience Platform에 수집된 프로필을 이 대상으로 내보낼 수 있습니다. |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
|---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 세그먼트 내보내기]** | 위의 섹션에 나열된 ID를 키로 사용하는 세그먼트(대상자)의 모든 구성원을 내보내고 있습니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. Experience Platform 평가를 기반으로 프로필이 세그먼트에서 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

이 대상에 연결하려면 다음과같이 하십시오. [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

>[!IMPORTANT]
> 
>Beta 릴리스에서는 Experience Platform 조직에 속한 모든 샌드박스에서 Experience Cloud 대상 대상에 대한 단일 대상 연결을 만들 수 있습니다.

### 대상에 인증 {#authenticate}

대상에 인증하려면 다음을 선택합니다. **[!UICONTROL 설정]** 카탈로그의 대상 카드 보기에서 다음을 선택합니다. **[!UICONTROL 대상에 연결]**.

![Experience Cloud 대상 대상에 대한 대상에 연결 옵션 보기.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-authenticate-to-destination.png)

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

![Experience Cloud 대상 대상에 연결하는 데 필요한 설정과 선택 사항을 표시하는 새 대상 화면을 구성합니다.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/connect-to-destination.png)

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.

<!--

Commenting this part out for the duration of the beta program

### Enable alerts {#enable-alerts}

You can enable alerts to receive notifications on the status of the dataflow to your destination. Select an alert from the list to subscribe to receive notifications on the status of your dataflow. For more information on alerts, see the guide on [subscribing to destinations alerts using the UI](../../ui/alerts.md).
-->

대상 연결에 대한 세부 정보를 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.


## 이 대상에 대한 세그먼트 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

읽기 [프로필 및 세그먼트를 스트리밍 세그먼트 내보내기 대상으로 활성화](/help/destinations/ui/activate-segment-streaming-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침 아니요 [매핑 단계](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) 필수 및 아니요 [예약 단계](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 이 대상에 사용할 수 있습니다.

## 데이터 내보내기 유효성 검사 {#exported-data}

성공적인 데이터 내보내기의 유효성을 검사하려면 세그먼트가 원하는 Experience Cloud 솔루션에 성공적으로 통과했는지 확인할 수 있습니다.

### Audience Manager의 데이터 유효성 검사

Experience Platform 세그먼트는 Audience Manager에 다음과 같이 표시됩니다. [신호](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-signals), [트레이트](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-traits), 및 [세그먼트](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-segments). 위의 설명서 링크에 설명된 대로 데이터가 표시되었는지 Audience Manager에서 확인할 수 있습니다.

## 데이터 사용 및 관리 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스 적용, 다음을 읽습니다. [데이터 거버넌스 개요](/help/data-governance/home.md).

Experience Platform의 데이터 거버넌스는 두 가지 방법 모두에 의해 실행됩니다. [데이터 사용 레이블](/help/data-governance/labels/reference.md) 및 마케팅 액션.
데이터 사용 레이블은 애플리케이션으로 전송되지만 마케팅 액션은 전송되지 않습니다. 즉, 세그먼트가 Audience Manager에 도달하면 Experience Platform의 세그먼트를 사용 가능한 대상으로 내보낼 수 있습니다. Audience Manager에서 다음을 사용할 수 있습니다 [데이터 내보내기 제어](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html?lang=en) 세그먼트를 특정 대상으로 내보내지 못하도록 차단합니다.

### Audience Manager의 권한 관리

Audience Manager의 세그먼트 및 트레이트는 [역할 기반 액세스 제어](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html?lang=en) (RBAC).

Experience Platform에서 내보낸 세그먼트는 라는 Audience Manager의 특정 데이터 소스에 할당됩니다. **[!UICONTROL Experience Platform 세그먼트]**.

특정 사용자만 세그먼트에 액세스할 수 있도록 하려면 데이터 소스에 속하는 세그먼트에 액세스 제어를 적용할 수 있습니다. Experience Platform 세그먼트에서 만든 이러한 세그먼트 및 트레이트에 대해 Audience Manager에서 새 액세스 제어 권한을 설정해야 합니다.
