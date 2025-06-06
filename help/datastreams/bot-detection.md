---
title: 데이터스트림에 대한 보트 탐지 구성
description: 사람 트래픽과 사람 트래픽을 구분하기 위해 데이터스트림에 대한 봇 탐지를 구성하는 방법에 대해 알아봅니다.
exl-id: 6b221d97-0145-4d3e-a32d-746d72534add
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '1359'
ht-degree: 0%

---

# 데이터스트림에 대한 보트 탐지 구성

자동화된 프로그램, 웹 스크레이퍼, 스파이더 및 스크립팅된 스캐너로부터의 비사람 트래픽은 사람 방문자로부터 발생하는 이벤트를 식별하는 것을 어렵게 할 수 있습니다. 이 유형의 트래픽은 중요한 비즈니스 지표에 부정적인 영향을 주어 잘못된 트래픽 보고를 초래할 수 있습니다.

보트 검색을 사용하면 [Web SDK](../web-sdk/home.md), [Mobile SDK](https://developer.adobe.com/client-sdks/home/) 및 [[!DNL Edge Network API]](https://developer.adobe.com/data-collection-apis/docs/api/)에서 생성된 이벤트를 알려진 스파이더 및 보트에서 생성된 이벤트로 식별할 수 있습니다.

데이터스트림에 대한 보트 감지를 구성하여 특정 IP 주소, IP 범위 및 요청 헤더를 식별하여 보트 이벤트로 분류할 수 있습니다. 이렇게 하면 사이트 또는 모바일 애플리케이션에서 사용자 활동을 보다 정확하게 측정할 수 있습니다.

Edge Network에 대한 요청이 보트 감지 규칙과 일치하는 경우, XDM 스키마는 아래와 같이 보트 점수로 업데이트됩니다(항상 1로 설정됨).

```json
{
  "botDetection": {
    "score": 1
  }
}
```

이 보트 점수는 요청을 받는 솔루션이 보트 트래픽을 올바르게 식별하는 데 도움이 됩니다.

>[!IMPORTANT]
>
>보트 감지는 보트 요청을 삭제하지 않습니다. 보트 채점을 사용하여 XDM 스키마만 업데이트하고 이벤트를 구성한 [데이터스트림 서비스](configure.md)에 전달합니다.
>
>Adobe 솔루션은 다양한 방식으로 봇 점수를 처리할 수 있습니다. 예를 들어 Adobe Analytics은 자체 [보트 필터링 서비스](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/bot-removal/bot-rules.html?lang=ko)를 사용하며 Edge Network에서 설정한 점수를 사용하지 않습니다. 두 서비스는 동일한 [IAB 보트 목록](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/)을 사용하므로 보트 점수는 동일합니다.

보트 감지 규칙은 만들어진 후 Edge Network을 통해 전파되는 데 최대 15분이 걸릴 수 있습니다.

## 전제 조건 {#prerequisites}

데이터 스트림에서 봇 탐지가 작동하려면 **[!UICONTROL 봇 탐지 정보]** 필드 그룹을 스키마에 추가해야 합니다. 스키마에 필드 그룹을 추가하는 방법에 대해 알아보려면 [XDM 스키마](../xdm/ui/resources/schemas.md#add-field-groups) 설명서를 참조하세요.

## 데이터스트림에 대한 보트 탐지 구성 {#configure}

데이터 스트림 구성을 만든 후 보트 검색을 구성할 수 있습니다. [데이터 스트림을 만들고 구성](configure.md)하는 방법에 대한 설명서를 참조한 다음 아래 지침에 따라 데이터 스트림에 봇 감지 기능을 추가하십시오.

데이터 스트림 목록으로 이동하여 보트 검색을 추가할 데이터 스트림을 선택합니다.

![데이터스트림 목록을 표시하는 데이터스트림 사용자 인터페이스](assets/bot-detection/datastream-list.png)

데이터 스트림 세부 정보 페이지에서 오른쪽 레일의 **[!UICONTROL 보트 검색]** 옵션을 선택합니다.

![데이터 스트림 사용자 인터페이스에서 강조 표시된 봇 검색 옵션입니다.](assets/bot-detection/bot-detection.png)

**[!UICONTROL 보트 검색 규칙]** 페이지가 표시됩니다.

![데이터 스트림 설정 페이지의 보트 검색 설정.](assets/bot-detection/bot-detection-page.png)

[보트 탐지 규칙] 페이지에서 다음 기능을 사용하여 보트 탐지를 구성할 수 있습니다.

* [[!DNL [IAB/ABC International Spiders and Bots List]]](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/) 사용 중.
* 보트 감지 규칙을 만듭니다.

### IAB/ABC International Spiders and Bots List 사용 {#iab-list}

[IAB/ABC International Spiders and Bots List](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/)은(는) 타사의 산업 표준 인터넷 스파이더 및 보트 목록입니다. 이 목록은 검색 엔진 크롤러, 모니터링 도구 및 분석 횟수에 포함하지 않으려는 기타 비인적 트래픽과 같은 자동화된 트래픽을 식별하는 데 도움이 됩니다.

IAB/ABC International Spiders and Bots List를 사용하도록 데이터 스트림을 구성하려면 다음을 수행하십시오.

1. **[!UICONTROL 이 데이터 스트림에서 보트 감지를 위해 IAB/ABC International Spiders and Bots List 사용]** 옵션을 전환합니다.
2. 보트 검색 설정을 데이터 스트림에 적용하려면 **[!UICONTROL 저장]**&#x200B;을 선택하십시오.

![IAB 스파이더 및 보트 목록을 사용할 수 있습니다.](assets/bot-detection/bot-detection-list.png)

### 보트 탐지 규칙 만들기 {#rules}

[IAB/ABC International Spiders and Bots List](https://www.iab.com/guidelines/iab-abc-international-spiders-bots-list/)을(를) 사용하는 것 외에도 각 데이터 스트림에 대해 고유한 보트 감지 규칙을 정의할 수 있습니다.

**IP 주소** 및 **IP 주소 범위**&#x200B;를 기반으로 봇 검색 규칙을 만들 수 있습니다.

보다 세분화된 보트 탐지 규칙이 필요한 경우 IP 조건을 요청 헤더 조건과 결합할 수 있습니다. 보트 탐지 규칙은 다음 헤더를 사용할 수 있습니다.

| HTTP 헤더 | 설명 |
| --- | --- |
| `user-agent` | 서버 및 네트워크 피어가 요청한 사용자 에이전트의 애플리케이션, 운영 체제, 공급업체 및/또는 버전을 식별할 수 있도록 해주는 헤더입니다. |
| `content-type` | 리소스의 원래 미디어 유형을 나타냅니다(컨텐츠 인코딩이 전송되기 전). |
| `referer` | 리소스를 요청한 웹 페이지의 주소를 식별합니다. |
| `sec-ch-ua` | 브라우저와 연결된 각 브랜드의 브랜드 및 중요 버전을 쉼표로 구분된 목록으로 제공합니다. |
| `sec-ch-ua-mobile` | 브라우저가 모바일 장치에 있는지 여부를 나타냅니다. 데스크탑 브라우저에서 모바일 사용자 경험에 대한 기본 설정을 나타내는 데 사용할 수도 있습니다. |
| `sec-ch-ua-platform` | 사용자 에이전트가 실행 중인 플랫폼 또는 운영 체제를 제공합니다. 예: &quot;Windows&quot; 또는 &quot;Android&quot;. |
| `sec-ch-ua-platform-version` | 사용자 에이전트가 실행 중인 운영 체제의 버전을 제공합니다. |
| `sec-ch-ua-arch` | ARM 또는 x86과 같은 사용자 에이전트의 기본 CPU 아키텍처를 제공합니다. |
| `sec-ch-ua-model` | 브라우저가 실행 중인 디바이스 모델을 나타냅니다. |
| `sec-ch-ua-bitness` | 사용자 에이전트의 기본 CPU 아키텍처에 대한 &quot;비트율&quot;을 제공합니다. 이는 정수 또는 메모리 주소의 비트 단위 크기이며, 일반적으로 64 또는 32비트입니다. |
| `sec-ch-ua-wow64` | 사용자 에이전트 바이너리가 64비트 Windows에서 32비트 모드로 실행 중인지 여부를 나타냅니다. |

보트 탐지 규칙을 만들려면 아래 단계를 수행하십시오.

1. **[!UICONTROL 새 규칙 추가]**&#x200B;를 선택합니다.

   새 규칙 추가 단추가 강조 표시된 ![보트 검색 설정 화면입니다.](assets/bot-detection/bot-detection-new-rule.png)

2. **[!UICONTROL 규칙 이름]** 필드에 규칙 이름을 입력하십시오.

   ![규칙 이름이 강조 표시된 보트 검색 규칙 화면](assets/bot-detection/rule-name.png)

3. 새 IP 기반 규칙을 추가하려면 **[!UICONTROL 새 IP 조건 추가]**&#x200B;를 선택하십시오. IP 주소 또는 IP 주소 범위별로 규칙을 정의할 수 있습니다.

   ![IP 주소 필드가 강조 표시된 봇 검색 규칙 화면입니다.](assets/bot-detection/ip-address-rule.png)

   ![IP 범위 필드가 강조 표시된 봇 검색 규칙 화면입니다.](assets/bot-detection/ip-range-rule.png)

   >[!TIP]
   >
   >IP 조건은 논리 `OR` 작업을 기반으로 합니다. 정의한 IP 조건 중 하나와 일치하는 경우 요청이 봇에서 시작된 것으로 표시됩니다.

4. 규칙에 헤더 조건을 추가하려면 **[!UICONTROL 헤더 조건 그룹 추가]**&#x200B;를 선택한 다음 규칙이 사용할 헤더를 선택하십시오.

   헤더 조건이 강조 표시된 ![보트 검색 규칙 화면입니다.](assets/bot-detection/header-conditions.png)

   그런 다음 선택한 헤더에 사용할 조건을 추가합니다.

   헤더 조건이 강조 표시된 ![보트 검색 규칙 화면입니다.](assets/bot-detection/header-condition-rule.png)

5. 원하는 보트 검색 규칙을 구성한 후 **[!UICONTROL 저장]**&#x200B;을 선택하여 데이터 스트림에 규칙을 적용합니다.

   헤더 조건이 강조 표시된 ![보트 검색 규칙 화면입니다.](assets/bot-detection/bot-detection-save.png)


## 보트 탐지 규칙 예 {#examples}

보트 감지를 시작하는 데 도움이 되도록 아래 설명된 예를 사용하여 보트 감지 규칙을 만들 수 있습니다.

### 하나의 IP 주소를 기반으로 한 보트 감지 {#one-ip}

특정 IP 주소에서 발생하는 모든 요청을 보트 트래픽으로 표시하려면 아래 이미지에 표시된 대로 단일 IP 주소를 평가하는 새 보트 감지 규칙을 만듭니다.

![하나의 IP 주소를 기반으로 하는 봇 검색 규칙입니다.](assets/bot-detection/bot-detection-one-ip.png)

### 두 개의 IP 주소를 기반으로 한 보트 감지 {#two-ip}

두 개의 특정 IP 주소 중 하나에서 발생하는 모든 요청을 보트 트래픽으로 표시하려면 아래 이미지에 표시된 대로 두 개의 IP 주소를 평가하는 새 보트 감지 규칙을 만듭니다.

![두 IP 주소를 기반으로 하는 보트 검색 규칙](assets/bot-detection/bot-detection-two-ips.png)

### IP 주소 범위를 기반으로 한 보트 감지 {#range}

특정 범위의 IP 주소에서 발생하는 모든 요청을 보트 트래픽으로 표시하려면 아래 이미지에 표시된 대로 전체 IP 주소 범위를 평가하는 새 보트 감지 규칙을 만듭니다.

![IP 범위를 기반으로 하는 보트 검색 규칙](assets/bot-detection/bot-detection-range.png)

### IP 주소 및 요청 헤더를 기반으로 한 보트 탐지 {#ip-header}

특정 IP 주소에서 시작되고 특정 요청 헤더를 봇 트래픽으로 포함하는 모든 요청을 표시하려면 아래 이미지에 표시된 대로 새 봇 탐지 규칙을 만듭니다.

이 규칙은 요청이 특정 IP 주소에서 발생하는지, `referer` 요청 헤더가 `www.adobe.com`(으)로 시작하는지 확인합니다.

![IP 주소 및 요청 헤더를 기반으로 한 봇 검색 규칙입니다.](assets/bot-detection/bot-detection-header-ip.png)

### 여러 조건을 기반으로 한 보트 감지 {#multiple-conditions}

다음을 기반으로 보트 탐지 규칙을 만들 수 있습니다.

* **여러 다른 조건**: 다른 조건은 논리 `AND` 작업으로 평가됩니다. 즉, 요청이 봇에서 시작된 것으로 식별되려면 조건이 동시에 충족되어야 합니다.
* **같은 형식의 여러 조건**: 같은 형식의 조건은 논리 `OR` 작업으로 평가됩니다. 즉, 조건이 하나라도 충족되면 요청이 봇에서 시작된 것으로 식별됩니다.

아래 이미지에 표시된 규칙은 다음 조건이 충족되는 경우 봇 발생 요청을 식별합니다.

요청은 두 IP 주소 중 하나에서 시작되며, `referer` 헤더는 `www.adobe.com`(으)로 시작되고, `sec-ch-ua-mobile` 헤더는 요청을 데스크톱 브라우저에서 시작한 것으로 식별합니다.

![여러 조건을 기반으로 하는 보트 검색 규칙입니다.](assets/bot-detection/bot-detection-multiple.png)
