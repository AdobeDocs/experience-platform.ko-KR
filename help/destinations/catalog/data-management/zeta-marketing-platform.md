---
title: Zeta 마케팅 플랫폼
description: ZMP(Zeta Marketing Platform)는 인텔리전스(독점 데이터 및 AI)를 기반으로 고객을 보다 효율적으로 확보, 성장 및 유지할 수 있도록 지원하는 클라우드 기반 시스템입니다.
hide: true
hidefromtoc: true
source-git-commit: bf553371316d9d9cb368fc4d1be14196201ef680
workflow-type: tm+mt
source-wordcount: '1352'
ht-degree: 1%

---


# Zeta 마케팅 플랫폼 {#zeta-marketing-platform}

## 개요 {#overview}

ZMP(Zeta Marketing Platform)는 인텔리전스(독점 데이터 및 AI)를 기반으로 고객을 보다 효율적으로 확보, 성장 및 유지할 수 있도록 지원하는 클라우드 기반 시스템입니다. 자세한 내용은 다음을 참조하십시오. [제타 글로벌](https://zetaglobal.com/).

Adobe Experience Platform에서 사용할 수 있는 Zeta Marketing Platform 커넥터를 사용하면 Experience Platform에서 ZMP로 대상을 원활하게 동기화할 수 있습니다.

>[!IMPORTANT]
>
>대상 커넥터 및 설명서 페이지는 *제타 글로벌* 팀. 문의 사항이나 업데이트 요청은 다음 팀으로 문의하십시오. [연락처](https://zetaglobal.com/about/contact-us/).

## 사용 사례 {#use-cases}

### 대상 세그먼트 작성 {#use-case-build-audiences}

마케터는 고유한 대상 프로필을 작성하고, 가장 가치 있는 세그먼트를 식별하고, Zeta Marketing Platform이 지원하는 모든 디지털 채널에서 사용하려고 합니다. 소비자 프로필의 진정한 360 보기를 만들고 의미 있는 대상을 빌드하고 활성화하려고 합니다. Zeta Marketing Platform이 지원하는 채널에 대한 자세한 내용은 을 참조하십시오 [여기](https://zetaglobal.com/platform/integrations/).

### 광고가 있는 타겟 사용자 {#use-case-target-users}

광고주는 DSP(제타 Demand Side Platform)를 통해 특정 대상 내의 사용자를 타겟팅하는 것을 목표로 합니다. 이러한 사용자는 브랜드와 상호 작용합니다. Zeta DSP에 대한 자세한 내용을 보려면 [여기](https://knowledgebase.zetaglobal.com/programmatic-user-guide/).

## 전제 조건 {#prerequisites}

### Zeta Marketing Platform 사전 요구 사항

* Zeta Marketing Platform 대상에 대한 새 연결을 설정하기 전에 Zeta Marketing Platform 계정에 빈 고객 목록을 만들어야 합니다. 이러한 고객 목록 중 하나를 보낼 Adobe Experience Platform 대상을 받을 지정된 대상으로 선택해야 합니다. 지침에 따라 ZMP에서 빈 고객 목록을 만들 수 있습니다 [여기](https://knowledgebase.zetaglobal.com/zmp/creating-audiences#CreatingAudiences-CreatingaCustomerList).
* Adobe Experience Platform에서는 특정 ZMP 대상 인스턴스에 대해 여러 대상을 활성화할 수 있지만 각 ZMP 대상 인스턴스는 하나의 Experience Platform 대상만 수신해야 합니다. Experience Platform에서 여러 대상을 처리하려면 각 대상에 대해 추가 ZMP 대상 인스턴스를 생성하고 드롭다운에서 다른 고객 목록을 선택하십시오. 이 방법을 사용하면 대상 ZMP 대상을 덮어쓰지 않습니다. 다음을 참조하십시오 [대상 세부 정보 입력](#destination-details) 을 참조하십시오.
* 다음 자격 증명을 사용하여 대상을 구성합니다.
   * 사용자 이름: **api**
   * 암호: ZMP REST API 키. ZMP 계정에 로그인하고 로 이동하면 REST API 키를 찾을 수 있습니다. **설정** > **통합** > **키 및 앱** 섹션. 다음을 참조하십시오. [ZMP 설명서](https://knowledgebase.zetaglobal.com/zmp/integrations) 을 참조하십시오.

## 지원되는 ID {#supported-identities}

[!DNL Zeta Marketing Platform] 는 아래 표에 설명된 사용자 지정 사용자 ID의 활성화를 지원합니다. 자세한 내용은 [id](/help/identity-service/features/namespaces.md).

>[!IMPORTANT]
> Zeta Marketing Platform 대상을 사용하려면 소스 ID 네임스페이스를 ZMP에 매핑해야 합니다 `uid` 타겟 ID. 이렇게 하면 Zeta Marketing Platform이 각 프로필을 고유하게 구별할 수 있습니다.

| 대상 ID | 설명 | 고려 사항 | 참고 |
---------|----------|----------|----------|
| uid | ZMP가 고객 프로필을 구별하는 데 사용하는 고유 ID | 필수 | 다음을 선택합니다. `Email` 이메일 주소를 사용하여 고유 프로필을 식별하려는 경우 표준 id 네임스페이스. 또는 사용자 지정 네임스페이스를에 매핑하도록 선택할 수 있습니다. `uid` 고객 프로필에 이메일이 없는 경우. |
| email_md5_id | 각 고객 프로필을 나타내는 이메일 MD5 | 선택 사항입니다 | 이메일 MD5 값을 사용하여 고객 프로필을 고유하게 식별하려면 이 타겟 ID를 선택합니다. 플랫폼에서는 일반 텍스트를 MD5로 변환하지 않으므로 Experience Platform 내에서 이메일 주소가 이미 MD5 포맷이어야 합니다. 이 시나리오에서 을(를) 설정합니다. `uid` (필수) 동일한 이메일 MD5 값 또는 다른 적절한 ID 네임스페이스로 복제합니다. |

{style="table-layout:auto"}

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ 덧신 | Experience Platform을 통해 생성된 대상자 [세분화 서비스](../../../segmentation/home.md). |
| 사용자 정의 업로드 | X | 대상 [가져옴](../../../segmentation/ui/overview.md#import-audience) csv 파일에서 Experience Platform으로 변환했습니다. |

{style="table-layout:auto"}

>[!NOTE]
> 개별 구성원이 Platform 대상자에서 추가되거나 제거되면 대상 고객 목록이 그에 따라 동기화되도록 업데이트가 ZMP로 전송됩니다.

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. Experience Platform 평가를 기반으로 프로필이 세그먼트에서 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

이 대상에 연결하려면 다음과같이 하십시오. [대상 구성 자습서](../../ui/connect-destination.md). 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

대상에 인증하려면 필수 필드를 입력한 다음 을(를) 선택합니다. **[!UICONTROL 대상에 연결]**.

* **[!UICONTROL 사용자 이름]**: `api`
* **[!UICONTROL 암호]**: ZMP REST API 키. ZMP 계정에 로그인하고 로 이동하면 REST API 키를 찾을 수 있습니다. **설정** > **통합** > **키 및 앱** 섹션. 다음을 참조하십시오. [ZMP 설명서](https://knowledgebase.zetaglobal.com/zmp/integrations) 을 참조하십시오.

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

![ZMP 구성을 보여주는 이미지](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-configure-new-destination.png)
* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL ZMP 계정 사이트 ID]**: 내 ZMP **사이트 Id** 대상자를 보낼 위치입니다. 다음으로 이동하여 사이트 ID를 볼 수 있습니다. **설정** > **통합** > **키 및 앱** 섹션. 추가 정보를 찾을 수 있음 [여기](https://knowledgebase.zetaglobal.com/zmp/integrations).
* **[!UICONTROL ZMP 세그먼트]**: Platform 대상자로 업데이트하려는 ZMP 사이트 ID 계정의 고객 목록 세그먼트입니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 다음 안내서를 참조하십시오. [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보를 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.

## 이 대상에 대한 세그먼트 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.
>* 내보내려면 *id*, 다음이 필요합니다. **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). <br> ![워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다.](/help/destinations/assets/overview/export-identities-to-destination.png "워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다."){width="100" zoomable="yes"}

읽기 [프로필 및 세그먼트를 스트리밍 세그먼트 내보내기 대상으로 활성화](/help/destinations/ui/activate-segment-streaming-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침

### 속성 및 ID 매핑 {#map}

다음은 프로필을 로 내보낼 때 올바른 ID 매핑의 예입니다 [!DNL Zeta Marketing Platform].

소스 필드 선택:
* 소스 ID 네임스페이스(예: 사용자 지정 또는 표준) 선택 `Email`)를 사용하여 Adobe Experience Platform에서 프로필을 고유하게 식별하고 [!DNL Zeta Marketing Platform].
* 로 내보내고 에서 업데이트해야 하는 XDM 소스 프로필 속성을 선택합니다. [!DNL Zeta Marketing Platform].

대상 필드 선택:
* (필수) 선택 `uid` 소스 id 네임스페이스를 매핑하는 대상 id입니다.
* (선택 사항) 선택 `email_md5_id` 이메일 md5 값을 나타내는 소스 id 네임스페이스를 매핑한 대상 id입니다. 플랫폼에서 일반 텍스트를 MD5로 변환하지 않으므로 Experience Platform 내에서 이메일 주소가 이미 MD5 포맷이어야 합니다
* 필요한 경우 추가 대상 매핑을 선택합니다.

![ID 매핑](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-mapping-example.png)

## 내보낸 데이터/데이터 내보내기 유효성 검사 {#exported-data}

Experience Platform에서 Zeta Marketing Platform으로의 성공적인 대상자 활성화는 ZMP에서 대상 고객 목록을 업데이트합니다. 대상 고객 목록의 개수 및 샘플 프로필은 성공적으로 활성화된 ID의 수와 같습니다.

![ZMP의 고객 목록](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-customer-list-in-zmp.png)

Experience Platform에서 활성화된 각 대상 멤버도 아래에 표시됩니다. **대상** > **사람** ZMP에서 또한 다음을 볼 수 있습니다. **고객 목록** 아래 표시된 대로 단일 고객 보기에서 프로필이 속해 있는 세그먼트를 세그먼트화합니다.

![단일 고객 보기 ZMP](../../assets/catalog/data-management-platform/zeta-marketing-platform/zeta-single-customer-view-in-zmp.png)

## 데이터 사용 및 관리 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스 적용, 다음을 읽습니다. [데이터 거버넌스 개요](/help/data-governance/home.md).

## 추가 리소스 {#additional-resources}

* [제타 기술 자료](https://knowledgebase.zetaglobal.com/zmp/)
