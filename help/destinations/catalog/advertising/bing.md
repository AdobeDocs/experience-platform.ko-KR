---
keywords: '광고; bing; '
title: Microsoft Bing 연결
description: Microsoft Bing 연결 대상을 사용하면 Microsoft Display Advertising에서 리타겟팅 및 대상 타깃팅된 디지털 캠페인을 실행할 수 있습니다.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: 15ea3ab9370541c35b874414a8753e8812eea9c6
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 1%

---

# [!DNL Microsoft Bing] 연결 {#bing-destination}

## 개요 {#overview}

[!DNL Microsoft Bing] 대상은 프로필 데이터를 [!DNL Microsoft Display Advertising]에 전송하는 데 도움이 됩니다.

프로필 데이터를 [!DNL Microsoft Bing]에 보내려면 먼저 대상에 연결해야 합니다.

## 사용 사례 {#use-cases}

마케터는 [!DNL Microsoft Advertising IDs]으로 작성된 세그먼트를 사용하여 [!DNL Microsoft Advertising] 채널에서 디스플레이 광고를 통해 사용자를 타깃팅하고 싶습니다.

## 지원되는 ID {#supported-identities}

[!DNL Microsoft Bing] 은 아래 표에 설명된 id의 활성화를 지원합니다. [id](/help/identity-service/namespaces.md)에 대해 자세히 알아보십시오.

| Target ID | 설명 |
|---|---|
| 가정부 | Microsoft 광고 ID |

## 내보내기 유형 {#export-type}

**[!DNL Segment Export]** - 세그먼트(대상)의 모든 구성원을 대상으로  [!DNL Microsoft Bing] 내보냅니다.

## 전제 조건 {#prerequisites}

[!DNL Microsoft Bing]을(를) 사용하여 첫 번째 대상을 만들고 과거에 Experience Cloud ID 서비스에서 [ID 동기화 기능](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html)을 활성화하지 않은 경우(Adobe Audience Manager 또는 다른 애플리케이션 사용) Adobe 컨설팅이나 고객 지원 센터에 연락하여 ID 동기화를 활성화하십시오. 이전에 Audience Manager에서 [!DNL Microsoft Bing] 통합을 설정한 경우 설정한 ID 동기화를 Platform으로 이월합니다.

대상을 구성할 때 다음 정보를 제공해야 합니다.

* [!UICONTROL 계정 ID]: 정수  [!DNL Bing Ads CID]형식으로 된 것입니다.

## 대상에 연결 {#connect}

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오.

### 연결 매개 변수 {#parameters}

[이 대상을 설정할 때 다음 정보를 제공해야 합니다.](../../ui/connect-destination.md)

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식하는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 계정 ID]**: 사용자  [!DNL Bing Ads CID].

## 세그먼트를 이 대상에 활성화 {#activate}

대상으로 대상 세그먼트를 활성화하는 방법에 대한 지침은 [대상 세그먼트 활성화](../../ui/activate-destinations.md)를 참조하십시오.

[세그먼트 예약](../../ui/activate-destinations.md#segment-schedule) 단계에서 세그먼트를 대상의 해당 ID 또는 친숙한 이름에 수동으로 매핑해야 합니다.

세그먼트를 매핑할 때는 쉽게 사용할 수 있도록 [!DNL Platform] 세그먼트 이름 또는 더 짧은 형식의 세그먼트를 사용하는 것이 좋습니다. 그러나 대상의 세그먼트 ID나 이름은 [!DNL Platform] 계정의 세그먼트 ID와 일치하지 않아도 됩니다. 매핑 필드에 삽입한 모든 값은 대상에 의해 반영됩니다.

## 내보낸 데이터 {#exported-data}

데이터를 [!DNL Microsoft Bing] 대상으로 성공적으로 내보냈는지 확인하려면 [!DNL Microsoft Bing Ads] 계정을 확인하십시오. 활성화가 성공하면 계정에 대상이 채워집니다.
