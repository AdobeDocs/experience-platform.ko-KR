---
title: Verizon MediaYahoo DataX 연결
description: DataX는 Verizon Media/Yahoo가 안전하고 자동화된 확장 가능한 방식으로 외부 파트너와 데이터를 교환할 수 있도록 하는 다양한 구성 요소를 호스팅하는 Verizon Media/Yahoo 인프라의 집합체입니다.
exl-id: 7d02671d-8650-407d-9c9f-fad7da3156bc
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '934'
ht-degree: 4%

---

# [!DNL Verizon Media/Yahoo DataX] 연결

## 개요 {#overview}

[!DNL DataX]은(는) [!DNL Verizon Media/Yahoo]이(가) 안전하고 자동화된 확장 가능한 방식으로 외부 파트너와 데이터를 교환할 수 있도록 하는 다양한 구성 요소를 호스팅하는 집계 [!DNL Verizon Media/Yahoo] 인프라입니다.

>[!IMPORTANT]
>
>이 대상 커넥터 및 설명서 페이지는 [!DNL Verizon Media/Yahoo]의 [!DNL DataX] 팀에서 만들고 유지 관리합니다. 문의 사항이나 업데이트 요청은 [dataoperations@yahooinc.com](mailto:dataoperations@yahooinc.com)로 직접 문의하십시오.

## 전제 조건 {#prerequisites}

**MDM ID**

[!DNL Yahoo DataX]의 고유 식별자이며 이 대상으로 데이터 내보내기를 설정하는 필수 필드입니다. 이 ID를 모르는 경우 [!DNL Yahoo DataX] 계정 관리자에게 문의하십시오.

**분류 메타데이터**

Taxonomy 리소스는 기본 [!DNL DataX] 메타데이터 구조를 통해 확장을 정의합니다.

```json
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

[ 개발자 설명서에서 ](https://developer.verizonmedia.com/datax/guide/taxonomy/taxo-metadata/)분류 메타데이터[!DNL DataX]에 대해 자세히 알아보십시오.

## 등급 제한 및 보호 {#rate-limits-guardrails}

>[!IMPORTANT]
>
>100명 이상의 대상을 [!DNL Verizon Media/Yahoo DataX]&#x200B;(으)로 활성화할 때 대상에서 속도 제한 오류가 발생할 수 있습니다. 이 대상에 대한 대상을 활성화할 때 하나의 활성화 데이터 흐름에서 100개 미만의 대상을 활성화해 보십시오. 더 많은 세그먼트를 활성화해야 하는 경우 동일한 계정에 새 대상을 만듭니다.

[!DNL DataX]은(는) [DataX 설명서](https://developer.verizonmedia.com/datax/guide/rate-limits/)에 요약된 분류법 및 대상자 게시물에 대한 할당량 제한에 따라 속도가 제한됩니다.


| 오류 코드 | 오류 메시지 | 설명 |
|---------|----------|---------|
| 429 요청이 너무 많음 | 시간당 요금 한도 초과 **(한도: 100)** | 공급자당 허용된 요청 수(시간)입니다. |

{style="table-layout:auto"}

## 지원되는 ID {#supported-identities}

[!DNL Verizon Media]은(는) 아래 표에 설명된 ID 활성화를 지원합니다. [ID](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started)에 대해 자세히 알아보세요.

| 대상 ID | 설명 | 고려 사항 |
|---|---|---|
| email_lc_sha256 | SHA256 알고리즘으로 해시된 이메일 주소 | [!DNL Adobe Experience Platform]은(는) 일반 텍스트와 SHA256 해시된 전자 메일 주소를 모두 지원합니다. 소스 필드에 해시되지 않은 특성이 포함된 경우 **[!UICONTROL Apply transformation]** 옵션을 선택하여 [!DNL Experience Platform]이(가) 활성화 시 데이터를 자동으로 해시하도록 합니다. |
| GAID | GOOGLE ADVERTISING ID | 소스 ID가 GAID 네임스페이스인 경우 GAID 대상 ID를 선택합니다. |
| IDFA | 광고주용 Apple ID | 소스 ID가 IDFA 네임스페이스인 경우 IDFA 대상 ID를 선택합니다. |

{style="table-layout:auto"}

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
|---------|----------|----------|
| [!DNL Segmentation Service] | 예 | Experience Platform [세그먼테이션 서비스](../../../segmentation/home.md)를 통해 생성된 대상입니다. |
| 기타 모든 대상 원본 | 아니요 | 이 범주에는 [!DNL Segmentation Service]을(를) 통해 생성된 대상 외부의 모든 대상 출처가 포함됩니다. [다양한 대상 원본](/help/segmentation/ui/audience-portal.md#customize)에 대해 읽어 보십시오. 예를 들면 다음과 같습니다. <ul><li> CSV 파일에서 Experience Platform으로 사용자 지정 업로드 대상 [가져옴](../../../segmentation/ui/audience-portal.md#import-audience),</li><li> 유사 대상, </li><li> 페더레이션 대상, </li><li> [!DNL Adobe Journey Optimizer]과(와) 같은 다른 Experience Platform 앱에서 생성된 대상, </li><li> 등. </li></ul> |

{style="table-layout:auto"}



대상 데이터 유형별 지원되는 대상:

| 대상 데이터 유형 | 지원됨 | 설명 | 사용 사례 |
|--------------------|-----------|-------------|-----------|
| [사람 대상](/help/segmentation/types/people-audiences.md) | 예 | 고객 프로필을 기반으로 마케팅 캠페인을 위해 특정 사용자 그룹을 타깃팅할 수 있습니다. | 빈번한 구매자, 장바구니 포기 |
| [계정 대상자](/help/segmentation/types/account-audiences.md) | 아니요 | 계정 기반 마케팅 전략을 위해 특정 조직 내의 개인을 타깃팅합니다. | B2B 마케팅 |
| [잠재 고객](/help/segmentation/types/prospect-audiences.md) | 아니요 | 아직 고객이 아니지만 타겟 대상자와 특성을 공유하는 개인을 타겟팅합니다. | 타사 데이터를 이용한 잠재 고객 확보 |
| [데이터 집합 내보내기](/help/catalog/datasets/overview.md) | 아니요 | [!DNL Adobe Experience Platform] 데이터 레이크에 저장된 구조화된 데이터의 컬렉션입니다. | 보고, 데이터 과학 워크플로 |

{style="table-layout:auto"}


## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
|---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL Audience export]** | Verizon Media 대상에 사용된 식별자(이메일, GAID, IDFA)로 대상자의 모든 구성원을 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL Streaming]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 사용 사례 {#use-cases}

[!DNL DataX] API는 [!DNL Verizon Media]&#x200B;(VMG)의 이메일 주소를 키로 사용하는 특정 대상 그룹을 타깃팅하려는 광고주가 사용할 수 있습니다. VMG의 실시간 API를 사용하여 새 대상을 빠르게 만들고 원하는 대상 그룹을 푸시할 수 있습니다.

## 대상에 연결 {#connect}

>[!IMPORTANT]
>
>대상에 연결하려면 **[!UICONTROL View Destinations]** 및 **[!UICONTROL Manage Destinations]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

Experience Platform UI의 ![Yahoo DataX 대상 카드](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오.

### 연결 매개변수 {#parameters}

[이 대상을 설정](../../ui/connect-destination.md)하는 동안 다음 정보를 제공해야 합니다.

* **[!UICONTROL Name]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL Description]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL MDM ID]**: [!DNL Yahoo DataX]의 고유 식별자이며 이 대상으로 데이터 내보내기를 설정하는 필수 필드입니다. 이 ID를 모르는 경우 [!DNL Yahoo DataX] 계정 관리자에게 문의하십시오.  MDM ID를 사용하면 특정 전용 사용자 세트(예: 광고주를 위한 자사 데이터)에서만 데이터를 사용하도록 제한할 수 있습니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 제공했으면 **[!UICONTROL Next]**&#x200B;을(를) 선택합니다.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
>
>* 데이터를 활성화하려면 **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** 및 **[!UICONTROL View Segments]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.
>* *ID*&#x200B;을(를) 내보내려면 **[!UICONTROL View Identity Graph]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. <br> ![대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오.](/help/destinations/assets/overview/export-identities-to-destination.png "대상자를 대상으로 활성화하려면 워크플로에서 강조 표시된 ID 네임스페이스를 선택하십시오."){width="100" zoomable="yes"}

대상을 대상으로 활성화하는 방법에 대한 지침은 [프로필 및 대상을 대상으로 활성화](../../ui/activate-segment-streaming-destinations.md)를 참조하십시오.

## 데이터 사용 및 관리 {#data-usage-governance}

데이터를 처리할 때 모든 [!DNL Adobe Experience Platform] 대상이 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=ko)를 참조하십시오.

## 추가 리소스 {#additional-resources}

자세한 내용은 [!DNL Yahoo/Verizon Media][의  [!DNL DataX] ](https://developer.verizonmedia.com/datax/guide/)설명서를 참조하십시오.
