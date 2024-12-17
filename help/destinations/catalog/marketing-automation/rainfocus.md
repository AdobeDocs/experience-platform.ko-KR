---
title: RainFocus 참가자 프로필
description: RainFocus Attendee Profiles 대상 커넥터를 사용하여 대상 프로필을 RainFocus 전역 Attendee 프로필과 동기화하는 방법에 대해 알아봅니다.
last-substantial-update: 2024-12-17T00:00:00Z
source-git-commit: a3dcf49d3ed9afacd3ffef10d6f280c71ebdf584
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 2%

---


# RainFocus 참가자 프로필 {#rainfocus-destination}

## 개요 {#overview}

[!DNL RainFocus Attendee Profiles] 대상을 사용하여 참석자 프로필을 만들고 업데이트하려면 Adobe Experience Platform에서 [!DNL RainFocus] 플랫폼으로 고객 프로필을 스트리밍하십시오.

>[!IMPORTANT]
>
>대상 커넥터 및 문서 페이지는 [!DNL RainFocus] 팀에서 만들고 유지 관리합니다. 문의 사항이나 업데이트 요청은 `clientcare@rainfocus.com`에서 직접 문의하거나 RainFocus [도움말 센터](https://help.rainfocus.com/hc/en-us)를 방문하십시오.

## 사용 사례 {#use-cases}

RainFocus 대상을 사용하는 방법과 시기를 더 잘 이해할 수 있도록 Adobe Experience Platform 고객이 이 대상을 사용하여 해결할 수 있는 사용 사례를 소개합니다.

### 사용 사례 #1 {#use-case-1}

대기업 기술 회사가 곧 열릴 글로벌 엑스포에 대한 공개 등록을 앞두고 있으며 등록 프로세스를 간소화하기 위해 고객 프로필을 [!DNL RainFocus]에 푸시하려고 합니다.

### 사용 사례 #2 {#use-case-2}

금융 서비스 브랜드는 신규 고객과 기존 고객을 대상으로 하는 일련의 로드쇼를 개최할 예정이다. Adobe Experience Platform에는 Target 고객이 있는 일련의 대상 세그먼트가 있습니다. [!DNL RainFocus] 대상 커넥터를 사용하면 활성화를 위해 해당 프로필을 [!DNL RainFocus](으)로 쉽게 보낼 수 있습니다.

## 전제 조건 {#prerequisites}

[!DNL RainFocus] 대상을 사용하려면 먼저 다음 전제 조건을 충족해야 합니다.

* OAuth(전역)를 사용하여 [!DNL RainFocus] API 프로필을 만듭니다.
   * **참석자 저장소** 끝점을 사용하도록 설정해야 합니다.
   * **클라이언트 ID** 및 **클라이언트 암호**&#x200B;를 생성해야 합니다.

또한 프로필을 보낼 RainFocus **이벤트 코드** 식별자가 있어야 합니다.

## 지원되는 ID {#supported-identities}

[!DNL RainFocus]은(는) 아래 표에 설명된 ID 활성화를 지원합니다. [ID](/help/identity-service/features/namespaces.md)에 대해 자세히 알아보세요.

| 대상 ID | 설명 | 고려 사항 |
|---|---|---|
| email_lc_sha256 | SHA256 알고리즘으로 해시된 이메일 주소 | Adobe Experience Platform은 일반 텍스트와 SHA256 해시 이메일 주소를 모두 지원합니다. 소스 필드에 해시되지 않은 특성이 포함된 경우 **[!UICONTROL 변환 적용]** 옵션을 선택하여 [!DNL Platform]이(가) 활성화 시 데이터를 자동으로 해시하도록 하십시오. |

{style="table-layout:auto"}

## 지원되는 대상자 {#supported-audiences}

이 섹션에서는 이 대상으로 내보낼 수 있는 대상자 유형을 설명합니다.

| 대상자 원본 | 지원됨 | 설명 |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ 덧신 | Experience Platform [세그먼테이션 서비스](../../../segmentation/home.md)를 통해 생성된 대상입니다. |
| 사용자 정의 업로드 | ✓ 덧신 | CSV 파일에서 Experience Platform으로 대상 [가져옴](../../../segmentation/ui/overview.md#import-audience). |

{style="table-layout:auto"}

## 내보내기 유형 및 빈도 {#export-type-frequency}

대상 내보내기 유형 및 빈도에 대한 자세한 내용은 아래 표를 참조하십시오.

| 항목 | 유형 | 참고 |
---------|----------|---------|
| 내보내기 유형 | **[!UICONTROL 프로필 기반]** | [대상 활성화 워크플로](/help/destinations/ui/activate-batch-profile-destinations.md#select-attributes)의 프로필 특성 선택 화면에서 선택한 대로 원하는 스키마 필드(예: 이메일 주소, 전화번호, 성)와 함께 세그먼트의 모든 구성원을 내보냅니다. |
| 내보내기 빈도 | **[!UICONTROL 스트리밍]** | 스트리밍 대상은 &quot;항상&quot; API 기반 연결입니다. Experience Platform 평가를 기반으로 프로필이 세그먼트에서 업데이트되는 즉시 커넥터가 업데이트 다운스트림을 대상 플랫폼으로 전송합니다. [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대해 자세히 알아보세요. |

{style="table-layout:auto"}

## 대상에 연결 {#connect}

>[!IMPORTANT]
> 
>대상에 연결하려면 **[!UICONTROL 대상 보기]** 및 **[!UICONTROL 대상 관리]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

이 대상에 연결하려면 [대상 구성 자습서](../../ui/connect-destination.md)에 설명된 단계를 따르십시오. 대상 구성 워크플로에서 아래 두 섹션에 나열된 필드를 채웁니다.

### 대상으로 인증 {#authenticate}

대상에 인증하려면 필수 필드를 입력한 다음 **[!UICONTROL 대상에 연결]**&#x200B;을(를) 선택하십시오.

![RainFocus 대상 커넥터에 대한 인증 세부 정보를 제공합니다](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-authentication.png)

* **[!UICONTROL 클라이언트 ID]**: RainFocus API 프로필에서 제공한 [!DNL Client ID]을(를) 입력하십시오.
* **[!UICONTROL 클라이언트 암호]**: RainFocus API 프로필에서 제공한 [!DNL Client Secret]을(를) 입력하십시오.
* **[!UICONTROL 환경]**: 연결할 RainFocus 환경(예: `dev`, `prod`)을 지정하십시오.
* **[!UICONTROL 조직 ID]**: RainFocus 인스턴스에 대한 고유한 `orgid`을(를) 제공합니다.

### 대상 세부 정보 입력 {#destination-details}

대상에 대한 세부 정보를 구성하려면 아래의 필수 및 선택 필드를 채우십시오. UI에서 필드 옆에 있는 별표는 필드가 필수임을 나타냅니다.

![RainFocus 대상 커넥터에 대한 연결 세부 정보를 제공합니다](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-configure-destination-details.png)

* **[!UICONTROL 이름]**: 나중에 이 대상을 인식할 수 있는 이름입니다.
* **[!UICONTROL 설명]**: 나중에 이 대상을 식별하는 데 도움이 되는 설명입니다.
* **[!UICONTROL 이벤트 ID]**: 프로필이 전송될 [!DNL RainFocus] 이벤트 코드 식별자입니다.

### 경고 활성화 {#enable-alerts}

경고를 활성화하여 대상에 대한 데이터 흐름 상태에 대한 알림을 받을 수 있습니다. 목록에서 경고를 선택하여 데이터 흐름 상태에 대한 알림을 수신합니다. 경고에 대한 자세한 내용은 [UI를 사용하여 대상 경고 구독](../../ui/alerts.md)에 대한 안내서를 참조하십시오.

대상 연결에 대한 세부 정보를 모두 제공했으면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

## 이 대상에 대한 세그먼트 활성화 {#activate}

>[!IMPORTANT]
> 
>* 데이터를 활성화하려면 **[!UICONTROL 대상 보기]**, **[!UICONTROL 대상 활성화]**, **[!UICONTROL 프로필 보기]** 및 **[!UICONTROL 세그먼트 보기]** [액세스 제어 권한](/help/access-control/home.md#permissions)이 필요합니다. [액세스 제어 개요](/help/access-control/ui/overview.md)를 읽거나 제품 관리자에게 문의하여 필요한 권한을 받으십시오.

대상 세그먼트를 이 대상으로 활성화하는 방법에 대한 지침은 [프로필 및 세그먼트를 스트리밍 세그먼트 내보내기 대상으로 활성화](/help/destinations/ui/activate-segment-streaming-destinations.md)를 참조하십시오.

### 속성 및 ID 매핑 {#map}

사용 사례에 따라 다음 대상 ID 네임스페이스를 매핑해야 합니다.

* **전자 메일**&#x200B;은(는) **대상 필드 > ID 네임스페이스 선택 > 전자 메일**&#x200B;을(를) 사용하여 대상 필드로 매핑되어야 합니다.

![프로필 및 ID 필드를 매핑하는 방법](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-mapping.png)

추가 프로필 필드를 매핑하면 [!DNL RainFocus]의 참석자 프로필이 완전히 채워지므로 매핑하는 것이 좋습니다. [!DNL RainFocus]에서 다음 대상 필드를 사용할 수 있습니다.

| 대상 필드 | 설명 |
|------------|-------------|
| `address1` | 상세 주소의 첫 번째 줄입니다 |
| `address2` | 상세 주소의 두 번째 줄(해당하는 경우) |
| `city` | 도시 이름 |
| `companyname` | 회사 이름 |
| `countryid` | 해당 국가의 ISO 3166-1 알파-2 국가 코드 식별자 |
| `email` | 이메일 주소 |
| `firstname` | 사용자의 이름 |
| `lastname` | 사용자의 성 |
| `jobtitle` | 개인의 직책 |
| `phone` | 전화번호 |
| `state` | 주 또는 시/도에 대한 FIPS 주 알파 코드 |
| `zip` | 우편 번호 또는 우편 번호 |

{style="table-layout:auto"}

## 내보낸 데이터/데이터 내보내기 유효성 검사 {#exported-data}

프로필 집합이 [!DNL RainFocus](으)로 전송되면 [!DNL RainFocus]의 API 프로필 로깅을 사용하여 프로필이 성공적으로 수집되었는지 확인하십시오.

![RainFocus에서 API 프로필의 로그 보기](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-api-profile.png)

![프로필이 수집되었는지 확인](/help/destinations/assets/catalog/marketing-automation/rainfocus/rainfocus-destination-api-logging.png)

## 데이터 사용 및 관리 {#data-usage-governance}

데이터를 처리할 때 모든 [!DNL Adobe Experience Platform] 대상이 데이터 사용 정책을 준수합니다. [!DNL Adobe Experience Platform]에서 데이터 거버넌스를 적용하는 방법에 대한 자세한 내용은 [데이터 거버넌스 개요](/help/data-governance/home.md)를 참조하십시오.

## 추가 리소스 {#additional-resources}

* [RainFocus 스트리밍 Source 커넥터](https://experienceleague.adobe.com/en/docs/experience-platform/sources/connectors/analytics/rainfocus)