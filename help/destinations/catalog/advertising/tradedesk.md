---
keywords: 광고, 무역데스크, 광고 무역데스크
title: 트레이드 데스크 연결
description: Trade Desk는 광고 구매자가 디스플레이, 비디오 및 모바일 인벤토리 소스에 걸쳐 리타겟팅 및 대상자 타겟팅 디지털 캠페인을 실행할 수 있는 셀프서비스 플랫폼입니다.
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 3%

---

# [!DNL The Trade Desk] 연결

## 개요 {#overview}

[!DNL The Trade Desk] 대상 은 프로필 데이터를에 전송하는 데 도움이 됩니다. [!DNL The Trade Desk].

[!DNL The Trade Desk] 는 광고 구매자가 디스플레이, 비디오 및 모바일 인벤토리 소스에 걸쳐 리타겟팅 및 대상자 타겟팅 디지털 캠페인을 실행할 수 있는 셀프서비스 플랫폼입니다.

프로필 데이터를 (으)로 보내려면 [!DNL Trade Desk], 먼저 대상에 연결해야 합니다.

## 사용 사례 {#use-cases}

마케터로서 다음으로 구성된 대상을 사용할 수 있기를 원합니다 [!DNL Trade Desk IDs] 또는 디바이스 ID를 사용하여 리타겟팅 또는 대상 타겟팅된 디지털 캠페인을 생성할 수 있습니다.

## 지원되는 ID {#supported-identities}

[!DNL The Trade Desk] 는 아래 표에 표시된 id를 기반으로 대상의 활성화를 지원합니다. 자세히 알아보기 [id](/help/identity-service/features/namespaces.md).

| 신원 | 설명 |
|---|---|
| GAID | [!DNL Google Advertising ID] |
| IDFA | [!DNL Apple ID for Advertisers] |
| 트레이드 데스크 ID | 트레이드 데스크 플랫폼의 광고주 ID |

{style="table-layout:auto"}

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ 덧신 | Experience Platform을 통해 생성된 대상자 [세분화 서비스](../../../segmentation/home.md). |
| 사용자 정의 업로드 | ✓ | 대상 [가져옴](../../../segmentation/ui/overview.md#import-audience) csv 파일에서 Experience Platform으로 변환했습니다. |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 대상자 내보내기]** | 대상의 모든 구성원을 대상으로 내보내고 있습니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 전제 조건 {#prerequisites}

>[!IMPORTANT]
>
>을(를) 사용하여 첫 번째 대상을 만들려는 경우 [!DNL The Trade Desk] 및 이(가) 을(를) 활성화하지 않음 [ID 동기화 기능](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) 과거의 Experience Cloud ID 서비스(Adobe Audience Manager 또는 기타 애플리케이션 포함)에서 ID 동기화를 활성화하려면 Adobe 컨설팅 또는 고객 지원 센터에 문의하십시오. 이전에 을 설정한 경우 [!DNL The Trade Desk] Audience Manager의 통합, 설정한 ID 동기화를 플랫폼으로 이월합니다.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

이 대상에 연결하려면 다음과같이 하십시오. [대상 구성 자습서](../../ui/connect-destination.md).

### 연결 매개변수 {#parameters}

While [설정 중](../../ui/connect-destination.md) 이 대상에는 다음 정보를 제공해야 합니다.

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 계정 ID]**: 사용자 [!DNL Trade Desk] [!UICONTROL 계정 ID].
* **[!UICONTROL 서버 위치]**: 다음 사용자에게 묻기 [!DNL Trade Desk] 사용해야 하는 지역 서버를 나타냅니다. 선택할 수 있는 지역 서버는 다음과 같습니다.
   * **[!UICONTROL 유럽]**
   * **[!UICONTROL 싱가포르]**
   * **[!UICONTROL 도쿄]**
   * **[!UICONTROL 북미 동부]**
   * **[!UICONTROL 북아메리카(서부)]**
   * **[!UICONTROL 라틴 아메리카]**

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 다음 안내서를 참조하십시오. [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보를 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.
>* 내보내려면 *id*, 다음이 필요합니다. **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). <br> ![워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다.](/help/destinations/assets/overview/export-identities-to-destination.png "워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다."){width="100" zoomable="yes"}

다음을 참조하십시오 [대상 데이터를 스트리밍 대상 내보내기 대상으로 활성화](../../ui/activate-segment-streaming-destinations.md) 이 대상에 대한 대상자 활성화에 대한 지침을 참조하십시오.

다음에서 [대상자 일정](../../ui/activate-segment-streaming-destinations.md#scheduling) 단계에서는 대상을 대상 플랫폼의 해당 ID 또는 친숙한 이름에 수동으로 매핑해야 합니다.

세그먼트를 매핑할 때는 쉽게 사용할 수 있도록 Platform 대상 이름 또는 더 짧은 형식을 사용하는 것이 좋습니다. 그러나 대상의 대상 ID 또는 이름은 Platform 계정의 대상 ID와 일치할 필요가 없습니다. 매핑 필드에 삽입하는 모든 값은 대상에 의해 반영됩니다.

여러 장치 매핑 (쿠키 ID)을 사용하는 경우 [!DNL IDFA], [!DNL GAID]) 세 가지 매핑 모두에 대해 동일한 매핑 값을 사용해야 합니다. [!DNL The Trade Desk] 는 모든 세그먼트를 장치 수준 분류와 함께 단일 세그먼트로 집계합니다.

![세그먼트 매핑 ID](../../assets/common/segment-mapping-id.png)

## 내보낸 데이터 {#exported-data}

데이터를 (으)로 성공적으로 내보냈는지 확인하려면 [!DNL The Trade Desk] 대상, 다음을 확인: [!DNL Trade Desk] 계정입니다. 활성화가 성공하면 계정에 대상자가 채워집니다.
