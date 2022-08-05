---
keywords: 광고; criteo;
title: 기준 연결
description: Criteo는 신뢰할 수 있고 영향력 있는 광고를 통해 모든 소비자를 인터넷 개방에서 더 풍부한 경험을 제공합니다. 세계 최대 규모의 상거래 데이터 세트와 동급 최강의 AI를 사용하는 Criteo는 쇼핑 여정의 각 터치포인트를 적시에 적절한 광고를 통해 고객에게 도달하도록 개인화할 수 있습니다.
exl-id: e6f394b2-ab82-47bb-8521-1cf9d01a203b
source-git-commit: 8211ca28462548e1c17675e504e6de6f5cc55e73
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 2%

---

# (베타) 기준 연결

## 개요 {#overview}

>[!IMPORTANT]
>
>이 설명서 페이지는 Criteo에서 만들었습니다. 현재 베타 제품이며 변경될 수 있습니다. 문의 사항이나 업데이트 요청에 대해서는 Critio에 직접 문의하십시오 [여기](mailto:criteoTechnicalPartnerships@criteo.com).

Criteo는 신뢰할 수 있고 영향력 있는 광고를 통해 모든 소비자를 인터넷 개방에서 더 풍부한 경험을 제공합니다. 세계 최대 규모의 상거래 데이터 세트와 동급 최강의 AI를 사용하는 Criteo는 쇼핑 여정의 각 터치포인트를 적시에 적절한 광고를 통해 고객에게 도달하도록 개인화할 수 있습니다.

## 전제 조건 {#prerequisites}

* 관리자 사용자 계정이 설정되어 있어야 합니다 [Criteo Management Center](https://marketing.criteo.com).
* Critical Advertiser ID가 필요합니다(이 ID가 없는 경우 Critical 담당자에게 요청).
* 다음을 제공해야 합니다. [!DNL GUM caller ID]를 사용할 경우 [!DNL GUM ID] 를 식별자로 사용합니다.

## 제한 사항 {#limitations}

* 기준은 [!DNL SHA-256]-해시된 일반 텍스트 이메일(다음으로 변환) [!DNL SHA-256] 보내기 전). PII(개인 이름 또는 전화 번호와 같은 개인 식별 정보)는 전송하지 마십시오.
* 클라이언트는 하나 이상의 식별자를 제공해야 합니다. 우선 순위를 매깁니다 [!DNL GUM ID] 해시된 이메일에 대한 식별자로, 일치율이 향상되는 데 기여합니다.

![전제 조건](../../assets/catalog/advertising/criteo/prerequisites.png)

## 지원되는 ID {#supported-identities}

기준은 아래 표에 설명된 ID 활성화를 지원합니다. 추가 정보 [id](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Target ID | 설명 | 고려 사항 |
| --- | --- | --- |
| `email_sha256` | SHA-256 알고리즘을 사용하여 해시된 이메일 주소 | 일반 텍스트와 SHA-256 해시된 이메일 주소는 모두 Adobe Experience Platform에서 지원합니다. 소스 필드에 해시되지 않은 속성이 포함되어 있으면 [!UICONTROL 변형 적용] 활성화 시 Platform에서 자동으로 데이터를 해시하도록 하는 옵션. |
| `gum_id` | 크리테이오 [!DNL GUM] 쿠키 식별자 | [!DNL GUM IDs] 클라이언트가 사용자 식별 시스템과 Criteo의 사용자 ID([!DNL UID]). 식별자 유형이 `gum_id`, 추가 매개 변수, [!DNL GUM Caller ID]도 포함해야 합니다. 적절한 경우 Criteo 계정 팀에 문의하십시오 [!DNL GUM Caller ID] 또는 이 작업에 대한 자세한 정보를 [!DNL GUM ID] 필요한 경우 동기화합니다. |

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
| --- | --- | --- |
| 내보내기 유형 | 세그먼트 내보내기 | 에서 사용되는 식별자(이름, 전화 번호 또는 기타 식별자)로 세그먼트의 모든 멤버(대상)를 내보내고 있습니다 [!DNL Criteo] 대상. |
| 내보내기 빈도 | 스트리밍 | 스트리밍 대상은 &quot;항상 설정&quot; API 기반 연결입니다. 세그먼트 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터는 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. 자세한 내용 [스트리밍 대상](../../destination-types.md#streaming-destinations). |

## 사용 사례 {#use-cases}

를 사용하는 방법을 이해하는 데 도움이 되도록 [!DNL Criteo] 대상, Adobe Experience Platform 고객이 수행할 수 있는 몇 가지 목표는 다음과 같습니다 [!DNL Criteo]:

### 사용 사례 1 : 트래픽 가져오기

적절한 제품 오퍼와 유연한 크리에이티브를 통해 비즈니스를 소개하십시오. 지능형 제품 권장 사항을 사용하면 광고는 방문 및 참여를 트리거할 가능성이 가장 큰 제품을 자동으로 제공합니다. 유연한 타겟팅을 사용하면 Critio의 상거래 데이터 세트 또는 고유한 잠재 고객 목록 및 Adobe CDP 세그먼트에서 대상을 구축할 수 있습니다.

### 사용 사례 2 : 웹 사이트 전환 증가

방문자가 웹 사이트를 떠날 때 다음에 가는 위치에 특별한 거래 및 하이퍼 관련 오퍼를 표시하여 전환율을 높이는 리타겟팅 광고로 인해 누락된 내용을 방문자에게 알려줍니다. Adobe CDP 세그먼트를 연결하여 기존 고객을 다시 참여시키거나 충성도가 높은 구매자와 유사한 고객을 타깃팅할 수 있습니다.

## 기준에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md).

### 기준에 대한 인증

연결하는 단계는 다음과 같습니다.

1. Adobe Experience Platform에 로그인하고 기준 대상에 연결합니다.

   ![로그인합니다](../../assets/catalog/advertising/criteo/connect-destination.png)

1. 연결을 인증하도록 Criteo로 리디렉션됩니다. 먼저 자격 증명으로 로그인해야 할 수 있습니다.

   ![전자 로그인](../../assets/catalog/advertising/criteo/log-in-1.png)

   ![전자 로그인](../../assets/catalog/advertising/criteo/log-in-2.png)

   ![전자 로그인](../../assets/catalog/advertising/criteo/log-in-3.png)


### 연결 매개 변수 {#connection-parameters}

대상에 인증한 후 다음 연결 매개 변수를 입력하십시오.

![연결 매개 변수](../../assets/catalog/advertising/criteo/connection-parameters.png)

| 필드 | 설명 | 필수 여부 |
| --- | --- | --- |
| 이름 | 나중에 이 대상을 인식하는 데 도움이 되는 이름입니다. 여기서 선택하는 이름은 다음과 같습니다 [!DNL Audience] 이름(Criteo Management Center)을 사용하여 나중에 수정할 수 없습니다. | 예 |
| 설명 | 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다. | 아니요 |
| 광고주 ID | 조직의 기준 광고주 ID입니다. 이 정보를 얻으려면 Criteo 계정 관리자에게 문의하십시오. | 예 |
| 크리테이오 [!DNL GUM caller ID] | [!DNL GUM Caller ID] Analytics Premium을 사용할 수 없습니다. 적절한 경우 Criteo 계정 팀에 문의하십시오 [!DNL GUM Caller ID] 또는 이 작업에 대한 자세한 정보를 [!DNL GUM] 필요한 경우 동기화합니다. | 네, 언제나 [!DNL GUM ID] 은 식별자로 제공됩니다 |

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상으로 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보 제공을 마치면 를 선택합니다 **[!UICONTROL 다음]**.

## 세그먼트를 이 대상에 활성화 {#activate-segments}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 다음 문서를 참조하십시오. [액세스 제어 개요](/help/access-control/ui/overview.md) 또는 제품 관리자에게 문의하여 필요한 권한을 얻으십시오.

읽기 [스트리밍 세그먼트 내보내기 대상으로 프로필 및 세그먼트를 활성화합니다](../../ui/activate-segment-streaming-destinations.md) 대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침입니다.

## 내보낸 데이터 {#exported-data}

에서 내보낸 세그먼트를 볼 수 있습니다 [기준 관리 센터](https://marketing.criteo.com/audience-manager/dashboard).

에서 받은 사용자 프로필 추가 요청 본문 [!DNL Criteo] 연결은 다음과 유사합니다.

```json
{
  "data": {
    "type": "ContactlistWithUserAttributesAmendment",
    "attributes": {
      "operation": "add",
      "identifierType": "gum",
      "gumCallerId": "123",
      "identifiers": [
        {
          "identifier": "456",
          "attributes": [
            { "key": "ctoid_GumCaller", "value": "123" },
            { "key": "ctoid_Gum", "value": "456" },
            {
              "key": "ctoid_HashedEmail",
              "value": "98833030dc03751f2b2c1a0017078975fdae951aa6908668b3ec422040f2d4be"
            }
          ]
        }
      ]
    }
  }
}
```

에서 받은 사용자 프로필 제거 요청 본문 [!DNL Criteo] 연결은 다음과 유사합니다.

```json
{
  "data": {
    "type": "ContactlistWithUserAttributesAmendment",
    "attributes": {
      "operation": "remove",
      "identifierType": "gum",
      "gumCallerId": "123",
      "identifiers": [
        {
          "identifier": "456",
          "attributes": [
            { "key": "ctoid_GumCaller", "value": "123" },
            { "key": "ctoid_Gum", "value": "456" },
            {
              "key": "ctoid_HashedEmail",
              "value": "98833030dc03751f2b2c1a0017078975fdae951aa6908668b3ec422040f2d4be"
            }
          ]
        }
      ]
    }
  }
}
```

## 데이터 사용 및 거버넌스 {#data-usage}

모든 Adobe Experience Platform 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. Adobe Experience Platform에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=en).

## 추가 리소스

* [크리테이오 도움말 센터](https://help.criteo.com/kb/en)
* [Digital Developer Portal](https://developers.criteo.com)
