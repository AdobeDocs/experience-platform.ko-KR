---
title: Pinterest 고객 목록 연결
description: 고객 목록, 사이트를 방문한 사람 또는 Pinterest의 콘텐츠와 이미 상호 작용한 사람으로 대상을 만듭니다.
exl-id: e601f75f-0d40-4cd0-93ca-54d7439f1db7
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 3%

---

# [!DNL Pinterest Customer List] 연결

## 개요 {#overview}

고객 목록, 사이트를 방문한 사람 또는 Pinterest의 콘텐츠와 이미 상호 작용한 사람으로 대상을 만듭니다.

>[!IMPORTANT]
>
>이 대상은 Pinterest 팀이 빌드했습니다. 문의나 업데이트 요청은 https://help.pinterest.com/en/contact에서 직접 문의하십시오.

## 전제 조건 {#prerequisites}

* 사용자는 대상을 추가하려는 광고주 계정에 액세스할 수 있는 Pinterest 계정으로 인증해야 합니다. 광고주 계정 공유에 대한 세부 사항을 찾을 수 있습니다 [여기](https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts). 특히 사용자에게 &quot;대상&quot; 액세스 수준이 필요합니다.
* 고객 목록 ID 형식에 대한 자세한 내용은 [여기](https://help.pinterest.com/en/business/article/audience-targeting).

## 지원되는 ID {#supported-identities}

다음 [!DNL Pinterest Customer List] 대상은 아래 표에 설명된 ID의 활성화를 지원합니다. 추가 정보 [id](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

에서 [매핑 단계](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) 대상 활성화 워크플로우의 경우 원하는 ID를 대상 필드에 매핑합니다 *pinterest_audience*. ID는 Pinterest에 데이터를 수집하면 구분되고 해결됩니다.

| Target ID | 설명 | 고려 사항 |
|---|---|---|
| GAID | [!DNL Google Advertising ID] | 맵 *GAID* 소스 ID 네임스페이스를 대상 ID 필드에 추가합니다 *pinterest_audience*. ID는 Pinterest에 데이터를 수집하면 구분되고 해결됩니다. |
| IDFA | [!DNL Apple ID for Advertisers] | 맵 *IDFA* 소스 ID 네임스페이스를 대상 ID 필드에 추가합니다 *pinterest_audience*. ID는 Pinterest에 데이터를 수집하면 구분되고 해결됩니다. |
| 이메일 | 이메일 주소(텍스트 지우기 또는 SHA256 알고리즘을 사용하여 해시됨) | 일반 텍스트와 SHA256 해시된 이메일 주소는 모두 Adobe Experience Platform에서 지원합니다. <br> 맵 *이메일* 또는 *Email_LC_SHA256* 소스 ID 네임스페이스를 대상 ID 필드에 추가합니다 *pinterest_audience*. |

{style=&quot;table-layout:auto&quot;}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 세그먼트 내보내기]** | pinterest 고객 목록 대상에서 사용되는 식별자(이름, 전화 번호 또는 기타)로 세그먼트(대상)의 모든 구성원을 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상 설정&quot; API 기반 연결입니다. 세그먼트 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터는 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## 사용 사례 {#use-cases}

를 사용하는 방법과 시기를 더 잘 이해할 수 있도록 하기 위해 [!DNL Pinterest Customer List] 대상, Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례는 다음과 같습니다.

### 사용 사례 #1

고객 목록, 사이트를 방문한 사람 또는 Pinterest의 콘텐츠와 이미 상호 작용한 사람으로 대상을 만듭니다.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md).

### 연결 매개 변수 {#parameters}

While [설정](../../ui/connect-destination.md) 이 대상을 사용하려면 다음 정보를 제공해야 합니다.

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식하는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 광고주 ID]**: pinterest 광고주 ID입니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상으로 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보 제공을 마치면 를 선택합니다 **[!UICONTROL 다음]**.

## 세그먼트를 이 대상에 활성화 {#activate}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

읽기 [스트리밍 세그먼트 내보내기 대상으로 프로필 및 세그먼트를 활성화합니다](/help/destinations/ui/activate-segment-streaming-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

## 데이터 사용 및 거버넌스 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스를 적용하는 경우 다음을 참조하십시오. [데이터 거버넌스 개요](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=ko).

## 추가 리소스 {#additional-resources}

자세한 내용은 [Pinterest 도움말 센터 페이지](https://help.pinterest.com/en/business/article/audience-targeting) 추가 정보.
