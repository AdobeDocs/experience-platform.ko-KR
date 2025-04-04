---
title: Adobe Campaign Managed Cloud Services 연결
description: Adobe Campaign Managed Cloud Services은 크로스채널 고객 경험을 디자인할 수 있는 플랫폼과 시각적 캠페인 오케스트레이션, 실시간 상호 작용 관리 및 크로스채널 실행 환경을 제공합니다.
exl-id: fe151ad3-c431-4b5a-b453-9d1d9aedf775
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1633'
ht-degree: 2%

---

# Adobe Campaign Managed Cloud Services 연결 {#adobe-campaign-managed-services}

>[!IMPORTANT]
>
>이 통합은 [Adobe Campaign 버전 8.4 이상](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/release-notes.html#release-8-4-1)에서 작동합니다.

## 개요 {#overview}

Adobe Campaign Managed Cloud Services은 크로스채널 고객 경험을 디자인할 수 있는 플랫폼과 시각적 캠페인 오케스트레이션, 실시간 상호 작용 관리 및 크로스채널 실행 환경을 제공합니다. [Campaign 시작](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html)

Campaign을 사용하여 다음과 같은 작업을 수행할 수 있습니다.

* 고객에 대한 접근성 높은 단일 관점을 통해 개인화 및 참여 촉진
* 이메일, 모바일, 온라인 및 오프라인 채널을 고객 여정에 통합,
* 의미 있고 시의적절한 메시지 및 오퍼 게재를 자동화합니다.

## 가드레일 {#guardrails}

Adobe Campaign Managed Cloud Services 연결을 사용할 때는 다음 보호 기능에 유의하십시오.

* 이 대상에 대해 최대 25개의 대상을 [활성화](#activate)할 수 있습니다.

  Campaign 탐색기의 **[!UICONTROL 관리]** > **[!UICONTROL 플랫폼]** > **[!UICONTROL 옵션]** 폴더에서 **NmsCdp_Aep_Audience_List_Limit** 옵션의 값을 업데이트하여 이 제한을 변경할 수 있습니다.

* 각 대상에 대해 Adobe Campaign에 [맵](#map)에 최대 20개의 필드를 추가할 수 있습니다.

  Campaign 탐색기의 **[!UICONTROL 관리]** > **[!UICONTROL 플랫폼]** > **[!UICONTROL 옵션]** 폴더에서 **NmsCdp_Aep_Destinations_Max_Columns** 옵션 값을 업데이트하여 이 제한을 변경할 수 있습니다.

* Azure Blob 스토리지 DLZ(데이터 랜딩 영역)의 데이터 유지 : 7일.
* 활성화 빈도는 최소 3시간입니다.
* 이 연결에서 지원되는 최대 파일 이름 길이는 255자입니다. [내보낸 파일 이름을 구성](../../ui/activate-batch-profile-destinations.md#configure-file-names)할 때 파일 이름이 255자를 초과하지 않는지 확인하십시오. 최대 파일 이름 길이를 초과하면 활성화 오류가 발생합니다.

## 사용 사례 {#use-cases}

Adobe Campaign Manage Service 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례를 소개합니다.

* Adobe Experience Platform은 id 그래프, analytics의 행동 데이터, 오프라인 및 온라인 데이터 병합 등과 같은 정보를 통합하는 고객 프로필을 만듭니다. 이 통합을 통해 해당 Adobe Experience Platform 기반 대상을 사용하여 Adobe Campaign 내에 이미 존재하는 세분화 기능을 강화할 수 있으므로 Campaign에서 해당 데이터를 활성화할 수 있습니다.

  예를 들어 스포츠 의류 회사는 Adobe Experience Platform에서 제공하는 대상자를 활용하고 Adobe Campaign을 사용하여 활성화함으로써 Adobe Campaign에서 지원하는 다양한 채널에서 해당 고객 기반에 연결하려고 합니다. 메시지가 전송되면 전송, 열기 및 클릭 수와 같은 Adobe Campaign의 경험 데이터로 Adobe Experience Platform의 고객 프로필을 개선하려고 합니다.

  그 결과, Adobe Experience Cloud 생태계 전반에서 보다 일관적인 크로스 채널 캠페인과 다양한 고객 프로필이 적용되어 빠르게 학습할 수 있습니다.


* Campaign의 대상 활성화 외에도 Adobe Campaign Managed Services 대상을 활용하여 Adobe Experience Platform의 프로필에 연결된 추가 프로필 속성을 가져오고 동기화 프로세스를 통해 Adobe Campaign 데이터베이스에서 업데이트되도록 할 수 있습니다.

  예를 들어 Adobe Experience Platform에서 옵트인 및 옵트아웃 값을 캡처한다고 가정해 보겠습니다. 이 연결을 사용하면 이러한 값을 Adobe Campaign으로 가져오고 정기적으로 업데이트되도록 동기화 프로세스를 유지할 수 있습니다.

  >[!NOTE]
  >
  >프로필 속성 동기화는 Adobe Campaign 데이터베이스에 이미 있는 프로필에 사용할 수 있습니다.

[Adobe Experience Platform과의 Adobe Campaign 통합에 대해 자세히 알아보기](https://experienceleague.adobe.com/docs/campaign/campaign-v8/connect/ac-aep.html)

## 지원되는 ID {#supported-identities}

*Adobe Campaign Managed Cloud Services*&#x200B;에서는 아래 표에 설명된 ID 활성화를 지원합니다. [ID](/help/identity-service/features/namespaces.md)에 대해 자세히 알아보세요.

| 대상 ID | 설명 | 고려 사항 |
|---|---|---|
| external_id | 사용자 지정 사용자 ID | 소스 ID가 사용자 지정 네임스페이스인 경우 이 대상 ID를 선택합니다. 이 ID를 사용하여 고객을 나타내는 Campaign 인스턴스의 ID(loyalty_ID, account_ID, customer_ID...)에 매핑하는 것이 좋습니다. |
| ECID | Experience Cloud ID | ECID를 나타내는 네임스페이스입니다. 이 네임스페이스는 &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot; 별칭으로도 참조할 수 있습니다. 자세한 내용은 [ECID](/help/identity-service/features/ecid.md)에서 다음 문서를 참조하십시오. |
| email_lc_sha256 | SHA256 알고리즘으로 해시된 이메일 주소 | Adobe Experience Platform은 일반 텍스트와 SHA256 해시 이메일 주소를 모두 지원합니다. 소스 필드에 해시되지 않은 특성이 포함된 경우 **[!UICONTROL 변환 적용]** 옵션을 선택하여 [!DNL Experience Platform]이(가) 활성화 시 데이터를 자동으로 해시하도록 하십시오. |
| phone_sha256 | SHA256 알고리즘으로 해시된 전화번호 | 일반 텍스트와 SHA256 해시 전화 번호는 모두 Adobe Experience Platform에서 지원됩니다. 소스 필드에 해시되지 않은 특성이 포함된 경우 **[!UICONTROL 변환 적용]** 옵션을 선택하여 [!DNL Experience Platform]이(가) 활성화 시 데이터를 자동으로 해시하도록 하십시오. |
| GAID | GOOGLE ADVERTISING ID | 소스 ID가 GAID 네임스페이스인 경우 GAID 대상 ID를 선택합니다. |
| IDFA | 광고주용 Apple ID | 소스 ID가 IDFA 네임스페이스인 경우 IDFA 대상 ID를 선택합니다. |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | [대상 활성화 워크플로](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes)의 프로필 특성 선택 화면에서 선택한 대로 원하는 스키마 필드(예: 이메일 주소, 전화번호, 성)와 함께 대상자의 모든 구성원을 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL 일괄 처리]** | 배치 대상은 파일을 3, 6, 8, 12 또는 24시간 단위로 다운스트림 플랫폼으로 내보냅니다. [일괄 파일 기반 대상](/help/destinations/destination-types.md#file-based)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/destination-details.png)

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 인스턴스 선택]**: **[!DNL Campaign]** 마케팅 인스턴스.
* **[!UICONTROL 대상 매핑]**: **[!DNL Adobe Campaign]**&#x200B;에서 게재를 보낼 대상 매핑을 선택하십시오. [자세히 알아보기](https://experienceleague.adobe.com/docs/campaign/campaign-v8/profiles-and-audiences/add-profiles/target-mappings.html).
* **[!UICONTROL 동기화 유형 선택]**:

   * **[!UICONTROL 대상 동기화]**: 이 옵션을 사용하여 Adobe Experience Platform 대상을 Adobe Campaign으로 보낼 수 있습니다.
   * **[!UICONTROL 프로필 동기화(업데이트만 해당)]**: 이 옵션을 사용하여 Adobe Experience Platform 프로필 특성을 Adobe Campaign으로 가져오고 정기적으로 업데이트할 수 있도록 동기화 프로세스를 준비하십시오.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 모두 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

### 거버넌스 정책 및 시행 작업 {#governance}

대상으로 내보낼 데이터에 적용할 수 있는 마케팅 작업을 선택합니다. Adobe Campaign의 경우 **[!UICONTROL 이메일 타겟팅]** 마케팅 액션을 선택하는 것이 좋습니다.

마케팅 액션에 대한 자세한 내용은 [데이터 사용 정책 개요](/help/data-governance/policies/overview.md) 페이지를 참조하세요.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

대상 데이터를 이 대상으로 활성화하는 방법에 대한 지침은 [대상 데이터를 일괄 프로필 내보내기 대상으로 활성화](https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html)를 참조하십시오.

### 속성 및 ID 매핑 {#map}

프로필로 내보낼 XDM 필드를 선택하고 해당 Adobe Campaign 필드에 매핑합니다.[이메일 마케팅 대상의 ID 및 특성 선택에 대해 자세히 알아보기](overview.md)

1. 소스 필드 선택:

   * Adobe Experience Platform 및 Adobe Campaign에서 프로필을 고유하게 식별하는 소스 ID로 **식별자**(예: 이메일 필드)을(를) 선택합니다.

   * Adobe Campaign으로 내보내야 하는 다른 모든 **XDM 소스 프로필 특성**&#x200B;을 선택합니다.

   >[!NOTE]
   >
   >segmentMembershipStatus 필드는 segmentMembership 상태를 반영하는 필수 매핑입니다. 이 필드는 기본적으로 추가되며 수정하거나 제거할 수 없습니다.

1. 각 필드를 Adobe Campaign의 대상 필드와 매핑합니다. 사용 가능한 대상 필드는 [대상을 만들 때](#destination-details) 선택한 대상 매핑에 의해 결정됩니다.

1. 필수 속성 및 중복 제거 키를 식별합니다. &quot;필수&quot; 또는 &quot;중복 제거 키&quot;로 표시된 특성의 값은 null일 수 없습니다.

   * [필수 특성](../../ui/activate-batch-profile-destinations.md#mandatory-attributes) 모든 프로필 레코드에 선택한 특성이 포함되어 있는지 확인합니다. 예를 들어 내보낸 모든 프로필에는 이메일 주소가 들어 있습니다. 권장 사항은 ID 필드와 중복 제거 키로 사용되는 필드 모두를 필수로 설정하는 것입니다.
   * [중복 제거 키](../../ui/activate-batch-profile-destinations.md#mandatory-attributes)는 사용자가 프로필을 중복 제거할 ID를 결정하는 기본 키입니다.

     >[!IMPORTANT]
     >
     >중복 제거 키 속성의 이름이 선택한 대상 매핑의 열 이름과 일치하는지 확인합니다.

   ![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/mapping.png)

1. 매핑이 수행되면 대상 구성을 검토하고 완료하여 **[!DNL Campaign]**에 데이터를 보낼 수 있습니다.
   [대상 구성을 검토하고 완료하는 방법을 알아보세요](/help/destinations/destination-types.md#review).

## 내보낸 데이터/데이터 내보내기 유효성 검사 {#exported-data}

대상이 활성화되면 Campaign에서 해당 작업 및 내보낸 데이터에 액세스할 수 있습니다.

### 데이터 내보내기 작업 모니터링 {#jobs}

**[!UICONTROL 관리]** > **[!UICONTROL 감사]** > **[!UICONTROL 대상자 로드 작업]** 메뉴로 이동하여 Adobe Experience Platform에서 활성화된 모든 내보내기 작업을 모니터링합니다.

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-jobs.png)

### 내보낸 데이터 액세스 {#data}

**[!UICONTROL 대상 동기화]**&#x200B;의 경우 **[!UICONTROL 프로필 및 대상]** > **[!UICONTROL 목록]** > **[!UICONTROL AEP 대상]** 메뉴로 이동하여 내보낸 대상을 확인할 수 있습니다.

![](../../assets/catalog/email-marketing/adobe-campaign-managed-services/campaign-audiences.png)

**[!UICONTROL 프로필 동기화(업데이트만 해당)]**&#x200B;의 경우 대상에서 활성화된 대상자가 타겟팅한 각 프로필에 대해 Campaign 데이터베이스에 데이터가 자동으로 업데이트됩니다.

## 데이터 사용 및 관리 {#data-usage-governance}

데이터를 처리할 때 모든 [!DNL Adobe Experience Platform] 대상이 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](/help/data-governance/home.md)를 참조하십시오.
