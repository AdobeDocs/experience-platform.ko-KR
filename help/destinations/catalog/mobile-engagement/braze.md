---
keywords: 모바일; 브레이즈; 메시지;
title: 브레이즈 연결
description: Braze는 고객과 고객이 사랑하는 브랜드 간의 관련성 있고 기억에 남는 경험을 제공하는 포괄적인 고객 참여 플랫폼입니다.
last-substantial-update: 2024-08-20T00:00:00Z
exl-id: 508e79ee-7364-4553-b153-c2c00cc85a73
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1125'
ht-degree: 2%

---

# [!DNL Braze] 연결

## 개요 {#overview}

[!DNL Braze] 대상은 프로필 데이터를 [!DNL Braze]&#x200B;(으)로 전송하는 데 도움이 됩니다.

[!DNL Braze]은(는) 고객과 고객이 사랑하는 브랜드 간의 관련성 있고 기억에 남는 경험을 제공하는 포괄적인 고객 참여 플랫폼입니다.

[!DNL Braze]에 프로필 데이터를 보내려면 먼저 대상에 연결해야 합니다.

## 대상 세부 사항 {#specifics}

[!DNL Braze] 대상에 해당하는 다음 세부 정보를 참고하십시오.

* [!DNL Adobe Experience Platform]개의 대상을 `AdobeExperiencePlatformSegments` 특성 아래의 [!DNL Braze]&#x200B;(으)로 내보냅니다.

>[!NOTE]
>
>추가 사용자 지정 특성을 [!DNL Braze]에 보내면 [!DNL Braze] 데이터 포인트 사용량이 늘어날 수 있습니다. 추가 사용자 지정 특성을 보내기 전에 [!DNL Braze] 계정 관리자에게 문의하십시오.

## 사용 사례 {#use-cases}

마케터는 [!DNL Adobe Experience Platform]에 내장된 대상자를 사용하여 모바일 참여 대상에서 사용자를 타깃팅하려고 합니다. 또한 대상자와 프로필이 [!DNL Adobe Experience Platform]에서 업데이트되는 즉시 [!DNL Adobe Experience Platform] 프로필의 특성을 기반으로 개인화된 경험을 전달하려고 합니다.

## 지원되는 ID {#supported-identities}

[!DNL Braze]은(는) 아래 표에 설명된 ID 활성화를 지원합니다.

| 대상 ID | 설명 | 고려 사항 |
|---|---|---|
| external_id | 모든 ID의 매핑을 지원하는 사용자 지정 [!DNL Braze] 식별자입니다. | [!DNL Braze] [`external_id`](https://www.braze.com/docs/api/basics/#external-user-id-explanation)에 매핑하기만 하면 [identity](../../../identity-service/features/namespaces.md)을(를) [!DNL Braze] 대상으로 보낼 수 있습니다. |

{style="table-layout:auto"}

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Experience Platform [세그먼테이션 서비스](../../../segmentation/home.md)를 통해 생성된 대상입니다. |
| 사용자 정의 업로드 | ✓ | CSV 파일에서 Experience Platform으로 대상 [가져옴](../../../segmentation/ui/audience-portal.md#import-audience). |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | 필드 매핑에 따라 원하는 스키마 필드(예: 이메일 주소, 전화번호, 성) 및/또는 ID와 함께 세그먼트의 모든 멤버를 내보냅니다.[!DNL Adobe Experience Platform]개의 대상을 `AdobeExperiencePlatformSegments` 특성 아래의 [!DNL Braze]&#x200B;(으)로 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

대상에 인증하려면 필수 필드를 입력한 다음 **[!UICONTROL 대상에 연결]**&#x200B;을(를) 선택하십시오.

* **[!UICONTROL 계정 토큰 동기화]**: [!DNL Braze] [!DNL API] 키입니다. [!DNL API] 키를 가져오는 방법에 대한 자세한 지침은 [REST API 키 개요](https://www.braze.com/docs/api/api_key/)에서 확인할 수 있습니다.

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 이름을 입력하십시오.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명을 입력하십시오.
* **[!UICONTROL 끝점 인스턴스]**: 사용할 끝점 인스턴스를 [!DNL Braze] 담당자에게 문의하십시오.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 모두 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

이 대상에 대한 대상 활성화에 대한 지침은 [대상 데이터를 스트리밍 대상 내보내기 대상으로 활성화](../../ui/activate-segment-streaming-destinations.md)를 참조하십시오.

## 매핑 고려 사항 {#mapping-considerations}

대상 데이터를 [!DNL Adobe Experience Platform]에서 [!DNL Braze] 대상으로 올바르게 보내려면 필드 매핑 단계를 거쳐야 합니다.

매핑은 [!DNL Experience Platform] 계정의 [!DNL Experience Data Model]&#x200B;(XDM) 스키마 필드와 대상 대상의 해당 필드 필드 사이에 링크를 만드는 것으로 구성됩니다.

XDM 필드를 [!DNL Braze] 대상 필드에 올바르게 매핑하려면 다음 단계를 따르십시오.

[!UICONTROL 매핑] 단계에서 **[!UICONTROL 새 매핑 추가]**&#x200B;를 클릭합니다.

![대상 병합 매핑 추가](../../assets/catalog/mobile-engagement/braze/mapping.png)

[!UICONTROL Source 필드] 섹션에서 빈 필드 옆에 있는 화살표 단추를 클릭합니다.

![대상 Source 매핑 중단](../../assets/catalog/mobile-engagement/braze/mapping-source.png)

[!UICONTROL 소스 필드 선택] 창에서 다음 두 범주의 XDM 필드 중 하나를 선택할 수 있습니다.
* [!UICONTROL 특성 선택]: 이 옵션을 사용하여 XDM 스키마의 특정 필드를 [!DNL Braze] 특성에 매핑합니다.

![대상 매핑 Source 특성 동기화](../../assets/catalog/mobile-engagement/braze/mapping-attributes.png)

* [!UICONTROL ID 네임스페이스 선택]: 이 옵션을 사용하여 [!DNL Experience Platform] ID 네임스페이스를 [!DNL Braze] 네임스페이스에 매핑합니다.

![대상 매핑 Source 네임스페이스 동기화](../../assets/catalog/mobile-engagement/braze/mapping-namespaces.png)

소스 필드를 선택한 다음 **[!UICONTROL 선택]**&#x200B;을 클릭합니다.

[!UICONTROL 대상 필드] 섹션에서 필드 오른쪽에 있는 매핑 아이콘을 클릭합니다.

![대상 매핑 동기화](../../assets/catalog/mobile-engagement/braze/mapping-target.png)

[!UICONTROL 대상 필드 선택] 창에서 다음 두 범주의 대상 필드 중에서 선택할 수 있습니다.
* [!UICONTROL ID 네임스페이스 선택]: 이 옵션을 사용하여 [!DNL Experience Platform] ID 네임스페이스를 [!DNL Braze] ID 네임스페이스에 매핑합니다.
* [!UICONTROL 사용자 지정 특성 선택]: 이 옵션을 사용하여 XDM 특성을 [!DNL Braze] 계정에 정의한 사용자 지정 [!DNL Braze] 특성에 매핑합니다. <br> 이 옵션을 사용하여 기존 XDM 특성의 이름을 [!DNL Braze]&#x200B;(으)로 바꿀 수도 있습니다. 예를 들어 `lastName` XDM 특성을 [!DNL Braze]의 사용자 지정 `Last_Name` 특성에 매핑하면 [!DNL Braze]에 `Last_Name` 특성이 아직 존재하지 않는 경우 이 특성을 만들고 `lastName` XDM 특성을 매핑합니다.

![대상 매핑 필드 동기화](../../assets/catalog/mobile-engagement/braze/mapping-target-fields.png)

대상 필드를 선택한 다음 **[!UICONTROL 선택]**&#x200B;을 클릭합니다.

이제 목록에 필드 매핑이 표시됩니다.

![대상 매핑 중단 완료](../../assets/catalog/mobile-engagement/braze/mapping-complete.png)

매핑을 더 추가하려면 이전 단계를 반복합니다.

## 매핑 예 {#mapping-example}

XDM 프로필 스키마와 [!DNL Braze] 인스턴스에 다음 특성과 ID가 포함되어 있다고 가정합니다.

|  | XDM 프로필 스키마 | [!DNL Braze] 인스턴스 |
|---|---|---|
| 속성 | <ul><li><code>사람.이름.이름</code></li><li><code>person.name.lastName</code></li><li><code>mobilePhone.number</code></li></ul> | <ul><li><code>이름</code></li><li><code>성</code></li><li><code>전화 번호</code></li></ul> |
| ID | <ul><li><code>전자 메일</code></li><li><code>Google 광고 ID(GAID)</code></li><li><code>IDFA(광고주용 Apple ID)</code></li></ul> | <ul><li><code>external_id</code></li></ul> |

올바른 매핑은 다음과 같습니다.

![대상 병합 예제](../../assets/catalog/mobile-engagement/braze/mapping-example.png)

## 내보낸 데이터 {#exported-data}

데이터를 [!DNL Braze] 대상으로 내보냈는지 확인하려면 [!DNL Braze] 계정을 확인하세요. [!DNL Adobe Experience Platform]개의 대상을 `AdobeExperiencePlatformSegments` 특성 아래의 [!DNL Braze]&#x200B;(으)로 내보냅니다.

## 문제 해결 {#troubleshooting}

**이 대상에 대한 대상을 활성화하는 동안 시간 초과 오류가 발생했습니다. 어떻게 해야 합니까?**

간혹 이 대상에 대한 대상을 활성화하면 시간 초과 오류가 발생할 수 있습니다. 이 오류는 활성화 문제를 나타내지 않습니다.

시간 초과 오류가 표시되면 대상 플랫폼에서 대상 크기를 확인합니다. 대상자 크기가 올바른 경우 통합이 예상대로 작동합니다.

## 데이터 사용 및 관리 {#data-usage-governance}

데이터를 처리할 때 모든 [!DNL Adobe Experience Platform] 대상이 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](../../../data-governance/home.md)를 참조하십시오.
