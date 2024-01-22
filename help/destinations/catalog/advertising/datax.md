---
title: Verizon MediaYahoo DataX 연결
description: DataX는 Verizon Media/Yahoo가 안전하고 자동화된 확장 가능한 방식으로 외부 파트너와 데이터를 교환할 수 있도록 하는 다양한 구성 요소를 호스팅하는 Verizon Media/Yahoo 인프라의 집합체입니다.
exl-id: 7d02671d-8650-407d-9c9f-fad7da3156bc
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 2%

---

# [!DNL Verizon Media/Yahoo DataX] 연결

## 개요 {#overview}

[!DNL DataX] 집계입니다. [!DNL Verizon Media/Yahoo] 을 활성화하는 다양한 구성 요소를 호스팅하는 인프라 [!DNL Verizon Media/Yahoo] 안전하고 자동화된 확장 방식으로 외부 파트너와 데이터를 교환할 수 있습니다.

>[!IMPORTANT]
>
>이 대상 커넥터 및 설명서 페이지는 다음 방법으로 만들고 유지 관리됩니다. [!DNL Verizon Media/Yahoo]의 [!DNL DataX] 팀. 문의 사항이나 업데이트 요청은 다음 주소로 직접 문의하십시오. [dataops@verizonmedia.com](mailto:dataops@verizonmedia.com)

## 전제 조건 {#prerequisites}

**MDM ID**

의 고유 식별자입니다. [!DNL Yahoo DataX] 또한 이 대상에 대한 데이터 내보내기를 설정하는 필수 필드입니다. 이 ID를 모를 경우 다음으로 문의하십시오. [!DNL Yahoo DataX] 계정 관리자.

**분류 메타데이터**

분류 리소스는 기본 위의 확장을 정의합니다 [!DNL DataX] 메타데이터 구조

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

자세한 내용 [분류 메타데이터](https://developer.verizonmedia.com/datax/guide/taxonomy/taxo-metadata/) 다음에서 [!DNL DataX] 개발자 설명서.

## 등급 제한 및 보호 {#rate-limits-guardrails}

>[!IMPORTANT]
>
>100개 이상의 대상을 활성화할 때 다음이 수행됩니다. [!DNL Verizon Media/Yahoo DataX], 대상에서 속도 제한 오류를 수신할 수 있습니다. 이 대상에 대한 대상을 활성화할 때 하나의 활성화 데이터 흐름에서 100개 미만의 대상을 활성화해 보십시오. 더 많은 세그먼트를 활성화해야 하는 경우 동일한 계정에 새 대상을 만듭니다.

[!DNL DataX] 은(는) 다음에 요약된 분류법 및 대상자 게시물에 대한 할당량 제한에 따라 비율이 제한됩니다. [DataX 설명서](https://developer.verizonmedia.com/datax/guide/rate-limits/).


| 오류 코드 | 오류 메시지 | 설명 |
|---------|----------|---------|
| 429 요청이 너무 많음 | 시간당 요금 한도 초과 **(제한: 100)** | 공급자당 허용된 요청 수(시간)입니다. |

{style="table-layout:auto"}

## 지원되는 ID {#supported-identities}

[!DNL Verizon Media] 는 아래 표에 설명된 id 활성화를 지원합니다. 자세히 알아보기 [id](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html#getting-started).

| 대상 ID | 설명 | 고려 사항 |
|---|---|---|
| email_lc_sha256 | SHA256 알고리즘으로 해시된 이메일 주소 | Adobe Experience Platform은 일반 텍스트와 SHA256 해시 이메일 주소를 모두 지원합니다. 소스 필드에 해시되지 않은 속성이 포함된 경우 **[!UICONTROL 변환 적용]** 옵션, 보유 [!DNL Platform] 활성화 시 데이터를 자동으로 해시합니다. |
| GAID | Google 광고 ID | 소스 ID가 GAID 네임스페이스인 경우 GAID 대상 ID를 선택합니다. |
| IDFA | 광고주용 Apple ID | 소스 ID가 IDFA 네임스페이스인 경우 IDFA 대상 ID를 선택합니다. |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 대상자 내보내기]** | Verizon Media 대상에 사용된 식별자(이메일, GAID, IDFA)로 대상자의 모든 구성원을 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. 대상자 평가를 기반으로 Experience Platform에서 프로필이 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. 자세한 내용 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## 사용 사례 {#use-cases}

[!DNL DataX] API는 이메일 주소를 키로 사용하는 특정 대상 그룹을 타깃팅하려는 광고주가 사용할 수 있습니다. [!DNL Verizon Media] (VMG)는 VMG의 실시간에 가까운 API를 사용하여 빠르게 새 대상을 만들고 원하는 대상 그룹을 푸시할 수 있습니다.

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 다음이 필요합니다. **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.

![Platform UI의 Yahoo DataX 대상 카드](/help/destinations/assets/catalog/advertising/yahoo-datax/catalog.png)

이 대상에 연결하려면 다음과같이 하십시오. [대상 구성 자습서](../../ui/connect-destination.md).

### 연결 매개변수 {#parameters}

While [설정 중](../../ui/connect-destination.md) 이 대상에는 다음 정보를 제공해야 합니다.

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL MDM ID]**: 의 고유 식별자입니다. [!DNL Yahoo DataX] 또한 이 대상에 대한 데이터 내보내기를 설정하는 필수 필드입니다. 이 ID를 모를 경우 다음으로 문의하십시오. [!DNL Yahoo DataX] 계정 관리자.  MDM ID를 사용하면 특정 전용 사용자 세트(예: 광고주를 위한 자사 데이터)에서만 데이터를 사용하도록 제한할 수 있습니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 다음 안내서를 참조하십시오. [UI를 사용하여 대상 경고 구독](../../ui/alerts.md).

대상 연결에 대한 세부 정보를 제공했으면 을 선택합니다. **[!UICONTROL 다음]**.

## 이 대상으로 대상자 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]**, 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). 읽기 [액세스 제어 개요](/help/access-control/ui/overview.md) 필요한 권한을 얻으려면 제품 관리자에게 문의하십시오.
>* 내보내려면 *id*, 다음이 필요합니다. **[!UICONTROL ID 그래프 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions). <br> ![워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다.](/help/destinations/assets/overview/export-identities-to-destination.png "워크플로우에서 강조 표시된 ID 네임스페이스를 선택하여 대상에 대한 대상자를 활성화합니다."){width="100" zoomable="yes"}

읽기 [대상에 대한 프로필 및 대상자 활성화](../../ui/activate-segment-streaming-destinations.md) 대상을 대상으로 활성화하는 방법에 대한 지침을 참조하십시오.

## 데이터 사용 및 관리 {#data-usage-governance}

모두 [!DNL Adobe Experience Platform] 대상은 데이터를 처리할 때 데이터 사용 정책을 준수합니다. 방법에 대한 자세한 정보 [!DNL Adobe Experience Platform] 데이터 거버넌스 시행, 다음을 참조하십시오. [데이터 거버넌스 개요](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=ko).

## 추가 리소스 {#additional-resources}

자세한 내용은 [!DNL Yahoo/Verizon Media] [설명서 [!DNL DataX]](https://developer.verizonmedia.com/datax/guide/).
