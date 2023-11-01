---
title: Adobe Experience Platform 릴리스 정보 2023년 1월
description: Adobe Experience Platform의 2023년 1월 릴리스 정보입니다.
exl-id: 461898ce-5683-4ab1-9167-ac25843a1ff8
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '2408'
ht-degree: 99%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 일자: 2023년 1월 25일**

Adobe Experience Platform의 기존 기능 업데이트:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai/ml-services)
- [보증](#assurance)
- [데이터 수집](#data-collection)
- [[!DNL Destinations]](#destinations)
- [경험 데이터 모델 (XDM)](#xdm)
- [실시간 고객 프로필](#profile)
- [Segmentation Service](#segmentation)
- [소스](#sources)

## 인공 지능/머신 러닝 서비스 {#ai-ml}

인공 지능 및 머신 러닝 서비스는 마케팅 분석가 및 실무자가 고객 경험 사용 사례에서 AI/ML의 기능을 활용할 수 있도록 지원합니다. 이를 통해 마케팅 분석가는 비즈니스 수준의 구성을 통해 회사의 요구 사항에 따라 데이터 과학 전문 지식 없이도 예측을 설정할 수 있습니다.

### 기여도 AI

기여도 AI는 전환 이벤트로 연결되는 터치포인트에 크레딧을 적용하는 데 사용됩니다. 이를 통해 마케터는 고객 여정 전반에서 각 개별 마케팅 터치포인트의 마케팅 효과를 수량화할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| HIPAA 준비 | Healthcare Shield 고객은 이제 기여도 AI 및 기타 특정 Experience Platform 기반의 애플리케이션에서 보호된 상태 정보를 수신, 사용, 유지 관리 또는 전송할 수 있습니다. Healthcare Shield는 HIPAA의 적용을 받는 법인 또는 비즈니스 제휴자인 의료 고객을 위한 것입니다. 자세한 내용은 [HIPAA, Adobe 제품 및 서비스](https://www.adobe.com/kr/trust/compliance/hipaa-ready.html)에 관한 설명서를 참조하십시오. |
| 추가 점수 데이터 세트 열 편집 | 이제 기존 모델을 편집할 때 추가 점수 데이터 세트 열(보고 열)을 추가하거나 제거할 수 있습니다. 이렇게 하면 속성 점수의 유연성이 확장되어 모델이 이미 생성된 후 추가 차원에 대한 인사이트를 제공합니다. 자세한 내용은 [기여도 UI 안내서](../../intelligent-services/attribution-ai/user-guide.md)를 참조하십시오. |

{style="table-layout:auto"}

자세한 내용은 [AI/ML 서비스](../../intelligent-services/attribution-ai/overview.md) 개요를 참조하십시오.

### 고객 AI

Real-Time Customer Data Platform용 고객 AI를 사용하여 크기에 따라 개별 프로필에 대한 변경 및 전환과 같은 사용자 정의 성향 점수를 생성할 수 있습니다. 비즈니스 요구 사항을 머신 러닝 문제로 변환하거나 알고리즘을 선택하거나 교육 또는 배포하지 않아도 됩니다.

**업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| HIPAA 준비 | Healthcare Shield 고객은 이제 Real-Time Customer Data Platform용 고객 AI 및 기타 특정 Experience Platform 기반의 애플리케이션에서 보호된 상태 정보를 수신, 사용, 유지 관리 또는 전송할 수 있습니다. Healthcare Shield는 HIPAA의 적용을 받는 법인 또는 비즈니스 제휴자인 의료 고객을 위한 것입니다. 자세한 내용은 [HIPAA, Adobe 제품 및 서비스](https://www.adobe.com/kr/trust/compliance/hipaa-ready.html)에 관한 설명서를 읽어 보십시오. |

{style="table-layout:auto"}

자세한 내용은 [AI/ML 서비스](../../intelligent-services/customer-ai/overview.md) 개요를 참조하십시오.

## 보증 {#assurance}

Adobe Assurance를 사용하면 모바일 앱에서 데이터를 수집하거나 경험을 제공하는 방식을 검사하고, 증명하고, 시뮬레이션하고, 검증할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 유효성 검사 편집기 | 유효성 검사 편집기에 대한 새로운 개선 사항이 추가되었습니다. 이러한 개선 사항에는 유효성 검사 열, 새로운 코드 작성 도구 및 향상된 보기가 포함됩니다. |

{style="table-layout:auto"}

Assurance에 대한 자세한 내용은 [Assurance 설명서](https://developer.adobe.com/client-sdks/documentation/platform-assurance/)를 참조하십시오.

## 데이터 수집 {#data-collection}

Adobe Experience Platform은 클라이언트측 고객 경험 데이터를 수집하여 Adobe 또는 비 Adobe 대상으로 보강, 변환 및 배포가 가능한 Adobe Experience Platform Edge Network로 보낼 수 있는 기술 제품군을 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 새로운 기능 홈 화면 | 데이터 수집 UI의 홈 페이지가 업데이트되어 유용한 온보딩 정보와 생산성 간소화를 위한 링크가 포함되었습니다. 여기에는 다음 항목이 포함되어 있습니다.<ol><li>시작을 위한 설명서 및 권장 워크플로</li><li>최근 속성, 규칙 및 데이터 요소</li><li>자주 사용하는 확장 기능</li><li>빠른 설치 기능을 통한 새로운 확장 기능 업데이트</li></ol> |
| 이벤트 전달을 사용하여 [!DNL Google Ads]로 데이터 전송 | 이제 [Google Oauth 2 Secret](../../tags/ui/event-forwarding/secrets.md#google-oauth2)과 함께 이벤트 전달을 위한 [[!DNL Google Ads Enhanced Conversions] API 확장 기능](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md)을 사용하여 서버측 데이터를 [!DNL Google Ads]에 실시간으로 안전하게 전송할 수 있습니다. |

{style="table-layout:auto"}

## 대상 (2월 2일 업데이트됨) {#destinations}

[!DNL Destinations]는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있는 대상 플랫폼과 사전 설치된 통합입니다. 대상을 사용해 교차 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 대상**

| 대상 | 설명 |
| ----------- | ----------- |
| [(Beta) Adobe Experience Cloud Audiences 연결](../../destinations/catalog/adobe/experience-cloud-audiences.md) | [!UICONTROL (Beta) Adobe Experience Cloud 대상자] 연결을 사용하여 Experience Platform에서 Audience Manager, Analytics, Advertising Cloud, Adobe Campaign, Target 또는 Marketo 등의 여러 Experience Platform 솔루션으로 세그먼트를 공유합니다. |
| [Pega 프로필 연결](../../destinations/catalog/personalization/pega-profile.md) | Adobe Experience Platform의 [!DNL Pega Profile Connector]를 사용하여 [!DNL Amazon] S3 스토리지에 대한 실시간 아웃바운드 연결을 만들어 주기적으로 자체 S3 버킷 내의 Adobe Experience Platform의 CSV 파일로 프로필 데이터를 내보냅니다. [!DNL Pega Customer Decision Hub]에서는 S3 스토리지에서 이 프로필 데이터를 가져와서 [!DNL Pega Customer Decision Hub] 프로필을 업데이트하도록 데이터 작업을 예약할 수 있습니다 |
| [(Beta) The Trade Desk CRM EU 연결](../../destinations/catalog/advertising/tradedesk-emails.md) | EUID(유럽 통합 ID)가 출시되면서 이제 두 개의 [!DNL The Trade Desk - CRM] 대상이 [대상 카탈로그](/help/destinations/catalog/overview.md)에 표시됩니다. <ul><li> EU에서 소스 데이터를 제공하는 경우 **[!DNL The Trade Desk - CRM (EU)]** 대상을 사용하십시오.</li><li> APAC 또는 NAMER 지역에서 소스 데이터를 제공하는 경우 **[!DNL The Trade Desk - CRM (NAMER & APAC)]** 대상을 사용하십시오. </li></ul> |

**새로운 기능 또는 업데이트된 기능** {#destinations-new-updated-functionality}

| 기능 | 설명 |
| ----------- | ----------- |
| 스트리밍 대상과의 통합을 위한 유료 미디어 동의 정책 개선 사항 | 유료 미디어 활성화 사용 사례에 대한 [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations)에 대한 [동의 정책 시행 기능의 개선 사항](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement)입니다. 프로필이 더 이상 동의 정책에 적합하지 않은 경우 Experience Platform은 이제 해당 정책 종료를 스트리밍 대상에 미리 전달합니다. <br> <b>참고</b>: 이 기능은 **[!UICONTROL Privacy and Security Shield]** 및 **[!UICONTROL Healthcare Shield]** 고객에게만 제공됩니다 |
| 베타 클라우드 스토리지 대상 커넥터에 대한 새로운 구분 기호 옵션 | 이제 [(Beta) Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [(Beta) Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md), [(Beta) Azure Data Lake Storage Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [(Beta) 데이터 랜딩 영역](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [(Beta) Google Cloud Storage](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [(Beta) SFTP](/help/destinations/catalog/cloud-storage/sftp.md)와 같은 새로운 베타 클라우드 스토리지 대상에 세 가지 새로운 구분 기호 옵션(콜론 `:`, 파이프, 세미콜론 `;`) 을 사용할 수 있습니다. <br> 파일 기반 대상에 대해 지원되는 [파일 형식 지정 옵션](/help/destinations/ui/batch-destinations-file-formatting-options.md)에 대해 읽어 보십시오. |
| [Destination SDK](/help/destinations/destination-sdk/overview.md)의 [고객 데이터 필드](/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md) 구성에서 사용할 수 있는 새로운 옵션 매개변수 | `unique`: 사용자 조직에서 설정한 모든 대상 데이터 흐름에서 값이 고유한 고객 데이터 필드를 생성해야 하는 경우 이 매개변수를 사용합니다. <br> 예를 들면 [[!UICONTROL 사용자 정의 개인 설정]](/help/destinations/catalog/personalization/custom-personalization.md#parameters) 대상의 **[!UICONTROL 통합 별칭]** 필드는 고유해야 하며, 이 대상으로 전송되는 두 개의 개별 데이터 흐름은 이 필드에 대해 동일한 값을 가질 수 없습니다. |

**수정 사항 및 개선 사항** {#destinations-fixes-and-enhancements}

<table>
    <tr>
        <td><b>수정 사항 또는 개선 사항</b></td>
        <td><b>설명</b></td>
    </tr>
    <tr>
        <td>파일 기반 대상으로 내보내기 동작 업데이트됨 (PLAT-123316)</td>
        <td>데이터 파일을 일괄 처리 대상으로 내보낼 때 <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html#mandatory-attributes">필수 속성</a> 동작에서 문제를 해결했습니다. <br> 이전에는 출력 파일의 모든 레코드가 다음 두 가지를 모두 포함하는 것으로 확인되었습니다. <ol><li><code>mandatoryField</code> 열의 null이 아닌 값 및</li><li>필수가 아닌 다른 필드 중 하나 이상에서 null이 아닌 값.</li></ol> 두 번째 조건이 제거되었습니다. 그 결과 다음 예와 같이 내보낸 데이터 파일에 더 많은 출력 행이 표시될 수 있습니다.<br> <b> 2023년 1월 릴리스 이전의 샘플 동작 </b> <br> 필수 필드: <code>emailAddress</code> <br> <b>활성화할 데이터 입력</b> <br><table><thead><tr><th>이름</th><th>이메일 주소</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> <br> <b>활성화 출력</b> <br><table><thead><tr><th>이름</th><th>이메일 주소</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr></tbody></table> <br> <b> 2023년 1월 릴리스 이후의 샘플 동작 </b> <br> <b>활성화 출력</b> <br> <table><thead><tr><th>이름</th><th>이메일 주소</th></tr></thead><tbody><tr><td>John</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>Jenifer</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> </td>
    </tr>
    <tr>
        <td>필수 매핑 및 중복 매핑에 대한 UI 및 API 유효성 검사 (PLAT-123316)</td>
        <td>이제 활성화 대상 워크플로의 <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html#mapping">필드를 매핑</a>할 때 UI 및 API에 다음과 같이 유효성 검사가 시행됩니다.<ul><li><b>필수 매핑</b>: 대상 개발자가 필수 매핑(예: <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/advertising/google-ad-manager-360-connection.html">Google Ad Manager 360</a> 대상)을 사용하여 대상을 설정한 경우 사용자가 대상에 데이터를 활성화할 때 이러한 필수 매핑을 추가해야 합니다. </li><li><b>중복 매핑</b>: 활성화 워크플로의 매핑 단계에서 소스 필드에 중복 값을 추가할 수 있지만 대상 필드에는 추가할 수 없습니다. 허용 및 금지 매핑 조합의 예는 아래 표를 참조하십시오. <br><table><thead><tr><th>허용/금지</th><th>소스 필드</th><th>대상 필드</th></tr></thead><tbody><tr><td>허용됨</td><td><ul><li>email.address</li><li>email.address</li></ul></td><td><ul><li>emailalias1</li><li>이메일   별칭2</li></ul></td></tr><tr><td>금지</td><td><ul><li>email.address</li><li>hashed.emails</li></ul></td><td><ul><li>emailalias1</li><li>emailalias1</li></ul></td></tr></tbody></table> </li></ul></td>
    </tr>    
</table>

대상에 대한 일반적인 정보는 [대상 개요](../../destinations/home.md)를 참조하십시오.

## 경험 데이터 모델 (XDM) {#xdm}

XDM은 Adobe Experience Platform으로 가져오는 데이터에 대한 공통 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수하여 모든 고객 경험 데이터를 공통된 표현에 통합해 보다 빠르고 통합된 방식으로 인사이트를 제공할 수 있습니다. 고객 조치에서 귀중한 인사이트를 얻고, 세그먼트를 통해 고객 대상자를 정의하고, 개인 설정 목적으로 고객 속성을 사용할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 스키마 트리 표시 이름 개선 사항 | 이전에는 필드 이름이 UI에 표시되었지만, 이제는 스키마 캔버스의 스키마 필드에 대한 표시 이름이 읽기에 더 수월합니다. |

**새로운 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 클래스 | [[!UICONTROL 전환]](https://github.com/adobe/xdm/blob/master/components/classes/conversion.schema.json) | 통화 전환과 같은 전환 데이터를 추적하기 위한 클래스입니다. |
| 필드 그룹 | [[!UICONTROL 통화 전환율 세부 정보]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/conversion/currency-conversion-details.schema.json) | 통화 전환과 관련된 추가 세부 정보를 캡처하는 [!UICONTROL 전환] 클래스의 필드 그룹입니다. |
| 필드 그룹 | [[!UICONTROL 메타데이터와 동의 정책 평가 결과 매핑]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResultsv2.schema.jsonn) | 동의 정책의 시작과 끝에 대한 메타데이터 정보를 포함하여 여러 동의 정책의 평가 결과에 대한 세부 정보를 캡처합니다. |

**업데이트된 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 데이터 유형 | [[!UICONTROL 광고 상세 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | `ID` 필드 이름은 `name`으로 변경되며, 이전 `name` 필드는 이제 `friendlyName`입니다. |
| 데이터 유형 | [[!UICONTROL 의사 결정 제안 세부 사항]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-detail.schema.json) | 선택 전략의 세부 정보를 캡처하는 `selectionStrategy` 필드가 추가되었습니다. |
| 필드 그룹 | [[!UICONTROL 경험 이벤트 - 제안 상호 작용]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/experienceevent-proposition-interaction.schema.json) | 이제 필드 그룹은 [!UICONTROL 고객 여정 단계] 클래스와 호환됩니다. |
| 데이터 유형 | [[!UICONTROL 오류 세부 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | `ID` 필드 이름이 `name`으로 변경되었습니다. |
| 데이터 유형 | [[!UICONTROL 미디어 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/media.schema.json) | 패턴의 변경 사항을 비디오 세그먼트 속성으로 복구하였습니다. |
| 데이터 유형 | [[!UICONTROL Qoe 데이터 세부 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | `droppedFrameCount` 필드가 제거되었습니다. |
| 데이터 유형 | [[!UICONTROL 세션 세부 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | 이전에 부울이었을 때 `isAuthorized` 필드 이름을 `authorized`로 변경하였으며, `type`을 문자열로 업데이트하였습니다. |
| 데이터 유형 | [[!UICONTROL 배송]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | `shipDate`, `trackingNumber` 및 `trackingURL`과 같은 몇 가지 새 필드를 추가했습니다. |
| 필드 그룹 | [[!UICONTROL AJO 엔티티 필드]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity-mixins.schema.json) | `journeyNodeID`, `journeyNodeName` 및 `journeyModeType`과 같은 몇 가지 새 필드를 추가했습니다. |
| 필드 그룹 | [[!UICONTROL 고객 경험 이벤트]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/experienceevent-consumer.schema.json) | 또한 이제 필드 그룹은 [!UICONTROL 요약 지표] 클래스와 호환됩니다. |
| 필드 그룹 | [[!UICONTROL 제품 트리거]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/product-triggers.schema.json) | 이제 `productTriggers` 필드는 `weather` 오브젝트 아래에 중첩됩니다. |
| 필드 그룹 | [[!UICONTROL 상대적 트리거]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/relative-triggers.schema.json) | 이제 `relativeTriggers` 필드는 `weather` 오브젝트 아래에 중첩됩니다. |
| 필드 그룹 | [[!UICONTROL 심각한 트리거]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | 이제 `severeTriggers` 필드는 `weather` 오브젝트 아래에 중첩됩니다. |
| 필드 그룹 | [[!UICONTROL 날씨 트리거]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | 이제 `weatherTriggers` 필드는 `weather` 오브젝트 아래에 중첩됩니다. |
| 필드 그룹 | [[!UICONTROL XDM 관련 비즈니스 계정]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account/related-accounts.schema.json) | 이제 필드 그룹이 안정되었습니다. |

{style="table-layout:auto"}

Platform의 XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md)를 참조하십시오.

## 실시간 고객 프로필 {#profile}

Adobe Experience Platform을 사용하면 고객이 언제 어디서 브랜드와 상호 작용하는지에 관계없이 고객을 위한 조직화되고 일관되며 관련성 높은 경험을 제공할 수 있습니다. 실시간 고객 프로필을 사용하면 온라인, 오프라인, CRM 및 서드파티 데이터를 비롯한 여러 채널의 데이터를 결합하여 각 개별 고객에 대한 거시적인 보기를 확인할 수 있습니다. 프로필을 사용하면 모든 고객의 상호 작용에 대해 실행 가능한 타임스탬프가 지정된 계정을 제공하는 통합 보기로 고객 데이터를 통합할 수 있습니다.

**사용 중단 예정** {#deprecation}

2023년 3월 말에 `Existing` 상태는 세그먼트 멤버십 수명 주기에서 중복을 없애기 위해 [세그먼트 멤버십 맵](../../xdm/field-groups/profile/segmentation.md)에서 더 이상 사용되지 않습니다. 후속 공지에는 정확한 사용 중단 날짜가 포함됩니다.

사용 중단 후에 세그먼트에 적격한 프로필은 `Realized`로 표시되고, 부적격 프로필은 계속 `Exited`로 표시됩니다. 이렇게 하면 `Active` 및 `Expired` 세그먼트 상태의 파일 기반 대상과 동등해집니다.

[기업 대상](../../destinations/destination-types.md#streaming-profile-export)(Amazon Kinesis, Azure Event Hubs, HTTP API)을 사용하고 있으며 `Existing` 상태에 따라 자동화된 다운스트림 프로세스가 있을 경우 이러한 변경 사항은 영향을 미칠 수 있습니다. 이 경우에 해당하는 경우 다운스트림 통합을 검토하십시오. 특정 시간 이후에 새로 인증된 프로필을 확인하려는 경우 세그먼트 멤버십 맵에서 `Realized` 상태 및 `lastQualificationTime`을 조합하여 사용하도록 하십시오. 자세한 내용은 Adobe 담당자에게 문의하십시오.

프로필 데이터 작업에 대한 튜토리얼 및 모범 사례를 포함하여 실시간 고객 프로필에 대해 자세히 알아보려면 [실시간 고객 프로필 개요](../../profile/home.md)를 참조하십시오.

## Segmentation Service {#segmentation}

[!DNL Segmentation Service]는 고객 기반 내에서 마케팅 가능한 사용자 그룹을 구분하는 기준을 설명하여 프로필의 특정 하위 집합을 정의합니다. 세그먼트는 기록 데이터(예: 인구 통계 정보) 또는 고객과 브랜드의 상호 작용을 나타내는 시계열 이벤트를 기반으로 할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 세그먼트 빌더에서 일괄 처리 값 가져오기 | 세그먼트 빌더는 이제 CSV 또는 TSV 파일을 업로드하거나 쉼표로 구분된 값을 수동으로 삽입하여 여러 값 가져오기를 지원합니다. 더 자세한 내용은 [세그먼트 빌더 안내서](../../segmentation/ui/segment-builder.md#rule-builder-canvas)에서 확인할 수 있습니다. |
| 외부 대상자 멤버십 만료 | 기본적으로 외부 대상자 멤버십은 30일 동안 유지됩니다. 더 오래 유지하려면 대상자 데이터를 수집하는 동안 `validUntil` 필드를 사용합니다. |
| Platform에서 생성된 세그먼트 멤버십 만료 | `lastQualificationTime` 필드를 기준으로 30일 넘게 `Exited` 상태에 있는 세그먼트 멤버십은 삭제될 수 있습니다. |

{style="table-layout:auto"}

[!DNL Segmentation Service]에 대한 자세한 내용은 [세분화 개요](../../segmentation/home.md)를 참조하십시오.

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 해당 데이터를 구조화하고, 라벨링하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 서드파티 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

| 기능 | 설명 |
| --- | --- |
| 클라우드 스토리지 소스의 하위 폴더에 대한 사용자 액세스 허용 | 이제 새 계정을 만들 때 클라우드 스토리지 소스의 특정 하위 폴더에 대한 액세스를 정의할 수 있습니다. 생성되면 사용자는 허용된 하위 폴더의 데이터에만 액세스할 수 있습니다. 이 기능은 [Azure Blob Storage](../../sources/connectors/cloud-storage/blob.md), [Google Cloud Storage](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md) 및 [SFTP](../../sources/connectors/cloud-storage/sftp.md)와 같은 클라우드 스토리지 소스에서 사용할 수 있습니다. |
| [!DNL SugarCRM]의 Beta 가용성 | [!DNL SugarCRM] 소스는 이제 베타 버전으로 제공됩니다. [!DNL SugarCRM Accounts & Contacts] 및 [!DNL SugarCRM Events] 소스를 사용하여 데이터를 사용자의 [!DNL SugarCRM] 계정에서 Experience Platform으로 가져옵니다. 자세한 내용은 [[!DNL SugarCRM] 개요](../../sources/connectors/crm/sugarcrm.md)를 참조하십시오. |
