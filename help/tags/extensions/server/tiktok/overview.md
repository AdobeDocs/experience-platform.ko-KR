---
title: Adobe TikTok 웹 이벤트 API 확장 통합
description: 이 Adobe Experience Platform 웹 이벤트 API를 사용하면 TikTok과 웹 사이트 상호 작용을 직접 공유할 수 있습니다.
last-substantial-update: 2023-09-26T00:00:00Z
source-git-commit: d8b7006ade1dc82fdd79b7ed744c021bc304bca7
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 3%

---

# [!DNL TikTok] 웹 이벤트 API 확장 개요

다음 [!DNL TikTok] events API는 안전합니다. [Edge Network Server API](/help/server-api/overview.md) 정보를 공유할 수 있는 인터페이스 [!DNL TikTok] 웹 사이트에서의 사용자 작업에 대해 직접 설명합니다. 이벤트 전달 규칙을 활용하여 [!DNL Adobe Experience Platform Edge Network] 끝 [!DNL TikTok] 를 사용하여 [!DNL TikTok] 웹 이벤트 API 확장.

## [!DNL TikTok] 전제 조건 {#prerequisites}

을(를) 구성하려면 다음을 수행하십시오. [!DNL TikTok] 를 사용할 웹 이벤트 API [!DNL TikTok] events API, 다음을 생성해야 합니다. [!DNL TikTok] 픽셀 코드 및 액세스 토큰입니다.

유효한 권한이 있어야 합니다. [!DNL TikTok] 비즈니스 계정용 [!DNL TikTok] partner setup을 사용하여 픽셀을 지정합니다. 로 이동 [[!DNL TikTok] 비즈니스 등록 페이지용](https://www.tiktok.com/business/en-US/solutions/business-account) 아직 계정이 없는 경우 등록하고 계정을 만듭니다.

설정하려면 비즈니스 계정에 로그인해야 합니다. [!DNL TikTok] 파트너 설정을 사용하여 픽셀. 이렇게 하려면 아래 단계를 수행합니다.

1. 다음 위치로 이동 **[!UICONTROL 에셋]** 탭하고 선택 **[!UICONTROL 이벤트]**.
2. Web Events에서 **[!UICONTROL 관리]**.
3. 선택 **[!UICONTROL 웹 이벤트 설정]**.
4. 선택 **[!UICONTROL 파트너 설정]** 를 연결 방법으로 사용하십시오.

다음을 참조하십시오. [픽셀 시작](https://ads.tiktok.com/help/article/get-started-pixel) 를 설정하는 방법에 대한 자세한 내용은 안내서 를 참조하십시오. [!DNL TikTok] 픽셀.

픽셀이 성공적으로 생성되면 액세스 토큰을 생성할 수 있습니다. 이렇게 하려면 픽셀로 이동하여 **[!UICONTROL 설정]** 탭. Events API에서 **[!UICONTROL 액세스 토큰 생성]**.

다음을 참조하십시오. [[!DNL TikTok] 시작 안내서](https://business-api.tiktok.com/portal/docs?id=1739584855420929) 픽셀 코드 및 액세스 토큰을 설정하는 방법에 대한 자세한 내용을 보려면 여기를 클릭하십시오.

## 설치 및 구성 [!DNL TikTok] 웹 이벤트 API 확장 {#install}

확장을 설치하려면 다음을 선택합니다 **[!UICONTROL 확장]** 왼쪽 탐색. 다음에서 **[!UICONTROL 카탈로그]** 탭에서 **[!UICONTROL TikTok 웹 이벤트 API 확장]** 다음을 선택합니다. **[!UICONTROL 설치]**.

![다음을 표시하는 확장 카탈로그 [!DNL TikTok] 확장 카드 강조 표시 설치.](../../../images/extensions/server/tiktok/install-extension.png)

다음 화면에서는 이전에 생성한 다음 구성 값을 입력합니다 [!DNL TikTok] 광고 관리자:

* **[!UICONTROL 픽셀 코드]**
* **[!UICONTROL 액세스 토큰]**

완료되면 다음을 선택합니다. **[!UICONTROL 저장]**.

![[!DNL TikTok] 구성 화면 [!DNL TikTok] 웹 이벤트 API 확장.](../../../images/extensions/server/tiktok/configure.png)

## 이벤트 전달 규칙 구성 {#config-rule}

모든 데이터 요소가 설정되면 이벤트가 전송되는 시기와 방법을 결정하는 이벤트 전달 규칙 만들기를 시작할 수 있습니다 [!DNL TikTok].

새로 만들기 [규칙](../../../ui/managing-resources/rules.md) 이벤트 전달 속성에서 다음을 수행합니다. 아래 **[!UICONTROL 작업]**, 새 작업을 추가하고 확장을 로 설정합니다. **[!UICONTROL TikTok 웹 이벤트 API 확장]**. Edge Network 이벤트를 로 보내려면 [!DNL TikTok], 를 설정합니다. **[!UICONTROL 작업 유형]** 끝 **[!UICONTROL TikTok 웹 이벤트 API 이벤트 보내기].**

![다음 [!UICONTROL TikTok 웹 이벤트 API 이벤트 보내기] 에 대해 액션 유형 선택 중 [!DNL TikTok] 데이터 수집 UI의 규칙](../../../images/extensions/server/tiktok/select-action.png)

선택 후 아래 설명된 대로 이벤트를 추가로 구성하는 추가 제어 기능이 나타납니다. 완료되면 다음을 선택합니다. **[!UICONTROL 변경 내용 유지]** 을 눌러 규칙을 저장합니다.

**[!UICONTROL 웹 이벤트 및 매개 변수]**

웹 이벤트와 매개 변수에는 이벤트에 대한 일반 정보가 포함되어 있습니다. 표준 이벤트는 [!DNL TikTok] 통합 도구 및는 보고 , 전환 최적화 및 대상 작성에 사용할 수 있습니다.

| 입력 | 설명 |
| --- | --- |
| 이벤트 이름 | 이벤트의 이름입니다. 다음은에서 생성한 사전 정의된 이름의 작업입니다. [!DNL TikTok] 필수 필드입니다. 다음을 참조하십시오. [[!DNL TikTok] 마케팅 API](https://business-api.tiktok.com/portal/docs?id=1741601162187777) 지원되는 이벤트에 대한 자세한 내용은 설명서를 참조하십시오. |
| 이벤트 시간 | ISO 8601 또는 yyyy-MM-dd&#39;T&#39;HH의 문자열로 표시된 날짜-시간:mm:ss:SSSZ 형식입니다. 필수 필드입니다. |
| 이벤트 ID | 광고주가 각 이벤트를 표시하기 위해 생성한 고유 ID. 이 필드는 선택 사항이며 중복 제거에 사용됩니다. |

{style="table-layout:auto"}

![다음 [!DNL Web Events and Parameters] 필드로의 데이터 입력 예를 보여 주는 섹션입니다.](../../../images/extensions/server/tiktok/configure-web-events-parameters.png)

**[!UICONTROL 사용자 컨텍스트 매개 변수]**

사용자 컨텍스트 매개 변수에는 웹 방문자 이벤트를 와 일치시키는 데 사용되는 고객 정보가 포함됩니다 [!DNL TikTok] 사용자. 여러 유형의 일치하는 데이터를 포함하면 타깃팅 및 최적화 모델의 정확도를 높일 수 있습니다.

| 입력 | 설명 |
| --- | --- |
| IP 주소 | 해시되지 않은 브라우저의 공개 IP 주소입니다. IPv4 및 IPv6 주소에 대한 지원이 제공됩니다. IPv6 주소의 전체 형식과 압축 형식은 모두 인식됩니다. |
| 사용자 에이전트 | 사용자 디바이스에서 해시되지 않은 사용자 에이전트. |
| 이메일 | 전환 이벤트와 연계된 연락처의 이메일 주소. |
| 전화 | 전화번호는 E164 형식 [+][국가 코드]여야 합니다.[지역 번호][local phone number] 해싱하기 전에 |
| 쿠키 ID | Pixel SDK를 사용하는 경우에서 고유 식별자를 자동으로 저장합니다. `_ttp` 쿠키(쿠키가 활성화된 경우). 다음 `_ttp` 값을 추출하여 이 필드에 사용할 수 있습니다. |
| 외부 ID | 사용자 ID, 외부 쿠키 ID 등과 같은 모든 고유 식별자는 SHA256으로 해시해야 합니다. |
| TikTok 클릭 ID | 다음 `ttclid` 광고가 선택될 때마다 랜딩 페이지의 URL에 추가됩니다 [!DNL TikTok]. |
| 페이지 URL | 이벤트 시 페이지 URL입니다. |
| 페이지 레퍼러 URL | 페이지 레퍼러의 URL입니다. |

{style="table-layout:auto"}

![다음 [!DNL User Context Parameters] 필드로의 데이터 입력 예를 보여 주는 섹션입니다.](../../../images/extensions/server/tiktok/configure-user-context-parameters.png)

**[!UICONTROL 속성 매개 변수]**

지원되는 추가 속성을 구성하려면 속성 매개 변수를 사용하십시오.

| 입력 | 설명 |
| --- | --- |
| 가격 | 단일 항목의 비용. |
| 수량 | 이벤트에서 구매 중인 항목 수입니다. 0보다 큰 양수여야 합니다. |
| 콘텐츠 유형 | 다음 중 하나의 값 `product` 또는 `product_group` 제품 카탈로그를 설정할 때 데이터 피드를 구성하는 방법에 따라 content_type 개체 속성에 을 할당해야 합니다. |
| 콘텐츠 ID | 제품 항목에 대한 고유 식별자. |
| 콘텐츠 범주 | 페이지/제품 범주. |
| 컨텐츠 이름 | 페이지/제품 이름. |
| 통화 | 이벤트에서 구매 중인 항목의 통화입니다. 이는 ISO-4217에 표시되어 있습니다. |
| 값 | 주문의 총 가격. 이 값은 가격 * 수량과 같습니다. |
| 설명 | 항목 또는 페이지에 대한 설명. |
| 쿼리 | 제품을 조회하는 데 사용된 텍스트 문자열입니다. |
| 상태 | 주문, 품목 또는 서비스의 상태. 예: &quot;제출됨&quot;. |

{style="table-layout:auto"}

![다음 [!DNL Properties Parameters] 필드로의 데이터 입력 예를 보여 주는 섹션입니다.](../../../images/extensions/server/tiktok/configure-properties-parameters.png)

## 이벤트 중복 제거 {#deduplication}

[!DNL TikTok] 다음 두 가지를 모두 사용하는 경우 중복 제거를 위해 픽셀을 설정해야 합니다. [!DNL TikTok] pixel SDK 및 [!DNL TikTok] 동일한 이벤트를 전송할 웹 이벤트 API 확장 [!DNL TikTok].

클라이언트 및 서버에서 중복되지 않고 개별 이벤트 유형을 보내는 경우에는 중복 제거가 필요하지 않습니다. 보고에 부정적인 영향을 주지 않도록에서 공유하는 모든 단일 이벤트가 [!DNL TikTok] pixel SDK 및 [!DNL TikTok] 웹 이벤트 API 확장이 중복 제거됩니다.

공유 이벤트를 보낼 때 모든 이벤트에 픽셀 ID, 이벤트 ID 및 이름이 포함되어 있는지 확인하십시오. 서로 5분 이내에 도착하는 중복 이벤트는 병합됩니다. 데이터 필드가 첫 번째 이벤트에 없으면 후속 이벤트와 결합됩니다. 48시간 이내에 수신되는 중복 이벤트는 모두 제거됩니다.

다음을 참조하십시오. [!DNL TikTok] 설명서 [이벤트 중복 제거](https://ads.tiktok.com/help/article/event-deduplication) 이 프로세스에 대한 자세한 내용은 을 참조하십시오.

## 다음 단계

이 안내서에서는 서버측 이벤트 데이터를에 보내는 방법을 다룹니다. [!DNL TikTok] 사용 [!DNL TikTok] 웹 이벤트 API 확장. 의 이벤트 전달 기능에 대한 자세한 내용 [!DNL Adobe Experience Platform]을(를) 참조하십시오. [이벤트 전달 개요](../../../ui/event-forwarding/overview.md).
