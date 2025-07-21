---
title: Snowflake 연결
description: 비공개 목록을 사용하여 Snowflake 계정으로 데이터를 내보냅니다.
hide: true
hidefromtoc: true
badgeBeta: label="Beta" type="Informative"
exl-id: 4a00e46a-dedb-4dd3-b496-b0f4185ea9b0
source-git-commit: dca3762169d2a469948ee7e877213697f4c444b6
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 6%

---

# Snowflake 연결 {#snowflake-destination}

>[!IMPORTANT]
>
>이 대상 커넥터는 Beta 버전으로 일부 고객만 사용할 수 있습니다. 액세스 권한을 요청하려면 Adobe 담당자에게 문의하십시오.

## 개요 {#overview}

Snowflake 대상 커넥터를 사용하여 Adobe의 Snowflake 인스턴스로 데이터를 내보낸 다음 Adobe이 [개인 목록](https://other-docs.snowflake.com/en/collaboration/collaboration-listings-about)을 통해 인스턴스와 공유합니다.

Snowflake 대상의 작동 방식과 Adobe과 Snowflake 간에 데이터가 전송되는 방법을 이해하려면 다음 섹션을 참조하십시오.

### Snowflake 데이터 공유 작동 방식 {#data-sharing}

이 대상은 [!DNL Snowflake] 데이터 공유를 사용합니다. 즉, 물리적으로 내보낸 데이터나 자신의 Snowflake 인스턴스로 전송된 데이터가 없습니다. 대신 Adobe은 Adobe의 Snowflake 환경 내에서 호스팅되는 라이브 테이블에 대한 읽기 전용 액세스 권한을 부여합니다. Snowflake 계정에서 직접 이 공유 테이블을 쿼리할 수 있지만 테이블을 소유하지는 않으며 지정된 보존 기간 이후에 수정하거나 유지할 수 없습니다. Adobe은 공유 테이블의 수명 주기와 구조를 완전히 관리합니다.

Adobe의 Snowflake 인스턴스에서 소유의 인스턴스로 데이터를 처음 공유할 때 Adobe의 비공개 목록을 수락하라는 메시지가 표시됩니다.

![Snowflake 개인 목록 수락 화면을 보여 주는 스크린샷](../../assets/catalog/cloud-storage/snowflake/snowflake-accept-listing.png)

### 데이터 유지 및 TTL(Time-to-Live) {#ttl}

이 통합을 통해 공유되는 모든 데이터의 고정 TTL(Time-to-Live)은 7일입니다. 마지막 내보내기 후 7일이 지나면 데이터 흐름이 여전히 활성 상태인지 여부에 관계없이 공유 테이블이 자동으로 만료되어 액세스할 수 없게 됩니다. 7일 이상 데이터를 유지해야 하는 경우 TTL이 만료되기 전에 콘텐츠를 자체 Snowflake 인스턴스에서 소유한 테이블로 복사해야 합니다.

### 대상자 업데이트 동작 {#audience-update-behavior}

대상을 [일괄 처리 모드](../../../segmentation/methods/batch-segmentation.md)에서 평가하면 공유 테이블의 데이터가 24시간마다 새로 고쳐집니다. 즉, 대상 멤버십의 변경 사항과 이러한 변경 사항이 공유 테이블에 반영되는 시간 사이에 최대 24시간이 지연될 수 있습니다.

### 증분 내보내기 논리 {#incremental-export}

대상에 대해 데이터 흐름이 처음 실행되면 다시 채우기를 수행하고 현재 자격이 있는 모든 프로필을 공유합니다. 이 초기 채우기 이후에는 증분 업데이트만 공유 테이블에 반영됩니다. 즉, 대상자에 추가되거나 대상에서 제거된 프로필입니다. 이 접근 방식을 사용하면 효율적인 업데이트가 보장되고 공유 테이블이 최신 상태로 유지됩니다.

## 전제 조건 {#prerequisites}

Snowflake 연결을 구성하기 전에 다음 전제 조건을 충족하는지 확인하십시오.

* [!DNL Snowflake] 계정에 액세스할 수 있습니다.
* Snowflake 계정이 비공개 목록을 구독하고 있습니다. 귀하 또는 Snowflake에 대한 계정 관리자 권한이 있는 회사에서 이 구성을 할 수 있습니다.

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다. 아래 두 표는 이 커넥터가 지원하는 대상을 _대상 원본_ 및 _대상에 포함된 프로필 유형_&#x200B;별로 나타냅니다.

| 대상자 원본 | 지원됨 | 설명 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Experience Platform [세그먼테이션 서비스](../../../segmentation/home.md)를 통해 생성된 대상입니다. |
| 기타 모든 대상 원본 | ✓ | 이 범주에는 [!DNL Segmentation Service]을(를) 통해 생성된 대상 외부의 모든 대상 출처가 포함됩니다. [다양한 대상 원본](/help/segmentation/ui/audience-portal.md#customize)에 대해 읽어 보십시오. 예를 들면 다음과 같습니다. <ul><li> CSV 파일에서 Experience Platform으로 사용자 지정 업로드 대상 [가져옴](../../../segmentation/ui/audience-portal.md#import-audience),</li><li> 유사 대상, </li><li> 페더레이션 대상, </li><li> Adobe Journey Optimizer과 같은 다른 Experience Platform 앱에서 생성된 대상자 </li><li> 등. </li></ul> |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 대상자 내보내기]** | [!DNL Snowflake] 대상에 사용된 식별자(이름, 전화번호 또는 기타)를 사용하여 대상자의 모든 구성원을 내보내고 있습니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

대상에 인증하려면 **[!UICONTROL 대상에 연결]**&#x200B;을 선택하세요.

![대상에 인증하는 방법을 보여 주는 샘플 스크린샷](../../assets/catalog/cloud-storage/snowflake/authenticate-destination.png)

### 대상 세부 정보 입력 {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_snowflake_accountID"
>title="Snowflake 계정 ID 입력"
>abstract="계정이 조직에 연결되어 있는 경우 다음 형식을 사용합니다. `OrganizationName.AccountName`<br><br> 계정이 조직에 연결되어 있지 않은 경우 다음 형식을 사용합니다. `AccountName`"

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

![대상에 대한 세부 정보를 채우는 방법을 보여 주는 샘플 스크린샷](../../assets/catalog/cloud-storage/snowflake/configure-destination-details.png)

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL Snowflake 계정 ID]**: Snowflake 계정 ID. 계정이 조직에 연결되어 있는지 여부에 따라 다음 계정 ID 형식을 사용하십시오.
   * 계정이 조직에 연결되어 있는 경우: `OrganizationName.AccountName`.
   * 계정이 조직에 연결되어 있지 않은 경우: `AccountName`.
* **[!UICONTROL 계정 승인]**: Snowflake 계정 ID 승인을 전환하여 계정 ID가 올바르고 사용자가 소유하고 있는지 확인합니다.

>[!IMPORTANT]
>
> 대상 이름 및 Experience Platform 샌드박스 이름에 사용된 특수 문자는 Snowflake에서 밑줄(`_`)로 자동 변환됩니다. 혼동을 피하기 위해 대상 및 샌드박스 이름에 특수 문자를 사용하지 마십시오.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 모두 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

이 대상으로 대상을 활성화하는 방법에 대한 지침은 [프로필 및 대상을 스트리밍 대상 내보내기 대상으로 활성화](/help/destinations/ui/activate-segment-streaming-destinations.md)를 참조하십시오.

### 속성 매핑 {#map}

Snowflake 대상은 프로필 속성을 사용자 지정 속성에 매핑할 수 있도록 지원합니다.

![Snowflake 대상에 대한 매핑 화면을 표시하는 Experience Platform 사용자 인터페이스 이미지입니다.](../../assets/catalog/cloud-storage/snowflake/mapping.png)

대상 특성은 **[!UICONTROL 특성 이름]** 필드에 입력한 특성 이름을 사용하여 Snowflake에서 자동으로 만들어집니다.

## 내보낸 데이터/데이터 내보내기 유효성 검사 {#exported-data}

Snowflake 계정을 확인하여 데이터가 올바르게 내보내졌는지 확인하십시오.

## 데이터 사용 및 관리 {#data-usage-governance}

데이터를 처리할 때 모든 [!DNL Adobe Experience Platform] 대상이 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](/help/data-governance/home.md)를 참조하십시오.
