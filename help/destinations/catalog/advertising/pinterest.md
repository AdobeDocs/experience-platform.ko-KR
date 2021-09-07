---
title: Pinterest 고객 목록 연결
description: 고객 목록, 사이트를 방문한 사람 또는 Pinterest의 콘텐츠와 이미 상호 작용한 사람으로 대상을 만듭니다.
source-git-commit: 9bd309ae9d9edf56de855422abd109af1a10cffc
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 2%

---


# Pinterest 고객 목록 연결

## 개요 {#overview}

고객 목록, 사이트를 방문한 사람 또는 Pinterest의 콘텐츠와 이미 상호 작용한 사람으로 대상을 만듭니다.

>[!IMPORTANT]
>
>이 대상은 Pinterest 팀이 빌드했습니다. 문의나 업데이트 요청은 https://help.pinterest.com/en/contact에서 직접 문의하십시오.

## 전제 조건 {#prerequisites}

* 사용자는 대상을 추가하려는 광고주 계정에 액세스할 수 있는 Pinterest 계정으로 인증해야 합니다. 광고주 계정 공유에 대한 자세한 내용은 다음 위치에서 확인할 수 있습니다. https://help.pinterest.com/en/business/article/share-and-manage-access-to-your-ad-accounts 특히 사용자에게 &quot;대상&quot; 액세스 수준이 필요합니다.
* 고객 목록 ID 형식에 대한 자세한 내용은 다음을 참조하십시오. https://help.pinterest.com/en/business/article/audience-targeting


## 지원되는 ID {#supported-identities}

pinterest 고객 목록 대상은 아래 표에 설명된 ID의 활성화를 지원합니다. [id](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started)에 대해 자세히 알아보십시오.

대상 활성화 워크플로우의 [매핑 단계에서 원하는 ID를 대상 필드 *pinterest_audience*&#x200B;에 매핑합니다. ](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) ID는 Pinterest에 데이터를 수집하면 구분되고 해결됩니다.

| Target ID | 설명 | 고려 사항 |
|---|---|---|
| GAID | Google 광고 ID | *GAID* 소스 ID 네임스페이스를 대상 ID 필드 *pinterest_audience*&#x200B;에 매핑합니다. ID는 Pinterest에 데이터를 수집하면 구분되고 해결됩니다. |
| IDFA | 광고주용 Apple ID | *IDFA* 소스 ID 네임스페이스를 대상 ID 필드 *pinterest_audience*&#x200B;에 매핑합니다. ID는 Pinterest에 데이터를 수집하면 구분되고 해결됩니다. |
| 이메일 | 이메일 주소(텍스트 지우기 또는 SHA256 알고리즘을 사용하여 해시됨) | 일반 텍스트와 SHA256 해시된 이메일 주소는 모두 Adobe Experience Platform에서 지원합니다. <br> Emailor  ** Email_ *LC_SHA256* 소스 ID 네임스페이스를 대상 ID 필드  *pinterest_audience*&#x200B;에 매핑합니다. |

{style=&quot;table-layout:auto&quot;}

## 내보내기 유형 {#export-type}

**세그먼트 내보내기**  - Pinterest 고객 목록 대상에서 사용되는 식별자(이름, 전화 번호 또는 기타)로 세그먼트(대상)의 모든 구성원을 내보냅니다.

## 사용 사례 {#use-cases}

pinterest 고객 목록 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 샘플 사용 사례가 여기에 있습니다.


### 사용 사례 #1

고객 목록, 사이트를 방문한 사람 또는 Pinterest의 콘텐츠와 이미 상호 작용한 사람으로 대상을 만듭니다.

## 대상에 연결 {#connect}

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오.



### 연결 매개 변수 {#parameters}

[이 대상을 설정할 때 다음 정보를 제공해야 합니다.](../../ui/connect-destination.md)

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식하는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 계정 ID]**: pinterest 광고 계정 ID입니다.

## 세그먼트를 이 대상에 활성화 {#activate}

대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침은 [프로필 및 세그먼트를 스트리밍 세그먼트 내보내기 대상으로 활성화](/help/destinations/ui/activate-segment-streaming-destinations.md)를 참조하십시오.

## 데이터 사용 및 거버넌스 {#data-usage-governance}

모든 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html)를 참조하십시오.

## 추가 리소스 {#additional-resources}

자세한 내용은 Pinterest 도움말 센터 페이지(https://help.pinterest.com/en/business/article/audience-targeting)을 참조하십시오.