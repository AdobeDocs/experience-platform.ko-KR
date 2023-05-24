---
keywords: 광고; bing;
title: Microsoft Bing 연결
description: Microsoft Bing 연결 대상을 사용하면 Microsoft 디스플레이 광고 전반에 걸쳐 리타겟팅 및 대상자 타겟팅 디지털 캠페인을 실행할 수 있습니다.
exl-id: e1c0273b-7e3c-4d77-ae14-d1e528ca0294
source-git-commit: aec9708680c2a4cb3c70af12f95c67ec37b2e129
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 8%

---

# [!DNL Microsoft Bing] 연결 {#bing-destination}

## 개요 {#overview}

다음 [!DNL Microsoft Bing] 대상 은 프로필 데이터를에 전송하는 데 도움이 됩니다. [!DNL Microsoft Display Advertising].

프로필 데이터를 (으)로 보내려면 [!DNL Microsoft Bing], 먼저 대상에 연결해야 합니다.

## 사용 사례 {#use-cases}

마케터로서 다음으로 구성된 세그먼트를 사용할 수 있기를 원합니다 [!DNL Microsoft Advertising IDs] 간 디스플레이 광고를 통해 사용자를 타겟팅하려면 [!DNL Microsoft Advertising] 채널.

## 지원되는 ID {#supported-identities}

[!DNL Microsoft Bing] 는 아래 표에 설명된 id 활성화를 지원합니다. 자세히 알아보기 [id](/help/identity-service/namespaces.md).

| TARGET ID | 설명 |
|---|---|
| 하녀 | Microsoft 광고 ID |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

**[!DNL Segment Export]** - 세그먼트의 모든 멤버(대상)를 [!DNL Microsoft Bing] 대상.

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 세그먼트 내보내기]** | 세그먼트(대상자)의 모든 구성원을 (으)로 내보내는 경우 [!DNL Microsoft Bing] 대상. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. Experience Platform 평가를 기반으로 프로필이 세그먼트에서 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 사전 요구 사항 {#prerequisites}

>[!IMPORTANT]
>
>을(를) 사용하여 첫 번째 대상을 만들려는 경우 [!DNL Microsoft Bing] 및 이(가) 을(를) 활성화하지 않음 [ID 동기화 기능](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/idsync.html) 과거의 Experience Cloud ID 서비스(Adobe Audience Manager 또는 기타 애플리케이션 포함)에서 ID 동기화를 활성화하려면 Adobe 컨설팅 또는 고객 지원 센터에 문의하십시오. 이전에 을 설정한 경우 [!DNL Microsoft Bing] Audience Manager의 통합, 설정한 ID 동기화를 플랫폼으로 이월합니다.

대상을 구성할 때는 다음 정보를 제공해야 합니다.

* [!UICONTROL 계정 ID]: 사용자 [!DNL Bing Ads CID], 정수 형식.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

이 대상에 연결하려면 다음과같이 하십시오. [대상 구성 자습서](../../ui/connect-destination.md).

### 연결 매개 변수 {#parameters}

While [설정 중](../../ui/connect-destination.md) 이 대상에는 다음 정보를 제공해야 합니다.

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 계정 ID]**: 사용자 [!DNL Bing Ads Customer ID] (CID). CID는 정수입니다. 로그인할 때 URL에 있습니다. [!DNL Microsoft Advertising].

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 다음 안내서를 참조하십시오. [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보를 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.

## 이 대상에 대한 세그먼트 활성화 {#activate}

>[!CONTEXTUALHELP]
>id="platform_destinations_bing_mapping_id"
>title="ID 매핑"
>abstract="선택한 세그먼트를 매핑할 숫자 Bing 세그먼트 ID를 입력합니다. 제공된 [!UICONTROL 매핑 ID]가 Bing 대상의 세그먼트 ID와 일치하지 않는 경우 Bing 계정에 예상되는 대상자 데이터가 표시되지 않습니다."

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

다음을 참조하십시오 [대상 데이터를 스트리밍 세그먼트 내보내기 대상으로 활성화](../../ui/activate-segment-streaming-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침

다음에서 [세그먼트 일정](../../ui/activate-segment-streaming-destinations.md#scheduling) 단계에서는 의 세그먼트 이름을 수동으로 매핑해야 합니다. [!UICONTROL 매핑 ID] 필드. 이렇게 하면 세그먼트 메타데이터를에 올바르게 전달할 수 있습니다 [!DNL Bing].

![세그먼트 이름을 Bing 매핑 ID에 매핑하는 방법의 예와 함께 세그먼트 일정 화면을 표시하는 UI 이미지입니다.](../../assets/catalog/advertising/bing/mapping-id.png)

## 내보낸 데이터 {#exported-data}

데이터가 성공적으로 로 내보내졌는지 확인하려면 [!DNL Microsoft Bing] 대상, 다음을 확인: [!DNL Microsoft Bing Ads] 계정입니다. 활성화가 성공하면 계정에 대상자가 채워집니다.
