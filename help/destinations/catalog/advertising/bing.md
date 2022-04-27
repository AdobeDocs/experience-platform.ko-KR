---
keywords: '광고; bing; '
title: Microsoft Bing 연결
description: Microsoft Bing 연결 대상을 사용하면 Microsoft 디스플레이 광고에서 리타겟팅 및 대상 타깃팅된 디지털 캠페인을 실행할 수 있습니다.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: 0006c498cd33d9deb66f1d052b4771ec7504457d
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 3%

---

# [!DNL Microsoft Bing] 연결 {#bing-destination}

## 개요 {#overview}

다음 [!DNL Microsoft Bing] 대상은 프로필 데이터를 로 보내는 데 도움이 됩니다. [!DNL Microsoft Display Advertising].

프로필 데이터를 로 보내려면 [!DNL Microsoft Bing]를 채울 때는 먼저 대상에 연결해야 합니다.

## 사용 사례 {#use-cases}

마케터는 [!DNL Microsoft Advertising IDs] 디스플레이 광고를 통해 사용자를 타깃팅합니다. [!DNL Microsoft Advertising] 채널입니다.

## 지원되는 ID {#supported-identities}

[!DNL Microsoft Bing] 은 아래 표에 설명된 id의 활성화를 지원합니다. 추가 정보 [id](/help/identity-service/namespaces.md).

| Target ID | 설명 |
|---|---|
| 가정부 | Microsoft 광고 ID |

{style=&quot;table-layout:auto&quot;}

## 내보내기 유형 및 빈도 {#export-type-frequency}

**[!DNL Segment Export]** - 세그먼트의 모든 멤버(대상)를 [!DNL Microsoft Bing] 대상.

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 세그먼트 내보내기]** | 세그먼트(대상)의 모든 구성원을 [!DNL Microsoft Bing] 대상. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상 설정&quot; API 기반 연결입니다. 세그먼트 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터는 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## 전제 조건 {#prerequisites}

>[!IMPORTANT]
>
>을 사용하여 첫 번째 대상을 만들려면 [!DNL Microsoft Bing] 및 [ID 동기화 기능](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) 과거(Adobe Audience Manager 또는 다른 애플리케이션 사용) Experience Cloud ID 서비스에서 ID 동기화를 활성화하려면 Adobe 컨설팅 또는 고객 지원 센터에 문의하십시오. 이전에 설정한 경우 [!DNL Microsoft Bing] 통합에서 설정한 ID 동기화를 Platform으로 이월합니다.

대상을 구성할 때 다음 정보를 제공해야 합니다.

* [!UICONTROL 계정 ID]: 이건 [!DNL Bing Ads CID]: 정수 형식으로

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md).

### 연결 매개 변수 {#parameters}

While [설정](../../ui/connect-destination.md) 이 대상을 사용하려면 다음 정보를 제공해야 합니다.

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식하는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 계정 ID]**: 사용자 [!DNL Bing Ads CID].

## 세그먼트를 이 대상에 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

자세한 내용은 [스트리밍 세그먼트 내보내기 대상으로 대상 데이터 활성화](../../ui/activate-segment-streaming-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

에서 [세그먼트 예약](../../ui/activate-segment-streaming-destinations.md#scheduling) 단계에서 세그먼트를 대상의 해당 ID 또는 친숙한 이름에 수동으로 매핑해야 합니다.

세그먼트를 매핑할 때는 [!DNL Platform] 쉽게 사용할 수 있도록 세그먼트 이름 또는 더 짧은 형식의 세그먼트를 만듭니다. 하지만 대상에 있는 세그먼트 ID나 이름이 [!DNL Platform] 계정이 필요합니다. 매핑 필드에 삽입한 모든 값은 대상에 의해 반영됩니다.

## 내보낸 데이터 {#exported-data}

데이터를 로 성공적으로 내보냈는지 확인하려면 [!DNL Microsoft Bing] 대상, [!DNL Microsoft Bing Ads] 계정이 필요합니다. 활성화가 성공하면 계정에 대상이 채워집니다.
