---
title: Verizon MediaYahoo DataX 통합
description: DataX는 Verizon Media/Yahoo가 안전하고 자동화된 확장 가능한 방식으로 외부 파트너와 데이터를 교환할 수 있도록 하는 다양한 구성 요소를 호스팅하는 종합적인 Verizon Media/Yahoo 인프라입니다.
source-git-commit: 07c8a7afaf6cd2af249ad52eabfbc5f8cd6689ae
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 2%

---


# Verizon Media/Yahoo DataX

## 개요 {#overview}

DataX는 Verizon Media/Yahoo가 안전하고 자동화된 확장 가능한 방식으로 외부 파트너와 데이터를 교환할 수 있도록 하는 다양한 구성 요소를 호스팅하는 종합적인 Verizon Media/Yahoo 인프라입니다.

>[!IMPORTANT]
>
>이 설명서 페이지는 Verizon Media/Yahoo의 DataX 팀이 작성했습니다. 문의 사항이나 업데이트 요청은 [dataops@verizonmedia.com](mailto:dataops@verizonmedia.com)에서 직접 문의하십시오

## 전제 조건 {#prerequisites}

**MDM ID**

Yahoo DataX의 고유 식별자이며, 이 대상에 데이터 내보내기를 설정하기 위한 필수 필드입니다. 이 ID를 모르는 경우 Yahoo Data X 계정 관리자에게 문의하십시오.

**비율 제한**

DataX는 [DataX 설명서](https://developer.verizonmedia.com/datax/guide/rate-limits/)에 요약된 분류 및 대상 게시물에 대한 할당량 제한에 따라 속도가 제한됩니다.


| 오류 코드 | 오류 메시지 | 설명 |
|---------|----------|---------|
| 429 너무 많은 요청 | 비율 제한이 시간당 **(제한: 100)** | 공급자당 1시간에 허용되는 요청 수입니다. |

{style=&quot;table-layout:auto&quot;}

**분류 메타데이터**

분류 리소스는 기본 DataX 메타데이터 구조에 대한 확장을 정의합니다

```
{

  >>(Base DataX Metadata)<<

        "extensions" : { "action" :
        {string}, "incrementalData" :
        {
                "taxonomyId": {string}
                },
                "links" : [{
                "rel"   : "https://datax.yahooapis.com/rels/fullTaxonomy", "title" : "Full
                Taxonomy post processing",
                "href": {string}
                ]
        }
}
```

DataX 개발자 설명서에서 [분류 메타데이터](https://developer.verizonmedia.com/datax/guide/taxonomy/taxo-metadata/)에 대해 자세히 알아보십시오.

## 지원되는 ID {#supported-identities}

Verizon Media는 아래 표에 설명된 ID 활성화를 지원합니다. [id](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=en#getting-started)에 대해 자세히 알아보십시오.

| Target ID | 설명 | 고려 사항 |
|---|---|---|
| email_lc_sha256 | SHA256 알고리즘을 사용하여 해시된 이메일 주소 | 일반 텍스트와 SHA256 해시된 이메일 주소는 모두 Adobe Experience Platform에서 지원합니다. 소스 필드에 해시되지 않은 특성이 들어 있는 경우 **[!UICONTROL 변환]** 적용 옵션을 선택하여 [!DNL Platform]에서 활성화 시 데이터를 자동으로 해시하도록 하십시오. |
| GAID | Google 광고 ID | 소스 ID가 GAID 네임스페이스이면 GAID 대상 ID를 선택합니다. |
| IDFA | 광고주용 Apple ID | 소스 ID가 IDFA 네임스페이스인 경우 IDFA 대상 ID를 선택합니다. |

{style=&quot;table-layout:auto&quot;}

## 내보내기 유형 {#export-type}

**세그먼트 내보내기**  - Verizon Media 대상에 사용된 식별자(이메일)를 사용하여 세그먼트(대상)의 모든 구성원을 내보냅니다.

## 사용 사례 {#use-cases}

DataX API는 VMG(Verizon Media)에서 이메일 주소를 키로 사용하는 특정 대상 그룹을 타겟팅하려는 광고주가 VMG의 근실시간 API를 사용하여 새로운 세그먼트를 신속하게 생성하고 원하는 대상 그룹을 푸시할 수 있습니다.

## 대상에 연결 {#connect}

![Platform UI의 Yahoo DataX 대상 카드](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오.

### 연결 매개 변수 {#parameters}

[이 대상을 설정할 때 다음 정보를 제공해야 합니다.](../../ui/connect-destination.md)

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식하는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL MDM ID]**: Yahoo DataX의 고유 식별자이며, 이 대상에 데이터 내보내기를 설정하기 위한 필수 필드입니다. 이 ID를 모르는 경우 Yahoo Data X 계정 관리자에게 문의하십시오.  MDM ID를 사용하면 특정 전용 사용자 집합(예: 광고주를 위한 자사 데이터)에서만 데이터를 사용하도록 제한할 수 있습니다.

## 세그먼트를 이 대상에 활성화 {#activate}

대상으로 대상 세그먼트를 활성화하는 방법에 대한 지침은 [대상](../../ui/activate-segment-streaming-destinations.md)에 프로필 및 세그먼트를 활성화합니다.

## 데이터 사용 및 거버넌스 {#data-usage-governance}

모든 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html)를 참조하십시오.

## 추가 리소스 {#additional-resources}

자세한 내용은 DataX](https://developer.verizonmedia.com/datax/guide/)에 대한 Yahoo/Verizon Media [설명서를 참조하십시오.