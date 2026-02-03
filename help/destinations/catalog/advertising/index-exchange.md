---
title: 색인 교환
description: 색인 Exchange(색인)에 연결하고 데이터를 활성화하면 색인 UI에서 만들어진 거래로 대상 세그먼트를 타깃팅할 수 있습니다.
last-substantial-update: 2026-01-27T00:00:00Z
source-git-commit: 04d01b2deafb1b8f1b0c256f31475bb75989a2c4
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 2%

---


# [!DNL Index Exchange] {#index-exchange}

## 개요 {#overview}

[!DNL Index]은(는) 미디어 소유자가 모든 화면에서 콘텐츠의 가치를 극대화할 수 있도록 지원하는 글로벌 광고 공급측 플랫폼입니다. 20년 이상의 업계 리더십 덕분에 [!DNL Index]은(는) 세계 최대 브랜드와 프리미엄 경험 메이커를 연결하여 고품질의 소비자 경험을 제공합니다.

이 대상 커넥터를 사용하여 Adobe Experience Platform의 대상 세그먼트를 [!DNL Index Exchange]의 프로그래밍 방식 광고 플랫폼으로 직접 내보냅니다.

내보낸 대상 세그먼트는 미디어 소유자, 마켓 플레이스 파트너별로 거래를 타깃팅하는 데 사용하거나 마켓 플레이스 공급업체에서 게시자 및 큐레이터와 공유할 수 있습니다.

>[!IMPORTANT]
>
>대상 커넥터 및 문서 페이지는 [!DNL Index] 팀에서 만들고 유지 관리합니다. 질문이나 업데이트 요청은 [technical_am_marketplace@indexexchange.com](mailto:technical_am_marketplace@indexexchange.com)로 직접 문의하십시오.

## 사용 사례 {#use-cases}

[!DNL Index Exchange] 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 사용 사례를 소개합니다.

### 모바일, 웹 및 CTV 플랫폼에서 사용자 타겟팅 {#targeting-users}

다양한 식별자를 사용하여 Experience Platform에서 [!DNL Index]&#x200B;(으)로 대상을 모바일, 웹 및 CTV 플랫폼의 사용자를 타겟팅하기 위해 전송하려는 미디어 소유자, 마켓플레이스 파트너 또는 마켓플레이스 공급업체.

### 모바일, 웹 및 CTV 플랫폼에서 특정 콘텐츠 타겟팅 {#targeting-content}

특정 URL, 앱 번들 또는 콘텐츠 ID를 사용하여 모바일, 웹 및 CTV 플랫폼에서 특정 콘텐츠를 보는 대상 사용자에게 Experience Platform에서 [!DNL Index]&#x200B;(으)로 대상을 전송하려는 미디어 소유자, 마켓플레이스 파트너 또는 마켓플레이스 공급업체.

## 전제 조건 {#prerequisites}

이 대상을 사용할 때 추가 프로세스를 사용하여 대상 세그먼트를 [!DNL Index]에 등록해야 계정에 표시됩니다. 이 프로세스에 대한 도움이 필요하면 [!DNL Index Exchange] 계정 담당자에게 문의하세요.

## 지원되는 ID {#supported-identities}

[!DNL Index]은(는) 아래 표에 설명된 ID 활성화를 지원합니다. [ID](/help/identity-service/features/namespaces.md)에 대해 자세히 알아보세요.

[!DNL Index Exchange] 대상은 업로드당 하나의 ID 유형만 지원합니다. 대상 세부 정보를 구성할 때 적절한 식별자 유형을 지정해야 합니다(아래 [&quot;대상 세부 정보 채우기&quot;](#destination-details) 섹션 참조).

여러 ID 유형을 업로드하려면 각 ID 유형에 대해 [!DNL Index Exchange] 대상의 별도 인스턴스를 만드십시오.

| 대상 ID | 설명 | 고려 사항 |
| --- | --- | --- |
| GAID | GOOGLE ADVERTISING ID | 소스 ID가 GAID 네임스페이스인 경우 GAID를 대상 ID로 선택합니다. |
| IDFA | 광고주용 Apple ID | 소스 ID가 IDFA 네임스페이스인 경우 IDFA 대상 ID를 선택합니다. |
| Windows AID | Windows Advertising ID | 소스 ID가 Windows AID 네임스페이스인 경우 Windows AID 대상 ID를 선택합니다. |
| extern_id | 사용자 지정 사용자 ID | 소스 ID가 사용자 지정 네임스페이스인 경우 이 대상 ID를 선택합니다. |

{style="table-layout:auto"}

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
| --------- | ---------- | ---------- |
| [!DNL Segmentation Service] | ✓ | Experience Platform [세그먼테이션 서비스](../../../segmentation/home.md)를 통해 생성된 대상입니다. |
| 사용자 정의 업로드 | ✓ | CSV 파일에서 Experience Platform으로 대상 [가져옴](../../../segmentation/ui/overview.md#import-audience). |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
| --------- | ---------- | --------- | 
| 내보내기 유형 | **[!UICONTROL Segment export]** | [!DNL Index Exchange] 대상에 사용된 식별자(IDFA, GAID 또는 기타)로 세그먼트의 모든 멤버(대상)를 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL Batch]** | 3, 6, 8, 12 또는 24시간 간격으로 파일을 다운스트림 플랫폼으로 내보냅니다. [일괄 파일 기반 대상](/help/destinations/destination-types.md#file-based)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL View Destinations]** 및 **[!UICONTROL Manage Destinations]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

![대상 세부 정보](../../assets/catalog/advertising/index-exchange/destination-details.png)

* [!UICONTROL Name]: 나중에 이 대상을 인식할 수 있도록 이름을 입력하십시오.
* [!UICONTROL Description]: 나중에 이 대상을 식별하는 데 도움이 되는 설명을 입력하십시오.
* [!UICONTROL Identifier Type]: [!DNL Index]에 보내는 식별자와 일치하는 인덱스 제공 식별자 유형을 선택합니다. 아래의 지원되는 식별자 유형 표를 참조하십시오. 사용할 식별자 유형을 잘 모를 경우 [!DNL Index] 담당자에게 문의하십시오. 여러 식별자 유형을 보내려면 이 대상의 별도 인스턴스를 만듭니다.
* [!UICONTROL Account ID]: [!DNL Index] 계정 ID를 입력하십시오. 게시자 ID와 다릅니다. 사용할 ID를 잘 모를 경우 [!DNL Index] 담당자에게 문의하세요.

#### 지원되는 식별자 유형

| 식별자 유형 | 설명 |
|------------------ | ------------- |
| [!DNL appbundle] | 모바일 앱 번들 |
| [!DNL contentid] | 컨텐츠 ID |
| [!DNL deviceid] | 장치 ID(예: IDFA, GAID, WAID 등) |
| [!DNL ip] | IP 주소 |
| [!DNL postcode] | ZIP / 우편 번호 |
| [!DNL url] | 사이트 URL |
| [!DNL ppid_xxx] | PPID 식별자의 경우 [!DNL Index Exchange] 계정 담당자에게 지원을 요청하십시오. |

{style="table-layout:auto"}

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 이 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 하나 이상의 경고를 선택하여 데이터 흐름에 대한 상태 알림을 구독합니다. 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.
대상 연결에 대한 세부 정보를 제공했으면 **[!UICONTROL Next]**&#x200B;을(를) 선택합니다.

## 이 대상에 대한 세그먼트 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** 및 **[!UICONTROL View Segments]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL View Identity Graph]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침은 [대상 데이터를 일괄 프로필 내보내기 대상으로 활성화](/help/destinations/ui/activate-batch-profile-destinations.md)를 참조하십시오.

### 속성 및 ID 매핑 {#map}

소스 필드 선택:

* 식별자(일반적으로 IDFA 또는 사용자 지정 ID 네임스페이스와 같은 네임스페이스)를 선택합니다. 대상을 구성할 때 선택한 식별자 유형에 해당해야 합니다. 예를 들어 IDFA 식별자를 소스 필드로 사용하는 경우 대상이 &quot;deviceid&quot; 식별자 유형으로 설정되어야 합니다.

대상 필드 선택:

* 대상 필드의 이름은 무시되며 중요하지 않습니다. 대상은 전송되는 식별자 유형만 처리하며, 이것은 대상을 구성할 때 선택한 식별자 유형에 의해 결정됩니다.

![특성 및 ID 매핑](../../assets/catalog/advertising/index-exchange/identity-mapping.png)

### [!DNL Index]에 세그먼트 등록 {#register-segments}

대상으로 데이터를 활성화하기 전이나 후에 [!DNL Index] 담당자에게 문의하여 활성화하려는 세그먼트를 등록합니다. 담당자 는 이름, ID, 설명 및 가격(해당되는 경우)을 포함하여 추가 세그먼트 세부 정보를 등록하는 방법에 대한 지침을 제공합니다.

## 내보낸 데이터/데이터 내보내기 유효성 검사 {#exported-data}

등록이 완료되면 세그먼트를 [!DNL Index] 계정에서 타깃팅할 수 있습니다. 데이터가 올바르게 수신되는지 확인하려면 수신된 세그먼트 데이터의 볼륨에 대한 세부 정보를 제공할 수 있는 [!DNL Index] 담당자에게 문의하십시오.

## 데이터 사용 및 관리 {#data-usage-governance}

모든 Experience Platform 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. Experience Platform에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](/help/data-governance/home.md)를 참조하십시오.
