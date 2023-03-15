---
title: Adobe Experience Platform 릴리스 노트 2023년 1월
description: Adobe Experience Platform의 2023년 1월 릴리스 정보.
source-git-commit: 6388c72aa0be8f5f91efaaa6a0edd22f3eb99de8
workflow-type: tm+mt
source-wordcount: '2414'
ht-degree: 6%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2023년 1월 25일**

Adobe Experience Platform의 기존 기능 업데이트:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai/ml-services)
- [보증](#assurance)
- [데이터 수집](#data-collection)
- [[!DNL Destinations]](#destinations)
- [경험 데이터 모델(XDM)](#xdm)
- [실시간 고객 프로필](#profile)
- [세분화 서비스](#segmentation)
- [소스](#sources)

## 인공 지능/머신 러닝 서비스 {#ai-ml}

인공 지능 및 머신 러닝 서비스는 마케팅 분석가 및 전문가가 고객 경험 사용 사례에서 AI/ML의 기능을 활용할 수 있도록 합니다. 이를 통해 마케팅 분석가는 비즈니스 수준 구성을 사용하여 데이터 과학 전문 지식 없이도 기업의 요구 사항에 맞는 예측을 설정할 수 있습니다.

### 기여도 AI

Attribution AI은 전환 이벤트로 이어지는 터치포인트에 크레딧을 제공하는 데 사용됩니다. 이를 통해 마케터는 고객 여정 전반에서 각 개별 마케팅 터치포인트의 마케팅 효과를 수량화할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| HIPAA 준비 | Healthcare Shield 고객은 이제 Attribution AI 및 기타 특정 Experience Platform 기반 애플리케이션에서 보호 상태 정보를 수신, 사용, 유지 관리 또는 전송할 수 있습니다. Healthcare Shield는 HIPAA에 따라 적용되는 엔티티 또는 비즈니스 제휴자인 의료 고객을 위한 것입니다. 자세한 내용은 [HIPAA 및 Adobe 제품 및 서비스](https://www.adobe.com/trust/compliance/hipaa-ready.html) |
| 추가 점수 데이터 세트 열 편집 | 이제 기존 모델을 편집할 때 추가 점수 데이터 세트 열(보고 열)을 추가하거나 제거할 수 있습니다. 이렇게 하면 속성 점수의 유연성이 확장되어 모델이 이미 생성된 후 추가 차원에 대한 통찰력을 얻을 수 있습니다. 다음을 참조하십시오. [속성 UI 안내서](../../intelligent-services/attribution-ai/user-guide.md) 자세히 알아보십시오. |

{style="table-layout:auto"}

다음을 참조하십시오. [AI/ML 서비스](../../intelligent-services/attribution-ai/overview.md) 개요 를 참조하십시오.

### 고객 AI

Real-time Customer Data Platform용 고객 AI는 규모에 따라 개별 프로필에 대한 이탈 및 전환과 같은 사용자 지정 성향 점수를 생성하는 데 사용됩니다. 비즈니스 요구 사항을 머신 러닝 문제로 변환하거나 알고리즘을 선택하거나 교육 또는 배포하지 않아도 됩니다.

**업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| HIPAA 준비 | Healthcare Shield 고객은 이제 Real-time Customer Data Platform 및 기타 특정 Experience Platform 기반 애플리케이션용 Customer AI에서 보호 상태 정보를 수신, 사용, 유지 관리 또는 전송할 수 있습니다. Healthcare Shield는 HIPAA에 따라 적용되는 엔티티 또는 비즈니스 제휴자인 의료 고객을 위한 것입니다. 자세한 내용은 [HIPAA 및 Adobe 제품 및 서비스](https://www.adobe.com/trust/compliance/hipaa-ready.html) |

{style="table-layout:auto"}

다음을 참조하십시오. [AI/ML 서비스](../../intelligent-services/customer-ai/overview.md) 개요 를 참조하십시오.

## 보증 {#assurance}

Adobe 보증을 통해 모바일 앱에서 데이터를 수집하거나 경험을 제공하는 방법을 검사, 증명, 시뮬레이션 및 확인할 수 있습니다.

**새 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 유효성 검사 편집기 | 유효성 검사 편집기에 대한 새로운 개선 사항이 추가되었습니다. 이러한 개선 사항에는 유효성 검사 열, 새 코드 작성 도구 및 향상된 보기가 포함됩니다. |

{style="table-layout:auto"}

Assurance에 대한 자세한 내용은 [보증 설명서](https://developer.adobe.com/client-sdks/documentation/platform-assurance/).

## 데이터 수집 {#data-collection}

Adobe Experience Platform은 클라이언트측 고객 경험 데이터를 수집하여 Adobe Experience Platform Edge Network로 전송하여 Adobe 또는 비 Adobe 대상으로 보강, 변환 및 배포할 수 있는 기술 제품군을 제공합니다.

**새 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 신규 홈 화면 | 데이터 수집 UI의 홈 페이지가 생산성 간소화를 위한 유용한 온보딩 정보 및 링크를 포함하도록 업데이트되었습니다. 여기에는 다음 항목이 포함되어 있습니다.<ol><li>시작하기 위한 설명서 및 권장 워크플로우</li><li>최근 속성, 규칙 및 데이터 요소</li><li>인기 있는 확장</li><li>빠른 설치 기능으로 새로운 확장 업데이트</li></ol> |
| 데이터 보내기 대상 [!DNL Google Ads] 이벤트 전달 사용 | 이제 다음을 사용할 수 있습니다. [[!DNL Google Ads Enhanced Conversions] API 확장](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) 이벤트 전달용, 결합 [Google Oauth 2 비밀](../../tags/ui/event-forwarding/secrets.md#google-oauth2): 서버측 데이터를 로 안전하게 전송합니다. [!DNL Google Ads] 실시간으로. |

{style="table-layout:auto"}

## 대상(업데이트 날짜: 2월 2일) {#destinations}

[!DNL Destinations] 는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 빌드된 통합입니다. 대상을 사용하여 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 다양한 사용 사례에 대해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새 대상**

| 대상 | 설명 |
| ----------- | ----------- |
| [(베타) Adobe Experience Cloud 대상 연결](../../destinations/catalog/adobe/experience-cloud-audiences.md) | 사용 [!UICONTROL (베타) Adobe Experience Cloud 대상] 연결을 통해 Audience Manager, Analytics, Advertising Cloud, Adobe Campaign, Target 또는 Marketo과 같은 다양한 Experience Platform 솔루션에 Experience Platform의 세그먼트를 공유할 수 있습니다. |
| [Pega 프로필 연결](../../destinations/catalog/personalization/pega-profile.md) | 사용 [!DNL Pega Profile Connector] Adobe Experience Platform에서 의 실시간 아웃바운드 연결을 [!DNL Amazon] Adobe Experience Platform의 프로필 데이터를 CSV 파일로 정기적으로 자체 S3 버킷으로 내보내는 S3 스토리지입니다. 위치 [!DNL Pega Customer Decision Hub], S3 저장소에서 이 프로필 데이터를 가져오도록 데이터 작업을 예약하여 [!DNL Pega Customer Decision Hub] 프로필. |
| [(Beta) 트레이드 데스크 CRM EU 연결](../../destinations/catalog/advertising/tradedesk-emails.md) | EUID(유럽 통합 ID)의 릴리스에서는 이제 두 가지가 표시됩니다 [!DNL The Trade Desk - CRM] 의 대상 [대상 카탈로그](/help/destinations/catalog/overview.md). <ul><li> EU에서 데이터를 소싱하는 경우 다음을 사용하십시오. **[!DNL The Trade Desk - CRM (EU)]** 대상.</li><li> APAC 또는 NAMER 영역에서 데이터를 소싱할 경우 **[!DNL The Trade Desk - CRM (NAMER & APAC)]** 대상. </li></ul> |

**새로운 기능 또는 업데이트된 기능** {#destinations-new-updated-functionality}

| 기능 | 설명 |
| ----------- | ----------- |
| 스트리밍 대상과의 통합을 위한 유료 미디어 동의 정책 개선 | An [동의 정책 시행 개선](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) 날짜 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations) 유료 미디어 활성화 사용 사례의 경우. 프로필이 더 이상 동의 정책에 대한 자격이 없는 경우 이제 Experience Platform은 자신의 정책 종료를 스트리밍 대상으로 미리 전달합니다. <br> <b>참고</b>: 이 기능은 다음 고객에게만 제공됩니다. **[!UICONTROL 개인 정보 보호 및 보안 보호]**&#x200B;및 **[!UICONTROL 헬스케어 실드]**. |
| Beta 클라우드 스토리지 대상 커넥터의 새로운 구분 기호 옵션 | 세 개의 새 구분 기호 옵션(콜론) `:`, 파이프, 세미콜론 `;`) 이제 새로운 beta 클라우드 스토리지 대상에 사용할 수 있습니다. [(베타) Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [(베타) Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md), [(베타) Azure Data Lake Storage Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [(베타) 데이터 랜딩 영역](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [(베타) Google 클라우드 스토리지](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [(베타) SFTP](/help/destinations/catalog/cloud-storage/sftp.md). <br> 지원되는 를 참조하십시오. [파일 서식 옵션](/help/destinations/ui/batch-destinations-file-formatting-options.md) 파일 기반 대상. |
| 에서 사용할 수 있는 새로운 선택적 매개 변수 [고객 데이터 필드](/help/destinations/destination-sdk/destination-configuration.md#customer-data-fields) 의 구성 [Destination SDK](/help/destinations/destination-sdk/overview.md) | `unique`: 사용자 조직에서 설정한 모든 대상 데이터 흐름에서 값이 고유해야 하는 고객 데이터 필드를 만들어야 할 때 이 매개 변수를 사용합니다. <br> 예를 들어 **[!UICONTROL 통합 별칭]** 의 필드 [[!UICONTROL 사용자 정의 개인화]](/help/destinations/catalog/personalization/custom-personalization.md#parameters) 대상은 고유해야 합니다. 즉, 이 대상에 대한 두 개의 개별 데이터 흐름은 이 필드에 대해 동일한 값을 가질 수 없습니다. |

**수정 사항 및 개선 사항** {#destinations-fixes-and-enhancements}

<table>
    <tr>
        <td><b>수정 또는 개선 사항</b></td>
        <td><b>설명</b></td>
    </tr>
    <tr>
        <td>파일 기반 대상으로 내보내기 동작이 업데이트되었습니다(PLAT-123316).</td>
        <td>의 동작에서 문제를 해결했습니다. <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#mandatory-attributes">필수 속성</a> 데이터 파일을 배치 대상으로 내보낼 때 <br> 이전에는 출력 파일의 모든 레코드에 다음 두 항목이 모두 포함되어 있는지 확인했습니다. <ol><li>null이 아닌 값 <code>mandatoryField</code> 열 및</li><li>필수가 아닌 다른 필드 중 하나 이상에서 null이 아닌 값.</li></ol> 두 번째 조건이 제거되었습니다. 그 결과 아래 예와 같이 내보낸 데이터 파일에 더 많은 출력 행이 표시될 수 있습니다.<br> <b> 2023년 1월 릴리스 이전의 샘플 동작 </b> <br> 필수 필드: <code>emailAddress</code> <br> <b>활성화하기 위한 데이터 입력</b> <br><table><thead><tr><th>이름</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>제니퍼</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> <br> <b>활성화 출력</b> <br><table><thead><tr><th>이름</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>제니퍼</td><td>jennifer@acme.com</td></tr></tbody></table> <br> <b> 2023년 1월 릴리스 이후 샘플 동작 </b> <br> <b>활성화 출력</b> <br> <table><thead><tr><th>이름</th><th>emailAddress</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>제니퍼</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> </td>
    </tr>
    <tr>
        <td>필수 매핑 및 중복 매핑에 대한 UI 및 API 유효성 검사(PLAT-123316)</td>
        <td>이제 다음의 경우 UI 및 API에서 유효성 검사가 다음과 같이 시행됩니다. <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#mapping">필드 매핑</a> 대상 활성화 워크플로에서 다음을 수행합니다.<ul><li><b>필수 매핑</b>: 대상 개발자가 필수 매핑을 사용하여 대상을 설정한 경우(예: <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/google-ad-manager-360-connection.html?lang=en">Google Ad Manager 360</a> 대상)을 설정하는 경우 데이터를 대상으로 활성화할 때 사용자가 이러한 필수 매핑을 추가해야 합니다. </li><li><b>중복 매핑</b>: 활성화 워크플로의 매핑 단계에서 소스 필드에는 중복 값을 추가할 수 있지만 대상 필드에는 추가할 수 없습니다. 허용되는 매핑 조합과 금지된 매핑 조합의 예는 아래 표를 참조하십시오. <br><table><thead><tr><th>허용됨/금지됨</th><th>소스 필드</th><th>Target 필드</th></tr></thead><tbody><tr><td>허용됨</td><td><ul><li>email.address</li><li>email.address</li></ul></td><td><ul><li>emailalias1</li><li>이메일 별칭2</li></ul></td></tr><tr><td>금지됨</td><td><ul><li>email.address</li><li>hashed.emails</li></ul></td><td><ul><li>emailalias1</li><li>emailalias1</li></ul></td></tr></tbody></table> </li></ul></td>
    </tr>    
</table>

대상에 대한 일반적인 정보는 [대상 개요](../../destinations/home.md).

## 경험 데이터 모델(XDM) {#xdm}

XDM은 Adobe Experience Platform으로 가져온 데이터에 대한 일반적인 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수함으로써 모든 고객 경험 데이터를 일반적인 표현에 통합하여 보다 빠르고 통합적인 방식으로 통찰력을 제공할 수 있습니다. 고객 작업에서 중요한 통찰력을 얻고, 세그먼트를 통해 고객 대상을 정의하고, 개인화 목적으로 고객 속성을 사용할 수 있습니다.

**새 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 스키마 트리 표시 이름 개선 사항 | 이전에는 UI에 필드 이름이 표시되었지만 지금은 스키마 캔버스에서 스키마 필드의 표시 이름이 보다 사람이 읽기 쉽습니다. |

**새로운 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 클래스 | [[!UICONTROL 전환]](https://github.com/adobe/xdm/blob/master/components/classes/conversion.schema.json) | 통화 전환과 같은 전환 데이터를 추적하기 위한 클래스입니다. |
| 필드 그룹 | [[!UICONTROL 통화 전환율 세부 정보]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/conversion/currency-conversion-details.schema.json) | 다음에 대한 필드 그룹 [!UICONTROL 전환] 클래스, 통화 전환과 관련된 추가 세부 정보 캡처 |
| 필드 그룹 | [[!UICONTROL 동의 정책 평가 결과가 메타데이터로 매핑됨]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResultsv2.schema.jsonn) | 동의 정책 시작에 대한 메타데이터 정보를 포함하여 여러 동의 정책의 평가 결과에 대한 세부 정보를 캡처하고 존재합니다. |

**업데이트된 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 데이터 유형 | [[!UICONTROL 광고 세부 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | 다음 `ID` 필드 이름이 (으)로 바뀌었습니다. `name`및 이전 `name` 필드는 현재 `friendlyName`. |
| 데이터 유형 | [[!UICONTROL 의사 결정 제안 세부 정보]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-detail.schema.json) | 을(를) 추가함 `selectionStrategy` 선택 전략의 세부 사항을 캡처하는 필드입니다. |
| 필드 그룹 | [[!UICONTROL 경험 이벤트 - 제안 상호 작용]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/experienceevent-proposition-interaction.schema.json) | 필드 그룹은 이제 과(와) 호환됩니다. [!UICONTROL 여정 단계 이벤트] 클래스. |
| 데이터 유형 | [[!UICONTROL 오류 세부 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | 다음 `ID` 필드 이름이 (으)로 바뀌었습니다. `name`. |
| 데이터 유형 | [[!UICONTROL 미디어 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/media.schema.json) | 패턴 변경을 비디오 세그먼트 속성으로 되돌렸습니다. |
| 데이터 유형 | [[!UICONTROL Qoe 데이터 세부 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | 을(를) 제거함 `droppedFrameCount` 필드. |
| 데이터 유형 | [[!UICONTROL 세션 세부 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | 이름이 변경됨 `isAuthorized` 필드 대상 `authorized`, 및 업데이트함 `type` 이전에 부울이었던 문자열을 반환합니다. |
| 데이터 유형 | [[!UICONTROL 배송]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | 다음과 같은 몇 가지 새 필드가 추가되었습니다. `shipDate`, `trackingNumber`, 및 `trackingURL`. |
| 필드 그룹 | [[!UICONTROL AJO 엔티티 필드]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity-mixins.schema.json) | 다음과 같은 몇 가지 새 필드가 추가되었습니다. `journeyNodeID`, `journeyNodeName`, 및 `journeyModeType`. |
| 필드 그룹 | [[!UICONTROL 고객 경험 이벤트]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/experienceevent-consumer.schema.json) | 이제 필드 그룹도 과 호환됩니다. [!UICONTROL 요약 지표] 클래스. |
| 필드 그룹 | [[!UICONTROL 제품 트리거]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/product-triggers.schema.json) | 다음 `productTriggers` 이제 필드가 다음에 중첩됩니다. `weather` 개체. |
| 필드 그룹 | [[!UICONTROL 상대 트리거]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/relative-triggers.schema.json) | 다음 `relativeTriggers` 이제 필드가 다음에 중첩됩니다. `weather` 개체. |
| 필드 그룹 | [[!UICONTROL 중증 트리거]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | 다음 `severeTriggers` 이제 필드가 다음에 중첩됩니다. `weather` 개체. |
| 필드 그룹 | [[!UICONTROL 날씨 트리거]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | 다음 `weatherTriggers` 이제 필드가 다음에 중첩됩니다. `weather` 개체. |
| 필드 그룹 | [[!UICONTROL XDM 관련 비즈니스 계정]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account/related-accounts.schema.json) | 필드 그룹은 이제 안정적입니다. |

{style="table-layout:auto"}

플랫폼의 XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md).

## 실시간 고객 프로필 {#profile}

Adobe Experience Platform을 사용하면 고객이 브랜드와 상호 작용하는 장소나 시기에 상관없이 고객이 통합적이고 일관적이며 적절한 경험을 제공할 수 있습니다. 실시간 고객 프로필을 사용하면 온라인, 오프라인, CRM 및 서드파티 데이터를 포함하여 여러 채널의 데이터를 결합하는 각 개별 고객에 대한 거시적인 보기를 확인할 수 있습니다. 프로필을 사용하면 모든 고객 상호 작용에 대해 실행 가능한 타임스탬프 계정을 제공하는 통합 보기로 고객 데이터를 통합할 수 있습니다.

**향후 사용 중단** {#deprecation}

세그먼트 멤버십 라이프사이클에서 중복을 제거하려면 `Existing` 상태는 다음에서 더 이상 사용되지 않습니다: [세그먼트 멤버십 맵](../../xdm/field-groups/profile/segmentation.md) 2023년 3월 말. 후속 발표에는 정확한 사용 중단 날짜가 포함될 예정입니다.

사용 중단 후, 세그먼트에서 적격한 프로필은 다음과 같이 표시됩니다. `Realized` 및 부적격 프로필은 계속 다음과 같이 표시됩니다. `Exited`. 이 경우 를 통해 파일 기반 대상과 동등해집니다. `Active` 및 `Expired` 세그먼트 상태.

이 변경 사항은 을 사용하는 경우 사용자에게 영향을 줄 수 있습니다. [enterprise 대상](../../destinations/destination-types.md#streaming-profile-export) (Amazon Kinesis, Azure Event Hubs, HTTP API) 및 에는 `Existing` 상태. 이러한 경우 다운스트림 통합을 검토하십시오. 특정 시간 이후에 새로 자격을 얻은 프로필을 식별하는 데 관심이 있는 경우 `Realized` 상태 및 `lastQualificationTime` 세그먼트 멤버십 맵에서 을 참조하십시오. 자세한 내용은 Adobe 담당자에게 문의하십시오.

프로필 데이터 작업을 위한 튜토리얼 및 모범 사례를 포함하여 실시간 고객 프로필에 대한 자세한 내용은 [실시간 고객 프로필 개요](../../profile/home.md).

## 세분화 서비스 {#segmentation}

[!DNL Segmentation Service] 은 고객 기반 내에서 마케팅 가능한 사용자 그룹을 구분하는 기준을 설명하여 프로필의 특정 하위 집합을 정의합니다. 세그먼트는 브랜드와의 고객 상호 작용을 나타내는 레코드 데이터(예: 인구 통계학적 정보) 또는 시계열 이벤트를 기반으로 할 수 있습니다.

**새 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 세그먼트 빌더에서 일괄 값 가져오기 | 이제 세그먼트 빌더는 CSV 또는 TSV 파일을 업로드하거나 쉼표로 구분된 값을 수동으로 삽입하여 여러 값 가져오기를 지원합니다. 자세한 내용은 [세그먼트 빌더 안내서](../../segmentation/ui/segment-builder.md#rule-builder-canvas). |
| 외부 대상 멤버십 만료 | 기본적으로 외부 대상 멤버십은 30일 동안 유지됩니다. 이러한 파일을 더 오래 유지하려면 `validUntil` 대상 데이터를 수집하는 동안 필드. |
| 플랫폼에서 생성한 세그먼트 멤버십 만료 | 에 있는 모든 세그먼트 멤버십 `Exited` 를 기준으로 30일 이상 주 `lastQualificationTime` 필드는 삭제될 수 있습니다. |

{style="table-layout:auto"}

에 대한 자세한 내용 [!DNL Segmentation Service], 다음을 참조하십시오. [세그먼테이션 개요](../../segmentation/home.md).

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 해당 데이터를 구조화하고, 레이블을 지정하고, 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 서드파티 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

| 기능 | 설명 |
| --- | --- |
| 사용자가 클라우드 스토리지 소스의 하위 폴더에 액세스할 수 있도록 허용 | 이제 새 계정을 만들 때 클라우드 스토리지 소스의 특정 하위 폴더에 대한 액세스를 정의할 수 있습니다. 이 폴더가 생성되면 사용자는 허용된 하위 폴더의 데이터에만 액세스할 수 있습니다. 이 기능은 다음 클라우드 스토리지 소스에서 사용할 수 있습니다. [Azure Blob 저장소](../../sources/connectors/cloud-storage/blob.md), [Google 클라우드 스토리지](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google Pubsub](../../sources/connectors/cloud-storage/google-pubsub.md), 및 [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| 의 베타 가용성 [!DNL SugarCRM] | [!DNL SugarCRM] 이제 beta에서 소스를 사용할 수 있습니다. 사용 [!DNL SugarCRM Accounts & Contacts] 및 [!DNL SugarCRM Events] 에서 데이터를 가져올 소스 [!DNL SugarCRM] Experience Platform 계정. 자세한 내용은 [[!DNL SugarCRM] 개요](../../sources/connectors/crm/sugarcrm.md). |