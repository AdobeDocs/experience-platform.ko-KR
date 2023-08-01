---
keywords: advertising; criteo;
title: 크리테오 연결
description: 크리테오는 신뢰할 수 있고 영향력 있는 광고를 통해 개방형 인터넷을 통해 모든 소비자에게 더 풍부한 경험을 제공할 수 있도록 지원합니다. 세계 최대 규모의 상거래 데이터 세트와 동급 최고의 AI를 갖춘 Criteo는 쇼핑 여정의 각 접점이 적절한 시간에 적절한 광고를 통해 고객에게 도달하도록 개인화되도록 보장합니다.
exl-id: e6f394b2-ab82-47bb-8521-1cf9d01a203b
source-git-commit: 1ed82798125f32fe392f2a06a12280ac61f225c6
workflow-type: tm+mt
source-wordcount: '1010'
ht-degree: 3%

---

# (베타) 크리테오 연결

## 개요 {#overview}

>[!IMPORTANT]
>
>이 대상 커넥터 및 설명서 페이지는 Criteo에서 만들고 유지 관리합니다. 현재 베타 제품이며 기능은 변경될 수 있습니다. 문의 사항이나 업데이트 요청은 크리테오에게 직접 문의하십시오 [여기](mailto:criteoTechnicalPartnerships@criteo.com).

크리테오는 신뢰할 수 있고 영향력 있는 광고를 통해 개방형 인터넷을 통해 모든 소비자에게 더 풍부한 경험을 제공할 수 있도록 지원합니다. 세계 최대 규모의 상거래 데이터 세트와 동급 최고의 AI를 갖춘 Criteo는 쇼핑 여정의 각 접점이 적절한 시간에 적절한 광고를 통해 고객에게 도달하도록 개인화되도록 보장합니다.

## 사전 요구 사항 {#prerequisites}

* 다음에 대한 관리자 사용자 계정이 있어야 합니다. [크리테오 관리 센터](https://marketing.criteo.com).
* Criteo 광고주 ID가 필요합니다(이 ID가 없는 경우 Criteo 담당자에게 문의).
* 다음을 제공해야 합니다. [!DNL GUM caller ID]를 사용하려는 경우 [!DNL GUM ID] 식별자로 사용됩니다.

## 제한 사항 {#limitations}

* 크리테오는 [!DNL SHA-256]해시된 일반 텍스트 이메일(변환 대상: [!DNL SHA-256] 보내기 전). PII(개인 이름 또는 전화 번호와 같은 개인 식별 정보)는 보내지 마십시오.
* Criteo는 클라이언트가 제공할 식별자가 하나 이상 필요합니다. 우선 순위 [!DNL GUM ID] 더 나은 일치율에 기여하므로 해시된 이메일에 대한 식별자로.

![전제 조건](../../assets/catalog/advertising/criteo/prerequisites.png)

## 지원되는 ID {#supported-identities}

크리터는 아래 표에 설명된 ID 활성화를 지원합니다. 자세히 알아보기 [id](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| TARGET ID | 설명 | 고려 사항 |
| --- | --- | --- |
| `email_sha256` | SHA-256 알고리즘으로 해시된 이메일 주소 | Adobe Experience Platform은 일반 텍스트와 SHA-256 해시 이메일 주소를 모두 지원합니다. 소스 필드에 해시되지 않은 속성이 포함된 경우 [!UICONTROL 변환 적용] 활성화 시 플랫폼이 데이터를 자동으로 해시하도록 하는 옵션입니다. |
| `gum_id` | 크리테오 [!DNL GUM] 쿠키 식별자 | [!DNL GUM IDs] 클라이언트가 사용자 식별 시스템과 크리터의 사용자 식별([!DNL UID]). 식별자 유형이 다음과 같은 경우 `gum_id`, 추가 매개 변수, [!DNL GUM Caller ID]도 포함되어야 합니다. 해당하는 경우 Criteo 계정 팀에 문의하십시오 [!DNL GUM Caller ID] 또는 이에 대한 자세한 내용을 보려면 [!DNL GUM ID] 필요한 경우 동기화합니다. |

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
| --- | --- | --- |
| 내보내기 유형 | 대상자 내보내기 | 에 사용된 식별자(이름, 전화번호 또는 기타)를 사용하여 대상자의 모든 구성원을 내보냅니다. [!DNL Criteo] 대상. |
| 내보내기 빈도 | 스트리밍 | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. 자세한 내용 [스트리밍 대상](../../destination-types.md#streaming-destinations). |

## 사용 사례 {#use-cases}

을(를) 사용하는 방법을 더 잘 이해할 수 있도록 [!DNL Criteo] 대상: 다음은 Adobe Experience Platform 고객이 달성할 수 있는 몇 가지 목표입니다. [!DNL Criteo]:

### 사용 사례 1 : 트래픽 가져오기

관련 제품 오퍼와 유연한 크리에이티브를 통해 비즈니스를 선보일 수 있습니다. 지능형 제품 추천을 사용하면 광고는 방문 및 참여를 트리거할 가능성이 가장 높은 제품을 자동으로 표시합니다. 유연한 타깃팅을 사용하면 Criteo의 상거래 데이터 세트 또는 고유한 잠재 고객 목록 및 Adobe CDP 세그먼트에서 대상을 구축할 수 있습니다.

### 사용 사례 2 : 웹 사이트 전환 증가

방문자가 웹 사이트를 떠날 때 다음 위치에 관계없이 특별 거래와 매우 연관성 있는 오퍼를 표시하여 전환을 늘리는 리타겟팅 광고에서 누락된 내용을 상기하십시오. Adobe CDP 대상을 연결하여 기존 고객을 다시 참여시키거나 가장 충성도가 높은 쇼핑객과 유사한 소비자를 타겟팅합니다.

## 크리테오에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

이 대상에 연결하려면 다음과같이 하십시오. [대상 구성 자습서](../../ui/connect-destination.md).

### 크리테오 인증

연결하는 단계는 다음과 같습니다.

1. Adobe Experience Platform에 로그인하고 Criteo 대상에 연결합니다.

   ![로그인합니다](../../assets/catalog/advertising/criteo/connect-destination.png)

1. 연결을 승인하려면 Criteo로 리디렉션됩니다. 먼저 크리테오 자격 증명으로 로그인해야 할 수 있습니다.

   ![크리테오 로그인](../../assets/catalog/advertising/criteo/log-in-1.png)

   ![크리테오 로그인](../../assets/catalog/advertising/criteo/log-in-2.png)

   ![크리테오 로그인](../../assets/catalog/advertising/criteo/log-in-3.png)


### 연결 매개 변수 {#connection-parameters}

대상에 인증한 후 다음 연결 매개 변수를 입력하십시오.

![연결 매개 변수](../../assets/catalog/advertising/criteo/connection-parameters.png)

| 필드 | 설명 | 필수 여부 |
| --- | --- | --- |
| 이름 | 나중에 이 대상을 인식하는 데 도움이 되는 이름입니다. 여기에서 선택한 이름은 다음과 같습니다. [!DNL Audience] 크리테오 관리 센터의 이름이며 이후 단계에서 수정할 수 없습니다. | 예 |
| 설명 | 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다. | 아니요 |
| 광고주 ID | 조직의 크리테오 광고주 ID. 이 정보를 얻으려면 크리터 계정 관리자에게 문의하십시오. | 예 |
| 크리테오 [!DNL GUM caller ID] | [!DNL GUM Caller ID] 조직의. 해당하는 경우 Criteo 계정 팀에 문의하십시오 [!DNL GUM Caller ID] 또는 이에 대한 자세한 내용을 보려면 [!DNL GUM] 필요한 경우 동기화합니다. | 예, 언제든지 [!DNL GUM ID] 는 식별자로 제공됩니다 |

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 다음 안내서를 참조하십시오. [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보를 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.

## 이 대상에 대상자 활성화 {#activate-segments}

>[!IMPORTANT]
> 
>데이터를 활성화하려면 **[!UICONTROL 대상 관리]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

읽기 [스트리밍 대상자 내보내기 대상으로 프로필 및 대상자 활성화](../../ui/activate-segment-streaming-destinations.md) 이 대상에 대한 대상자 활성화에 대한 지침을 참조하십시오.

## 내보낸 데이터 {#exported-data}

내보낸 대상자는 [크리테오 관리 센터](https://marketing.criteo.com/audience-manager/dashboard).

에 의해 수신된 사용자 프로필 추가에 대한 요청 본문 [!DNL Criteo] 연결은 다음과 유사합니다.

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

에 의해 수신된 사용자 프로필 제거의 요청 본문 [!DNL Criteo] 연결은 다음과 유사합니다.

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

## 데이터 사용 및 관리 {#data-usage}

모든 Adobe Experience Platform 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. Adobe Experience Platform에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=ko-KR).

## 추가 리소스

* [크리테오 도움말 센터](https://help.criteo.com/kb/en)
* [크리테오 개발자 포털](https://developers.criteo.com)
