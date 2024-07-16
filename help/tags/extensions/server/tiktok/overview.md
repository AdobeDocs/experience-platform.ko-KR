---
title: Adobe TikTok 웹 이벤트 API 확장 통합
description: 이 Adobe Experience Platform 웹 이벤트 API를 사용하면 TikTok과 웹 사이트 상호 작용을 직접 공유할 수 있습니다.
last-substantial-update: 2023-09-26T00:00:00Z
exl-id: 14b8e498-8ed5-4330-b1fa-43fd1687c201
source-git-commit: 4ee895cb8371646fd2013e2a8f65c2ffdae95850
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 2%

---

# [!DNL TikTok] 웹 이벤트 API 확장 개요

[!DNL TikTok] Edge Network API는 웹 사이트에서 사용자 작업에 대한 정보를 [!DNL TikTok]과(와) 직접 공유할 수 있는 보안 [이벤트 서버 API](/help/server-api/overview.md) 인터페이스입니다. 이벤트 전달 규칙을 사용하여 [!DNL TikTok] 웹 이벤트 API 확장을 사용하여 [!DNL Adobe Experience Platform Edge Network]에서 [!DNL TikTok](으)로 데이터를 보낼 수 있습니다.

## [!DNL TikTok]개 필수 구성 요소 {#prerequisites}

[!DNL TikTok] 이벤트 API를 사용하도록 [!DNL TikTok] 웹 이벤트 API를 구성하려면 [!DNL TikTok] 픽셀 코드와 액세스 토큰을 생성해야 합니다.

파트너 설정을 사용하여 [!DNL TikTok]픽셀을 만들려면 비즈니스 계정에 대해 올바른 [!DNL TikTok]이(가) 있어야 합니다. 아직 계정이 없는 경우 등록하고 계정을 만들려면 [[!DNL TikTok] 비즈니스 등록 페이지](https://www.tiktok.com/business/en-US/solutions/business-account)(으)로 이동하십시오.

파트너 설정을 사용하여 [!DNL TikTok]픽셀을 설정하려면 비즈니스 계정에 로그인해야 합니다. 이렇게 하려면 아래 단계를 수행합니다.

1. **[!UICONTROL Assets]** 탭으로 이동하여 **[!UICONTROL 이벤트]**&#x200B;를 선택합니다.
2. 웹 이벤트에서 **[!UICONTROL 관리]**&#x200B;를 선택합니다.
3. **[!UICONTROL 웹 이벤트 설정]**&#x200B;을 선택합니다.
4. 연결 방법으로 **[!UICONTROL 파트너 설정]**&#x200B;을(를) 선택하십시오.

[!DNL TikTok] 픽셀을 설정하는 방법에 대한 자세한 내용은 [픽셀 시작하기](https://ads.tiktok.com/help/article/get-started-pixel) 안내서를 참조하십시오.

픽셀이 성공적으로 생성되면 액세스 토큰을 생성할 수 있습니다. 이렇게 하려면 픽셀로 이동하여 **[!UICONTROL 설정]** 탭을 선택합니다. Events API에서 **[!UICONTROL 액세스 토큰 생성]**&#x200B;을 선택합니다.

픽셀 코드 및 액세스 토큰을 설정하는 방법에 대한 자세한 내용은 [[!DNL TikTok] 시작 안내서](https://business-api.tiktok.com/portal/docs?id=1739584855420929)를 참조하십시오.

## [!DNL TikTok] 웹 이벤트 API 확장 설치 및 구성 {#install}

확장을 설치하려면 왼쪽 탐색에서 **[!UICONTROL 확장]**&#x200B;을 선택합니다. **[!UICONTROL 카탈로그]** 탭에서 **[!UICONTROL TikTok 웹 이벤트 API 확장]**&#x200B;을 선택한 다음 **[!UICONTROL 설치]**&#x200B;를 선택합니다.

![설치를 강조 표시하는 [!DNL TikTok] 확장 카드를 표시하는 확장 카탈로그입니다.](../../../images/extensions/server/tiktok/install-extension.png)

다음 화면에서는 [!DNL TikTok] Ads Manager에서 이전에 생성한 다음 구성 값을 입력합니다.

* **[!UICONTROL 픽셀 코드]**
* **[!UICONTROL 액세스 토큰]**

완료되면 **[!UICONTROL 저장]**&#x200B;을 선택합니다.

[!DNL TikTok] 웹 이벤트 API 확장에 대한 ![[!DNL TikTok] 구성 화면입니다.](../../../images/extensions/server/tiktok/configure.png)

## 이벤트 전달 규칙 구성 {#config-rule}

모든 데이터 요소가 설정되면 이벤트가 [!DNL TikTok]에 전송되는 시기와 방법을 결정하는 이벤트 전달 규칙을 만들 수 있습니다.

이벤트 전달 속성에 새 [규칙](../../../ui/managing-resources/rules.md)을(를) 만듭니다. **[!UICONTROL 작업]**&#x200B;에서 새 작업을 추가하고 확장을 **[!UICONTROL TikTok 웹 이벤트 API 확장]**(으)로 설정합니다. Edge Network 이벤트를 [!DNL TikTok]에 보내려면 **[!UICONTROL 작업 유형]**&#x200B;을(를) **[!UICONTROL TikTok 웹 이벤트 API 이벤트 보내기].**(으)로 설정하십시오.

![데이터 수집 UI에서 [!DNL TikTok] 규칙에 대해 [!UICONTROL TikTok 웹 이벤트 API 이벤트 보내기] 작업 유형을 선택하고 있습니다.](../../../images/extensions/server/tiktok/select-action.png)

선택 후 아래 설명된 대로 이벤트를 추가로 구성하는 추가 제어 기능이 나타납니다. 완료되면 **[!UICONTROL 변경 내용 유지]**&#x200B;를 선택하여 규칙을 저장합니다.

**[!UICONTROL 웹 이벤트 및 매개 변수]**

웹 이벤트와 매개 변수에는 이벤트에 대한 일반 정보가 포함되어 있습니다. 표준 이벤트는 [!DNL TikTok] 통합 도구에서 지원되며 보고, 전환 최적화 및 대상 작성에 사용할 수 있습니다.

| 입력 | 설명 |
| --- | --- |
| 이벤트 이름 | 이벤트의 이름입니다. [!DNL TikTok]에서 만든 미리 정의된 이름을 사용하는 작업이며 필수 필드입니다. 지원되는 이벤트에 대한 자세한 내용은 [[!DNL TikTok] 마케팅 API](https://business-api.tiktok.com/portal/docs?id=1741601162187777) 설명서를 참조하세요. |
| 이벤트 시간 | ISO 8601 또는 `yyyy-MM-dd'T'HH:mm:ss:SSSZ` 형식의 문자열로 표시된 날짜-시간입니다. 필수 필드입니다. |
| 이벤트 ID | 광고주가 각 이벤트를 표시하기 위해 생성한 고유 ID. 이 필드는 선택 사항이며 중복 제거에 사용됩니다. |

{style="table-layout:auto"}

![필드에 입력된 데이터 예제를 보여 주는 [!DNL Web Events and Parameters] 섹션입니다.](../../../images/extensions/server/tiktok/configure-web-events-parameters.png)

**[!UICONTROL 사용자 컨텍스트 매개 변수]**

사용자 컨텍스트 매개 변수에는 웹 방문자 이벤트를 [!DNL TikTok] 사용자와 일치시키는 데 사용되는 고객 정보가 포함되어 있습니다. 여러 유형의 일치하는 데이터를 포함하면 타깃팅 및 최적화 모델의 정확도를 높일 수 있습니다.

| 입력 | 설명 |
| --- | --- |
| IP 주소 | 해시되지 않은 브라우저의 공개 IP 주소입니다. IPv4 및 IPv6 주소에 대한 지원이 제공됩니다. IPv6 주소의 전체 형식과 압축 형식은 모두 인식됩니다. |
| 사용자 에이전트 | 사용자 디바이스에서 해시되지 않은 사용자 에이전트. |
| 이메일 | 전환 이벤트와 연계된 연락처의 이메일 주소. |
| 휴대폰 | 해싱하기 전에 전화번호는 E164 형식 [+][국가 코드][지역 코드][local phone number]여야 합니다. |
| 쿠키 ID | Pixel SDK를 사용하는 경우 쿠키가 활성화되면 `_ttp` 쿠키에 고유 식별자가 자동으로 저장됩니다. 이 필드에 대해 `_ttp` 값을 추출하여 사용할 수 있습니다. |
| 외부 ID | 사용자 ID, 외부 쿠키 ID 등과 같은 모든 고유 식별자는 SHA256으로 해시해야 합니다. |
| TikTok 클릭 ID | [!DNL TikTok]에서 광고를 선택할 때마다 랜딩 페이지의 URL에 추가되는 `ttclid`입니다. |
| 페이지 URL | 이벤트 시 페이지 URL입니다. |
| 페이지 레퍼러 URL | 페이지 레퍼러의 URL입니다. |

{style="table-layout:auto"}

![필드에 입력된 데이터 예제를 보여 주는 [!DNL User Context Parameters] 섹션입니다.](../../../images/extensions/server/tiktok/configure-user-context-parameters.png)

**[!UICONTROL 속성 매개 변수]**

지원되는 추가 속성을 구성하려면 속성 매개 변수를 사용하십시오.

| 입력 | 설명 |
| --- | --- |
| 가격 | 단일 항목의 비용. |
| 수량 | 이벤트에서 구매 중인 항목 수입니다. 0보다 큰 양수여야 합니다. |
| 콘텐츠 유형 | 제품 카탈로그를 설정할 때 데이터 피드를 구성하는 방법에 따라 `product` 또는 `product_group` 값을 content_type 개체 속성에 할당해야 합니다. |
| 컨텐츠 ID | 제품 항목에 대한 고유 식별자. |
| 컨텐츠 범주 | 페이지/제품 범주. |
| 컨텐츠 이름 | 페이지/제품 이름. |
| 통화 | 이벤트에서 구매 중인 항목의 통화입니다. 이는 ISO-4217에 표시되어 있습니다. |
| 값 | 주문의 총 가격. 이 값은 가격 * 수량과 같습니다. |
| 설명 | 항목 또는 페이지에 대한 설명. |
| 쿼리 | 제품을 조회하는 데 사용된 텍스트 문자열입니다. |
| 상태 | 주문, 품목 또는 서비스의 상태. 예: &quot;제출됨&quot;. |

{style="table-layout:auto"}

![필드에 입력된 데이터 예제를 보여 주는 [!DNL Properties Parameters] 섹션입니다.](../../../images/extensions/server/tiktok/configure-properties-parameters.png)

## 이벤트 중복 제거 {#deduplication}

[!DNL TikTok]픽셀 SDK와 [!DNL TikTok] 웹 이벤트 API 확장을 모두 사용하여 동일한 이벤트를 [!DNL TikTok]에 보내는 경우 중복 제거에 대해 [!DNL TikTok]픽셀을 설정해야 합니다.

클라이언트 및 서버에서 중복되지 않고 개별 이벤트 유형을 보내는 경우에는 중복 제거가 필요하지 않습니다. 보고에 부정적인 영향을 주지 않도록 하려면 [!DNL TikTok] 픽셀 SDK 및 [!DNL TikTok] 웹 이벤트 API 확장에서 공유하는 단일 이벤트가 중복 제거되었는지 확인해야 합니다.

공유 이벤트를 보낼 때 모든 이벤트에 픽셀 ID, 이벤트 ID 및 이름이 포함되어 있는지 확인하십시오. 서로 5분 이내에 도착하는 중복 이벤트는 병합됩니다. 데이터 필드가 첫 번째 이벤트에 없으면 후속 이벤트와 결합됩니다. 48시간 이내에 수신되는 중복 이벤트는 모두 제거됩니다.

이 프로세스에 대한 자세한 내용은 [이벤트 중복 제거](https://ads.tiktok.com/help/article/event-deduplication)의 [!DNL TikTok] 설명서를 참조하십시오.

## 다음 단계

이 안내서에서는 [!DNL TikTok] 웹 이벤트 API 확장을 사용하여 서버측 이벤트 데이터를 [!DNL TikTok]에 보내는 방법을 다룹니다. [!DNL Adobe Experience Platform]의 이벤트 전달 기능에 대한 자세한 내용은 [이벤트 전달 개요](../../../ui/event-forwarding/overview.md)를 참조하세요.
