---
title: (베타) Experience Cloud 대상
description: Experience Platform에서 다양한 Experience Platform 솔루션으로 세그먼트를 공유하는 방법을 알아봅니다.
last-substantial-update: 2023-01-25T00:00:00Z
source-git-commit: 32222aa1c96537b51cd0db35d9cdabce9210f64a
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 2%

---


# (베타) [!UICONTROL Experience Cloud 대상] 연결

이 대상을 사용하면 Experience Platform에서 Audience Manager, Analytics, Advertising Cloud, Adobe Campaign, Target 또는 Marketo과 같은 다양한 Experience Cloud 솔루션으로 세그먼트를 공유할 수 있습니다.

![대상 카탈로그에서 강조 표시된 Experience Cloud 대상 대상입니다.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-destination-catalog.png)

>[!IMPORTANT]
>
>* 이 대상은 을 대체합니다 [이전 세그먼트 공유 통합](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-in-aam) Experience Platform에서 다양한 Experience Cloud 솔루션에 이르기까지
>* 이 대상은 현재 베타 버전입니다. 설명서 및 기능은 변경될 수 있습니다.


## 사용 사례 및 이점 {#use-cases}

를 사용하는 방법과 시기를 더 잘 이해할 수 있도록 하기 위해 [!UICONTROL Experience Cloud 대상] 대상, Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례는 다음과 같습니다.

### 데이터 관리 플랫폼 사용 사례 활성화 {#dmp-use-cases}

Audience Manager에서 다음과 같은 데이터 관리 플랫폼 사용 사례에 Experience Platform 세그먼트를 사용할 수 있습니다.

* 추가 [타사 데이터](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-types-collected.html?lang=en#third-party-data) 세그먼트를 보거나 편집하거나 삭제할 수 있습니다.
* [알고리즘 모델링](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/algorithmic-models/look-alike-modeling/understanding-models.html?lang=en);
* Experience Platform 대상 카탈로그에서 아직 지원되지 않는 쿠키 기반 대상으로 세그먼트를 활성화합니다.

### 내보낸 세그먼트를 세부적으로 제어 {#segments-control}

Experience Cloud 대상 대상을 통해 새로운 셀프 서비스 세그먼트 공유 통합을 사용하여 Audience Manager 및 그 이상으로 내보낼 세그먼트를 선택합니다. 이렇게 하면 다른 Experience Cloud 솔루션과 공유할 세그먼트와 Experience Platform에만 유지할 세그먼트를 결정할 수 있습니다.

기존 세그먼트 공유 통합에서는 세그먼트를 Audience Manager 이상으로 내보내야 하는 세그먼트를 세부적으로 제어할 수 없었습니다.

### 추가 Experience Cloud 솔루션과 Experience Platform 세그먼트 공유 {#share-segments-with-other-solutions}

Experience Platform 대상 카드를 사용하면 Audience Manager과 세그먼트를 공유하는 것 외에도 다음과 같이 프로비저닝된 다른 Experience Cloud 솔루션과 세그먼트를 공유할 수 있습니다.

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
> * 이 대상은 다음 작업을 수행할 수 있습니다. [Adobe Real-time Customer Data Platform Prime 및 Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) 고객.
> * 을(를) 활성화하려면 Audience Manager 라이센스가 필요합니다 [데이터 관리 플랫폼 활용 사례](#dmp-use-cases) 위에 자세히 언급되어 있습니다.
> * 사용자 *필요 없음* Experience Platform 세그먼트를 Adobe Advertising Cloud, Adobe Target, Marketo 및 기타 Experience Cloud 솔루션과 공유할 수 있는 Audience Manager 라이선스( [위의 섹션](#share-segments-with-other-solutions).


### 기존 세그먼트 공유 솔루션을 사용하는 고객의 경우

이미 세그먼트를 Experience Platform에서 Audience Manager 및 을 통해 기타 Experience Cloud 솔루션으로 공유하는 경우 [이전 세그먼트 공유 통합](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-in-aam)로 지정하는 경우 고객 지원 센터 또는 고객 성공 관리자에게 문의하여 이전 통합을 비활성화해야 합니다. 고객 지원 및 고객 지원 관리 팀은 통합을 비활성화하려면 Jira 티켓을 파일(템플릿 티켓 AAM-52354 참조)해야 합니다.

베타 고객의 프로비저닝 해제 티켓을 해결하는 데 걸리는 시간은 영업일 기준으로 6일 이하입니다. 기존 레거시 통합이 비활성화된 후 다음을 진행할 수 있습니다 [연결 만들기](#connect) 셀프 서비스 대상 카드를 통해

>[!IMPORTANT]
>
>Experience Platform에서 다른 솔루션으로의 세그먼트 내보내기는 Jira 티켓 확인과 대상 카드를 통해 새 연결이 설정되는 시간 사이에 중지됩니다. Jira 티켓이 닫히는 즉시 대상 카드를 통해 연결을 만들어 이 다운타임을 최소화할 수 있습니다.

## 알려진 제한 사항 및 콜아웃 {#known-limitations}

Experience Cloud 대상 카드의 베타 릴리스에서 다음의 알려진 제한 사항 및 중요 콜아웃을 참조하십시오.

* [데이터 흐름 모니터링](/help/dataflows/ui/monitor-destinations.md) 은 지원되지 않습니다.
* 대상에 연결할 때 [데이터 흐름 경고 사용](#enable-alerts). UI에 표시되지만, **경고 사용 옵션이 지원되지 않습니다.** 베타 릴리스에서 사용.
* **채우기 작업은 지원되지 않습니다**. Audience Manager 또는 기타 Experience Cloud 솔루션으로 처음 내보내는 세그먼트에는 세그먼트의 내역 모집단이 포함되지 않습니다.
* 베타 릴리스에서는 **Experience Cloud 대상 대상에 대한 단일 대상 연결** Experience Platform 조직에 속한 모든 샌드박스에서 제외합니다.
* 다음 항목이 있습니다 **4시간 지연** Experience Platform에서 데이터가 활성화되는 시간과 Audience Manager 및 기타 Experience Cloud 솔루션에서 데이터를 사용할 준비가 된 시간 사이에.

## 지원되는 ID {#supported-identities}

로 내보내는 프로필 [!UICONTROL Experience Cloud 대상] 대상은 아래 표에 설명된 ID에 매핑됩니다. 추가 정보 [id](/help/identity-service/namespaces.md).

| Target ID | 설명 | 고려 사항 |
|---|---|---|
| ECID | Experience Cloud ID | ECID를 나타내는 네임스페이스입니다. 이 네임스페이스를 다음 별칭으로 참조할 수도 있습니다. &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. 다음 문서를 참조하십시오. [ECID](/help/identity-service/ecid.md) 추가 정보. |
| GAID | Google 광고 ID | GAID(Google Advertising ID)의 기본 ID를 사용하여 Experience Platform에 수집된 프로필을 이 대상으로 내보낼 수 있습니다. |
| IDFA | 광고주용 Apple ID | IDFA(광고주용 Apple ID)의 기본 ID를 사용하여 Experience Platform에 수집된 프로필을 이 대상으로 내보낼 수 있습니다. |
| email_lc_sha256 | SHA256 알고리즘을 사용하여 해시된 이메일 주소 | 해시된 이메일 주소의 기본 ID를 사용하여 Experience Platform에 수집된 프로필을 이 대상으로 내보낼 수 있습니다. |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
|---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 세그먼트 내보내기]** | 위의 섹션에 나열된 ID를 키로 사용하는 세그먼트(대상)의 모든 구성원을 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상 설정&quot; API 기반 연결입니다. 세그먼트 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터는 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로우에서 아래 두 섹션에 나열된 필드를 채웁니다.

>[!IMPORTANT]
> 
>베타 릴리스에서는 Experience Platform 조직에 속한 모든 샌드박스에서 Experience Cloud 대상 대상에 단일 대상 연결을 만들 수 있습니다.

### 대상에 인증 {#authenticate}

대상을 인증하려면 **[!UICONTROL 설정]** 카탈로그의 대상 카드 보기에서 을(를) 선택하고 **[!UICONTROL 대상에 연결]**.

![Experience Cloud 대상 대상에 대한 대상에 연결 옵션 보기](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/experience-cloud-audiences-authenticate-to-destination.png)

### 대상 세부 사항 채우기 {#destination-details}

대상에 대한 세부 사항을 구성하려면 아래 필수 및 선택적 필드를 입력합니다. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

![Experience Cloud 대상 대상에 연결할 필수 및 선택적 설정을 보여주는 새 대상 화면을 구성합니다.](/help/destinations/assets/catalog/adobe/experience-cloud-audiences/connect-to-destination.png)

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식하는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.

<!--

Commenting this part out for the duration of the beta program

### Enable alerts {#enable-alerts}

You can enable alerts to receive notifications on the status of the dataflow to your destination. Select an alert from the list to subscribe to receive notifications on the status of your dataflow. For more information on alerts, see the guide on [subscribing to destinations alerts using the UI](../../ui/alerts.md).
-->

대상 연결에 대한 세부 정보 제공을 마치면 를 선택합니다 **[!UICONTROL 다음]**.


## 세그먼트를 이 대상에 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

읽기 [스트리밍 세그먼트 내보내기 대상으로 프로필 및 세그먼트를 활성화합니다](/help/destinations/ui/activate-segment-streaming-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다. 아니요 [매핑 단계](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) 필수 사항이며 아니요 [예약 단계](/help/destinations/ui/activate-segment-streaming-destinations.md#scheduling) 이 이 대상에 사용할 수 있습니다.

## 데이터 내보내기의 유효성 검사 {#exported-data}

성공적인 데이터 내보내기의 유효성을 검사하기 위해 세그먼트가 원하는 Experience Cloud 솔루션에 성공했는지 확인할 수 있습니다.

### Audience Manager에서 데이터 유효성 검사

Experience Platform 세그먼트가 Audience Manager에 [신호](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-signals), [트레이트](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-traits), 및 [세그먼트](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html?lang=en#aep-segments-as-aam-segments). 데이터가 위의 설명서 링크에 설명된 대로 표시되었는지 Audience Manager에서 확인할 수 있습니다.

## 데이터 사용 및 거버넌스 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스 적용, 읽기 [데이터 거버넌스 개요](/help/data-governance/home.md).

Experience Platform의 데이터 거버넌스는 둘 다에 의해 시행됩니다 [데이터 사용 레이블](/help/data-governance/labels/reference.md) 및 마케팅 작업을 수행할 수 있습니다.
데이터 사용량 레이블은 애플리케이션으로 전송되지만 마케팅 작업은 수행되지 않습니다. 즉, Experience Platform이 Audience Manager에 도달하면의 세그먼트를 사용 가능한 모든 대상으로 내보낼 수 있습니다. Audience Manager에서 [데이터 내보내기 제어](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html?lang=en) 세그먼트를 특정 대상으로 내보내지 못하도록 차단합니다.

### Audience Manager의 권한 관리

Audience Manager의 세그먼트와 트레이트는 [역할 기반 액세스 제어](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/administration/administration-overview.html?lang=en) (RBAC).

Experience Platform에서 내보낸 세그먼트는 라는 Audience Manager의 특정 데이터 소스에 할당됩니다. **[!UICONTROL Experience Platform 세그먼트]**.

특정 사용자만 세그먼트에 액세스할 수 있도록 하기 위해 데이터 소스에 속하는 세그먼트에 액세스 제어를 적용할 수 있습니다. Experience Platform 세그먼트에서 만든 이러한 세그먼트 및 트레이트에 대해 Audience Manager에서 새 액세스 제어 권한을 설정해야 합니다.