---
keywords: 광고, 무역데스크, 광고 무역데스크
title: 트레이드 데스크 연결
description: Trade Desk는 광고 구매자가 디스플레이, 비디오 및 모바일 인벤토리 소스에 걸쳐 리타겟팅 및 대상자 타겟팅 디지털 캠페인을 실행할 수 있는 셀프서비스 플랫폼입니다.
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '781'
ht-degree: 3%

---

# [!DNL The Trade Desk] 연결

## 개요 {#overview}

이 대상 커넥터를 사용하여 [!DNL The Trade Desk]&#x200B;(으)로 프로필 데이터를 보냅니다. 이 커넥터는 [!DNL The Trade Desk] 자사 끝점으로 데이터를 보냅니다. Adobe Experience Platform과 [!DNL The Trade Desk] 간의 통합은 [!DNL The Trade Desk] 타사 끝점으로 데이터 내보내기를 지원하지 않습니다.

[!DNL The Trade Desk]은(는) 광고 구매자가 디스플레이, 비디오 및 모바일 인벤토리 소스에 걸쳐 리타겟팅 및 대상자 타겟팅 디지털 캠페인을 실행할 수 있는 셀프서비스 플랫폼입니다.

[!DNL Trade Desk]에 프로필 데이터를 보내려면 먼저 이 페이지의 다음 섹션에 설명된 대로 대상에 연결해야 합니다.

## 사용 사례 {#use-cases}

마케터로서 [!DNL Trade Desk IDs] 또는 장치 ID로 구축된 대상을 사용하여 리타겟팅 또는 대상 타겟팅된 디지털 캠페인을 만들 수 있기를 원합니다.

## 지원되는 ID {#supported-identities}

[!DNL The Trade Desk]은(는) 아래 표에 표시된 ID를 기반으로 대상자 활성화를 지원합니다. [ID](/help/identity-service/features/namespaces.md)에 대해 자세히 알아보세요.

| ID | 설명 |
|---|---|
| GAID | [!DNL Google Advertising ID] |
| IDFA | [!DNL Apple ID for Advertisers] |
| 트레이드 데스크 ID | 트레이드 데스크 플랫폼의 광고주 ID |

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
| 내보내기 유형 | **[!UICONTROL 대상자 내보내기]** | 대상의 모든 구성원을 대상으로 내보내고 있습니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 전제 조건 {#prerequisites}

>[!IMPORTANT]
>
>[!DNL The Trade Desk]을(를) 사용하여 첫 번째 대상을 만들려고 하는데 이전에 Experience Cloud ID 서비스에서 [ID 동기화 기능](https://experienceleague.adobe.com/en/docs/id-service/using/id-service-api/methods/idsync)을(를) 활성화하지 않은 경우(Adobe Audience Manager 또는 기타 응용 프로그램 사용) Adobe Consulting 또는 고객 지원 센터에 연락하여 ID 동기화를 활성화하십시오. 이전에 Audience Manager에서 [!DNL The Trade Desk] 통합을 설정한 경우 설정한 ID 동기화가 Experience Platform으로 이월됩니다.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오.

### 연결 매개변수 {#parameters}

[이 대상을 설정](../../ui/connect-destination.md)하는 동안 다음 정보를 제공해야 합니다.

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 계정 ID]**: [!DNL Trade Desk] [!UICONTROL 계정 ID].
* **[!UICONTROL 서버 위치]**: 사용할 지역 서버를 [!DNL Trade Desk] 담당자에게 문의하십시오. 다음은 선택할 수 있는 사용 가능한 지역 서버입니다.
   * **[!UICONTROL 유럽]**
   * **[!UICONTROL 싱가포르]**
   * **[!UICONTROL 도쿄]**
   * **[!UICONTROL 북미 동부]**
   * **[!UICONTROL 북미 서부]**
   * **[!UICONTROL 라틴 아메리카]**

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 모두 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

이 대상에 대한 대상 활성화에 대한 지침은 [대상 데이터를 스트리밍 대상 내보내기 대상으로 활성화](../../ui/activate-segment-streaming-destinations.md)를 참조하십시오.

[대상 일정](../../ui/activate-segment-streaming-destinations.md#scheduling) 단계에서는 대상을 대상 플랫폼의 해당 ID 또는 친숙한 이름에 수동으로 매핑해야 합니다.

대상을 매핑할 때에는 Adobe에서 사용하기 쉽도록 Experience Platform 대상 이름 또는 더 짧은 형식을 사용하는 것이 좋습니다. 그러나 대상의 대상 ID 또는 이름은 Experience Platform 계정의 대상 ID 또는 이름과 일치할 필요가 없습니다. 매핑 필드에 삽입하는 모든 값은 대상에 의해 반영됩니다.

여러 장치 매핑(쿠키 ID, [!DNL IDFA], [!DNL GAID])을 사용하는 경우 세 매핑 모두에 대해 동일한 매핑 값을 사용해야 합니다. [!DNL The Trade Desk]은(는) 장치 수준 분류와 함께 모든 세그먼트를 단일 세그먼트로 집계합니다.

![세그먼트 매핑 ID](../../assets/common/segment-mapping-id.png)

## 내보낸 데이터 {#exported-data}

데이터를 [!DNL The Trade Desk] 대상으로 내보냈는지 확인하려면 [!DNL Trade Desk] 계정을 확인하세요. 활성화가 성공하면 계정에 대상자가 채워집니다.
