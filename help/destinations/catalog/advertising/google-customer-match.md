---
keywords: google customer match;Google customer match;Google Customer Match
title: Google 고객 일치 대상
seo-title: Google 고객 일치 대상
description: Google Customer Match를 사용하면 온라인 및 오프라인 데이터를 사용하여 검색, 쇼핑, Gmail, YouTube 등 Google의 소유물과 운영 자산에서 고객에게 도달하고 다시 참여할 수 있습니다.
seo-description: Google Customer Match를 사용하면 온라인 및 오프라인 데이터를 사용하여 검색, 쇼핑, Gmail, YouTube 등 Google의 소유물과 운영 자산에서 고객에게 도달하고 다시 참여할 수 있습니다.
translation-type: tm+mt
source-git-commit: 24c8dd0f01d7ea14b2fa5827722e797bd209f50c
workflow-type: tm+mt
source-wordcount: '1544'
ht-degree: 0%

---


# Google 고객 일치 대상

## 개요 {#overview}

[Google 고객](https://support.google.com/google-ads/answer/6379332?hl=en) 일치 기능을 사용하면 온라인 및 오프라인 데이터를 사용하여 다음과 같은 Google 소유 및 운영 자산에서 고객에게 도달하고 재참여할 수 있습니다. [!DNL Search], [!DNL Shopping], [!DNL Gmail]및 [!DNL YouTube]를 참조하십시오.

![실시간 CDP UI에서 Google 고객 일치 대상](../../assets/catalog/advertising/google-customer-match/catalog.png)

## 사용 사례

대상을 사용하는 방법과 시기를 보다 잘 이해할 수 있도록 실시간 고객 데이터 플랫폼 고객이 이 기능을 사용하여 해결할 수 있는 샘플 사용 사례를 소개합니다. [!DNL Google Customer Match]

### 사용 사례 #1

스포츠 의류 브랜드 기업은 과거 구매 [!DNL Google Search] 와 검색 내역을 기반으로 제안 및 항목을 개인화하여 기존 고객에게 도달하고 [!DNL Google Shopping] 싶어합니다. 의류 브랜드 기업은 자사의 CRM에서 실시간 CDP로 이메일 주소를 인제스트하고, 자체 오프라인 데이터에서 세그먼트를 작성하고, 이러한 세그먼트를 전송하여 모든 고객 [!DNL Google Customer Match] 에서 사용할 수 있도록 함으로써 광고 지출을 최적화할 수 [!DNL Search] [!DNL Shopping]있습니다.

### 사용 사례 #2

한 유명 기술 회사가 최근 새 휴대폰을 출시했다. 이 새로운 전화 모델을 홍보하기 위한 노력의 일환으로, 그들은 전화를 이전 모델을 소유하고 있는 고객에게 휴대폰의 새로운 기능과 기능에 대한 인식을 높이고자 노력하고 있다.

이 릴리스를 홍보하기 위해 이메일 주소를 식별자로 사용하여 CRM 데이터베이스의 이메일 주소를 실시간 CDP로 업로드합니다. 세그먼트는 이전 전화 모델을 소유하고 있는 고객을 기반으로 생성되어 이전 모델 및 유사한 고객을 타깃팅할 수 [!DNL Google Customer Match] 있도록 [!DNL YouTube]전송됩니다.

## 대상을 위한 데이터 [!DNL Google Customer Match] 거버넌스 {#data-governance}

실시간 CDP의 대상은 대상 플랫폼으로 전송되거나 수신되는 데이터에 대한 특정 규칙 및 의무를 가질 수 있습니다. 데이터의 제한 및 의무와 Adobe Experience Platform 및 대상 플랫폼에서 해당 데이터를 사용하는 방법을 이해해야 합니다. Adobe Experience Platform은 이러한 데이터 사용 의무 중 일부를 관리하는 데 도움이 되는 데이터 관리 툴을 제공합니다. [데이터 거버넌스 툴 및 정책에 대한 자세한](../../..//data-governance/labels/overview.md) 내용을 살펴보십시오.

## 내보내기 유형 및 ID {#export-type}

**세그먼트 내보내기** - 식별자(이름, 전화 번호 등)를 사용하여 세그먼트(대상)의 모든 멤버를 내보냅니다. 대상에 [!DNL Google Customer Match] 사용됩니다.

**ID** - Google에서 원시 또는 해시된 이메일을 고객 ID로 사용할 수 있습니다.

## [!DNL Google Customer Match] 계정 전제 조건 {#google-account-prerequisites}

실시간 CDP에서 [!DNL Google Customer Match] 대상을 설정하기 전에 Google 지원 설명서에 나와 있는 Google의 사용 정책 [!DNL Customer Match]을 읽고 준수해야 합니다 [](https://support.google.com/google-ads/answer/6299717).

### 허용 목록 {#allowlist}

>[!NOTE]
>
>실시간 CDP에서 첫 번째 대상을 설정하기 전에 Google의 허용 목록에 추가해야 [!DNL Google Customer Match] 합니다. 대상을 만들기 전에 아래에 설명된 허용 목록 프로세스가 Google에서 완료되었는지 확인하십시오.

실시간 CDP에서 [!DNL Google Customer Match] 대상을 만들려면 Google에 문의하고 고객 일치 파트너 [사용](https://support.google.com/google-ads/answer/7361372?hl=en&amp;ref_topic=6296507) 의 허용 목록 지침을 따라 Google 문서에서 데이터를 업로드해야 합니다.


### 이메일 해싱 요구 사항 {#hashing-requirements}

<!--

>[!IMPORTANT]
>
> When using mobile device IDs as identifiers, an AppId must be provided in the activation flow. For more information, see step 6 in the [Activate segments](#activate-segments) section of this page.

-->

Google에서는 PII(개인 식별 정보)가 명확하게 전송되지 않도록 요구합니다. 따라서, 활성화한 대상이 해시된 이메일 주소 [!DNL Google Customer Match] 에서 *키잉되어야* 합니다. 이메일 주소를 Adobe Experience Platform으로 인제스트하기 전에 해시하도록 선택하거나, Experience Platform에서 명확하게 이메일 주소를 사용하여 작업하도록 선택하고 알고리즘이 활성화하면 해당 이메일 주소를 해시하도록 할 수 있습니다.

Google의 해싱 요구 사항 및 기타 활성화 제한 사항에 대한 자세한 내용은 Google 설명서의 다음 섹션을 참조하십시오.

* [[!DNL Customer Match] 이메일 주소, 주소 또는 사용자 ID 사용](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_email_address_address_or_user_id)
* [[!DNL Customer Match] 고려 사항](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_considerations)

<!--

Links to be added when activation based on phone number and device IDs becomes available.

* [Customer Match with phone number](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_phone_number)
* [Customer Match with mobile device IDs](https://developers.google.com/adwords/api/docs/guides/remarketing#customer_match_with_mobile_device_ids)

-->

Experience Platform에서 이메일 주소 인제스트에 대한 자세한 내용은 [일괄 처리 개요](../../../ingestion/batch-ingestion/overview.md) 및 [스트리밍 통합 개요를 참조하십시오](../../../ingestion/streaming-ingestion/overview.md).

직접 이메일 주소를 해시하도록 선택한 경우 위의 링크에서 설명한 Google의 요구 사항을 준수해야 합니다.


>[!IMPORTANT]
>
>이메일 주소를 해시하지 않기로 선택하면 세그먼트를 활성화할 때 실시간 CDP가 자동으로 수행됩니다 [!DNL Google Customer Match]. [활성화 워크플로우](#activate-segments) (5단계 참조)에서 `Email` 일반 텍스트 이메일 주소 *및 해시된 이메일 주소* 에 대해 아래 `Email_LC_SHA256` 와 같은 옵션을 **&#x200B;선택합니다.

![활성화 시 해싱](../../assets/catalog/advertising/google-customer-match/identity-mapping.png)

## 대상에 연결 {#connect-destination}

대상 **** > **[!UICONTROL 카탈로그]**&#x200B;에서 **[!UICONTROL 광고]** 카테고리로스크롤합니다. 을 [!DNL Google Customer Match]선택하고 구성을 **[!UICONTROL 선택합니다]**.

![Google 고객 일치 대상에 연결](../../assets/catalog/advertising/google-customer-match/connect.png)

>[!NOTE]
>
>이 대상과의 연결이 이미 있는 경우 대상 카드에 **[!UICONTROL 활성화]** 단추가 표시됩니다. 활성화 및 구성 **[!UICONTROL 의 차이에 대한 자세한]****[!UICONTROL 내용은 대상 작업 공간 설명서의]**&#x200B;카탈로그 [섹션을](../../ui/destinations-workspace.md#catalog) 참조하십시오.

이전에 대상에 대한 연결을 **설정한** 경우 [!DNL Google Customer Match] 계정 **[!UICONTROL 을 선택하고 기존 연결을]** 선택합니다. 또는 새 계정 **[!UICONTROL 을]** 선택하여 새 연결을 설정할 수 [!DNL Google Customer Match]있습니다. [ **[!UICONTROL 대상에]** 연결]을 선택하여 로그인하고 Adobe Experience Cloud을 계정에 [!DNL Google Ad] 연결합니다.

>[!NOTE]
>
>실시간 CDP는 인증 프로세스의 자격 증명 유효성 검사를 지원하고 계정에 잘못된 자격 증명을 입력한 경우 오류 메시지를 [!DNL Google Ad] 표시합니다. 따라서 잘못된 자격 증명으로 워크플로우를 완료하지 못합니다.

![Google 고객 일치 대상 - 인증 단계에 연결](../../assets/catalog/advertising/google-customer-match/connection.png)

자격 증명이 확인되고 Adobe Experience Cloud이 Google 계정에 연결되면 **[!UICONTROL 다음]** 을 선택하여 **[!UICONTROL 설정]** 단계로 진행할 수 있습니다.

![자격 증명 확인됨](../../assets/catalog/advertising/google-customer-match/connection-success.png)

인증 **[!UICONTROL 단계에서]** 이름 [!UICONTROL 과] 정품 인증 [!UICONTROL 과정에 대한 설명] 을 입력하고 Google에 Account ID를 입력합니다.

또한 이 단계에서는 이 대상에 **[!UICONTROL 적용되어야 하는 모든]** 마케팅 사용 사례를 선택할 수 있습니다. 마케팅 사용 사례에서는 데이터를 대상으로 내보내려는 의도를 나타냅니다. Adobe에서 정의한 마케팅 사용 사례에서 선택하거나 고유한 마케팅 사용 사례를 만들 수 있습니다. 마케팅 활용 사례에 대한 자세한 내용은 실시간 CDP의 [데이터 거버넌스](../../../rtcdp/privacy/data-governance-overview.md#destinations) 페이지를 참조하십시오. 개별 Adobe에서 정의한 마케팅 사용 사례에 대한 자세한 내용은 [데이터 사용 정책 개요를 참조하십시오](../../../data-governance/policies/overview.md#core-actions).

위 필드 **[!UICONTROL 를]** 채운 후 대상 만들기를 선택합니다.

>[!IMPORTANT]
>
> * PII **[!UICONTROL 마케팅]** 사용 사례와 결합은 기본적으로 대상에 대해 선택되며 [!DNL Google Customer Match] 제거할 수 없습니다.
> * 대상 [!DNL Google Customer Match] 을 참조하십시오. **[!UICONTROL 계정 ID는]** Google의 고객 클라이언트 ID입니다. ID의 형식은 xxx-xxx-xxxx입니다.


![Connect Google 고객 일치 - 인증 단계](../../assets/catalog/advertising/google-customer-match/authentication.png)

이제 대상이 만들어집니다. 나중에 세그먼트 **[!UICONTROL 를]** 활성화하려면 저장 및 종료를 **[!UICONTROL 선택하거나]** 다음을 선택하여 워크플로우를 계속하고 활성화할 세그먼트를 선택할 수 있습니다. 다음 섹션, 세그먼트 [활성화 [!DNL Google Customer Match]](#activate-segments), 나머지 작업 흐름 중 하나를 참조하십시오.

## 세그먼트 활성화 [!DNL Google Customer Match] {#activate-segments}

세그먼트를 활성화하려면 [!DNL Google Customer Match]아래 단계를 따르십시오.

대상 **[!UICONTROL > 찾아보기에서]**&#x200B;세그먼트를 활성화할 [!DNL Google Customer Match] 대상을 선택합니다.

대상의 이름을 클릭합니다. 활성화 흐름으로 이동합니다.

![정품 인증](../../assets/catalog/advertising/google-customer-match/activate-flow.png)

대상에 대한 활성화 흐름이 이미 존재하는 경우 대상에 현재 전송되고 있는 세그먼트를 볼 수 있습니다. 오른쪽 레일에서 **[!UICONTROL 활성화]** 편집을 선택하고 아래 단계에 따라 정품 인증 세부 사항을 수정합니다.

활성화를 **[!UICONTROL 선택합니다]**. 대상 **[!UICONTROL 활성화]** 워크플로의 세그먼트 **[!UICONTROL 선택]** 페이지에서 보낼 세그먼트를 [!DNL Google Customer Match]선택합니다.

![세그먼트-대상](../../assets/catalog/advertising/google-customer-match/activate-segments.png)

ID **[!UICONTROL 매핑]** 단계에서 이 대상에 ID로 포함할 속성을 선택합니다. 새 매핑 **[!UICONTROL 추가를]** 선택하고 스키마를 검색하고 이메일 및/또는 해시된 이메일을 선택한 다음 해당 대상 ID에 매핑합니다.

![ID 매핑 초기 화면](../../assets/catalog/advertising/google-customer-match/identity-mapping.png)

**일반 텍스트 이메일 주소(기본 ID**):스키마의 기본 ID로 일반 텍스트(해시되지 않은) 이메일 주소가 있는 경우 **[!UICONTROL 소스 속성]** 의 이메일 필드를 선택하고 아래 **[!UICONTROL 와 같이 Target ID]**&#x200B;아래의 오른쪽 열에 있는 이메일 필드에 매핑합니다.

![일반 텍스트 이메일 ID 선택](../../assets/catalog/advertising/google-customer-match/raw-email.gif)

**전자 메일 주소를 기본 ID로 해시했습니다**.스키마의 기본 ID로 이메일 주소를 해시한 경우 **[!UICONTROL 소스 속성]** 에서 해시된 이메일 필드를 선택하고 아래와 같이 Target ID ****&#x200B;아래의 오른쪽 열에 있는 Email_LC_SHA256 필드에 매핑합니다.

![해시 이메일 ID 선택](../../assets/catalog/advertising/google-customer-match/hashed-emails.gif)

세그먼트 **[!UICONTROL 예약]** 페이지에서 대상으로 데이터를 전송하는 시작 날짜를 설정할 수 있습니다.

[ **[!UICONTROL 검토]** ] 페이지에서 선택 사항의 요약을 볼 수 있습니다. 흐름을 구분하려면 **[!UICONTROL 취소]** 를, 설정을 **[!UICONTROL 수정하려면]** [뒤로]를, **[!UICONTROL 마침을]** 선택하여 선택을 확인하고 데이터를 대상에 보내기 시작합니다.

>[!IMPORTANT]
>
>이 단계에서 실시간 CDP는 데이터 사용 정책 위반을 확인합니다. 아래는 정책을 위반한 예입니다. 위반이 해결되기 전에는 세그먼트 활성화 워크플로우를 완료할 수 없습니다. 정책 위반을 해결하는 방법에 대한 자세한 내용은 데이터 거버넌스 문서 섹션에서 [정책](../../../rtcdp/privacy/data-governance-overview.md#enforcement) 적용을 참조하십시오.

![선택 확인](../../assets/common/data-policy-violation.png)

정책 위반이 감지되지 않은 경우 **[!UICONTROL 마침을]** 선택하여 선택을 확인하고 대상으로 데이터 전송을 시작합니다.

![선택 확인](../../assets/catalog/advertising/google-customer-match/review.png)


<!--

Insert in Step 6 when mobile device ID activation is available

    >[!IMPORTANT]
    >
    >If you select mobile device IDs (GAID or IDFA) as primary identity in the Identity mapping step, you must also provide an Application Id in this step. If you selected GAID as identity, see [Set the Application ID](https://developer.android.com/studio/build/application-id) in the Android developer documentation. IF you selected IDFA as identity, see [App ID](https://developer.android.com/studio/build/application-id) in the Apple developer documentation.

    ![segment schedule page](/help/rtcdp/destinations/assets/gcm-segment-schedule.png) 

-->

## 세그먼트 활성화 성공 여부 확인 {#verify-activation}

정품 인증 과정이 완료되면 **[!UICONTROL Google Ads]** 계정으로 전환합니다. 이제 활성화된 세그먼트가 고객 목록으로 Google 계정에 표시됩니다. 세그먼트 크기에 따라, 제공할 활성 사용자가 100명 이상인 경우 일부 대상이 채워지지 않습니다.

## 추가 리소스 {#additional-resources}

* [Google 고객 일치 통합 - 비디오 자습서](https://experienceleague.adobe.com/docs/platform-learn/tutorials/rtcdp/integrate-with-google-customer-match.html)