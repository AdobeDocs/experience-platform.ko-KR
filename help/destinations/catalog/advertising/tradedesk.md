---
keywords: 광고; 영업 데스크 광고 회사
title: 무역센터 연결
description: Trade Desk는 광고 구매자가 디스플레이, 비디오 및 모바일 인벤토리 소스에서 타겟팅된 디지털 캠페인을 실행하고 재타겟팅할 수 있는 셀프서비스 플랫폼입니다.
exl-id: b8f638e8-dc45-4aeb-8b4b-b3fa2906816d
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '676'
ht-degree: 3%

---

# [!DNL The Trade Desk] 연결

## 개요 {#overview}

[!DNL The Trade Desk] 대상은 프로필 데이터를 로 보내는 데 도움이 됩니다. [!DNL The Trade Desk].

[!DNL The Trade Desk] 는 광고 구매자가 디스플레이, 비디오 및 모바일 인벤토리 소스에서 리타겟팅하고 대상 타겟팅된 디지털 캠페인을 실행할 수 있는 셀프 서비스 플랫폼입니다.

프로필 데이터를 로 보내려면 [!DNL Trade Desk]를 채울 때는 먼저 대상에 연결해야 합니다.

## 사용 사례 {#use-cases}

마케터는 [!DNL Trade Desk IDs] 또는 장치 ID를 사용하여 재타겟팅 또는 대상 타깃팅된 디지털 캠페인을 만들 수 있습니다.

## 지원되는 ID {#supported-identities}

[!DNL The Trade Desk] 은 아래 표에 설명된 id의 활성화를 지원합니다. 추가 정보 [id](/help/identity-service/namespaces.md).

| Target ID | 설명 |
|---|---|
| GAID | [!DNL Google Advertising ID] |
| IDFA | [!DNL Apple ID for Advertisers] |
| 거래 데스크 ID | Trade Desk 플랫폼의 광고주 ID |

{style=&quot;table-layout:auto&quot;}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 세그먼트 내보내기]** | 세그먼트(대상)의 모든 구성원을 대상으로 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상 설정&quot; API 기반 연결입니다. 세그먼트 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터는 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## 전제 조건 {#prerequisites}

>[!IMPORTANT]
>
>을 사용하여 첫 번째 대상을 만들려면 [!DNL The Trade Desk] 및 [ID 동기화 기능](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) 과거(Adobe Audience Manager 또는 다른 애플리케이션 사용) Experience Cloud ID 서비스에서 ID 동기화를 활성화하려면 Adobe 컨설팅 또는 고객 지원 센터에 문의하십시오. 이전에 설정한 경우 [!DNL The Trade Desk] 통합에서 설정한 ID 동기화를 Platform으로 이월합니다.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md).

### 연결 매개 변수 {#parameters}

While [설정](../../ui/connect-destination.md) 이 대상을 사용하려면 다음 정보를 제공해야 합니다.

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식하는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 계정 ID]**: 사용자 [!DNL Trade Desk] [!UICONTROL 계정 ID].
* **[!UICONTROL 서버 위치]**: 질문하기 [!DNL Trade Desk] 사용해야 하는 지역 서버를 나타냅니다. 다음 중에서 선택할 수 있는 지역 서버입니다.
   * **[!UICONTROL 유럽]**
   * **[!UICONTROL 싱가포르]**
   * **[!UICONTROL 도쿄]**
   * **[!UICONTROL 북미 동부]**
   * **[!UICONTROL 북미 서부]**
   * **[!UICONTROL 라틴 아메리카]**

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상으로 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보 제공을 마치면 를 선택합니다 **[!UICONTROL 다음]**.

## 세그먼트를 이 대상에 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

자세한 내용은 [스트리밍 세그먼트 내보내기 대상으로 대상 데이터 활성화](../../ui/activate-segment-streaming-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

에서 [세그먼트 예약](../../ui/activate-segment-streaming-destinations.md#scheduling) 단계별로 수동으로 세그먼트를 대상 플랫폼의 해당 ID 또는 친숙한 이름에 매핑해야 합니다.

세그먼트를 매핑할 때 세그먼트를 쉽게 사용할 수 있도록 Platform 세그먼트 이름 또는 더 짧은 형식을 사용하는 것이 좋습니다. 하지만 대상에 있는 세그먼트 ID 또는 이름이 Platform 계정의 세그먼트 ID와 일치하지 않아도 됩니다. 매핑 필드에 삽입한 모든 값은 대상에 의해 반영됩니다.

여러 장치 매핑(쿠키 ID)을 사용하는 경우 [!DNL IDFA], [!DNL GAID])를 채울 때는 세 가지 매핑 모두에 동일한 매핑 값을 사용해야 합니다. [!DNL The Trade Desk] 는 이러한 모든 세그먼트를 장치 수준 분류와 함께 단일 세그먼트로 집계합니다.

![세그먼트 매핑 ID](../../assets/common/segment-mapping-id.png)

## 내보낸 데이터 {#exported-data}

데이터를 성공적으로 로 내보냈는지 확인하려면 [!DNL The Trade Desk] 대상, [!DNL Trade Desk] 계정이 필요합니다. 활성화가 성공하면 계정에 대상이 채워집니다.
