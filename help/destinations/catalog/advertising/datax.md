---
title: Verizon MediaYahoo DataX 연결
description: DataX는 Verizon Media/Yahoo가 안전하고 자동화된 확장 가능한 방식으로 외부 파트너와 데이터를 교환할 수 있도록 하는 다양한 구성 요소를 호스팅하는 종합적인 Verizon Media/Yahoo 인프라입니다.
exl-id: 7d02671d-8650-407d-9c9f-fad7da3156bc
source-git-commit: b1945d42b82b549985d848071762fa6ee2451368
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 3%

---

# Verizon Media/Yahoo DataX 연결

## 개요 {#overview}

DataX는 Verizon Media/Yahoo가 안전하고 자동화된 확장 가능한 방식으로 외부 파트너와 데이터를 교환할 수 있도록 하는 다양한 구성 요소를 호스팅하는 종합적인 Verizon Media/Yahoo 인프라입니다.

>[!IMPORTANT]
>
>이 설명서 페이지는 Verizon Media/Yahoo의 DataX 팀이 작성했습니다. 문의 사항이나 업데이트 요청에 대해서는 [dataops@verizonmedia.com](mailto:dataops@verizonmedia.com)

## 전제 조건 {#prerequisites}

**MDM ID**

Yahoo DataX의 고유 식별자이며, 이 대상에 데이터 내보내기를 설정하기 위한 필수 필드입니다. 이 ID를 모르는 경우 Yahoo Data X 계정 관리자에게 문의하십시오.

**비율 제한**

DataX는 [DataX 설명서](https://developer.verizonmedia.com/datax/guide/rate-limits/).


| 오류 코드 | 오류 메시지 | 설명 |
|---------|----------|---------|
| 429 너무 많은 요청 | 시간당 비율 제한이 초과됨 **(제한: 100)** | 공급자당 1시간에 허용되는 요청 수입니다. |

{style=&quot;table-layout:auto&quot;}

**분류 메타데이터**

분류 리소스는 기본 DataX 메타데이터 구조에 대한 확장을 정의합니다

```
{

  >>(Base DataX Metadata)<<

        "extensions": { "action":
        {string}, "incrementalData":
        {
                "taxonomyId": {string}
                },
                "links": [{
                "rel": "https://datax.yahooapis.com/rels/fullTaxonomy", "title": "Full
                Taxonomy post processing",
                "href": {string}
                ]
        }
}
```

자세한 내용 [분류 메타데이터](https://developer.verizonmedia.com/datax/guide/taxonomy/taxo-metadata/) ( DataX 개발자 설명서) 를 참조하십시오.

## 지원되는 ID {#supported-identities}

Verizon Media는 아래 표에 설명된 ID 활성화를 지원합니다. 추가 정보 [id](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started).

| Target ID | 설명 | 고려 사항 |
|---|---|---|
| email_lc_sha256 | SHA256 알고리즘을 사용하여 해시된 이메일 주소 | 일반 텍스트와 SHA256 해시된 이메일 주소는 모두 Adobe Experience Platform에서 지원합니다. 소스 필드에 해시되지 않은 속성이 포함되어 있으면 **[!UICONTROL 변형 적용]** 옵션, [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다. |
| GAID | Google 광고 ID | 소스 ID가 GAID 네임스페이스이면 GAID 대상 ID를 선택합니다. |
| IDFA | 광고주용 Apple ID | 소스 ID가 IDFA 네임스페이스인 경우 IDFA 대상 ID를 선택합니다. |

{style=&quot;table-layout:auto&quot;}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 세그먼트 내보내기]** | Verizon Media 대상에 사용되는 식별자(이메일, GAID, IDFA)를 사용하여 세그먼트(대상)의 모든 구성원을 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상 설정&quot; API 기반 연결입니다. 세그먼트 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터는 업데이트 다운스트림을 대상 플랫폼으로 보냅니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## 사용 사례 {#use-cases}

DataX API는 VMG(Verizon Media)에서 이메일 주소를 키로 사용하는 특정 대상 그룹을 타겟팅하려는 광고주가 VMG의 근실시간 API를 사용하여 새로운 세그먼트를 신속하게 생성하고 원하는 대상 그룹을 푸시할 수 있습니다.

## 대상에 연결 {#connect}

![Platform UI의 Yahoo DataX 대상 카드](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md).

### 연결 매개 변수 {#parameters}

While [설정](../../ui/connect-destination.md) 이 대상을 사용하려면 다음 정보를 제공해야 합니다.

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식하는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL MDM ID]**: Yahoo DataX의 고유 식별자이며, 이 대상에 데이터 내보내기를 설정하기 위한 필수 필드입니다. 이 ID를 모르는 경우 Yahoo Data X 계정 관리자에게 문의하십시오.  MDM ID를 사용하면 특정 전용 사용자 집합(예: 광고주를 위한 자사 데이터)에서만 데이터를 사용하도록 제한할 수 있습니다.

## 세그먼트를 이 대상에 활성화 {#activate}

읽기 [대상에 프로필 및 세그먼트 활성화](../../ui/activate-segment-streaming-destinations.md) 대상 세그먼트를 대상으로 활성화하는 방법에 대한 지침입니다.

## 데이터 사용 및 거버넌스 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스를 적용하는 경우 다음을 참조하십시오. [데이터 거버넌스 개요](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

## 추가 리소스 {#additional-resources}

자세한 내용은 Yahoo/Verizon Media 를 참조하십시오 [dataX에 대한 설명서](https://developer.verizonmedia.com/datax/guide/).
