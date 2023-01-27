---
title: Adobe Experience Platform 릴리스 노트 - 2023년 1월
description: Adobe Experience Platform에 대한 2023년 1월 릴리스 노트입니다.
source-git-commit: 3ea2ac1b048adb14aa93b42e5b23ea70bb995414
workflow-type: tm+mt
source-wordcount: '1905'
ht-degree: 4%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2023년 1월 25일**

Adobe Experience Platform의 기존 기능 업데이트:

- [보증](#assurance)
- [데이터 수집](#data-collection)
- [[!DNL Destinations]](#destinations)
- [XDM(경험 데이터 모델)](#xdm)
- [실시간 고객 프로필](#profile)
- [세분화 서비스](#segmentation)
- [소스](#sources)

## 보증 {#assurance}

Adobe 보증을 사용하면 모바일 앱에서 데이터를 수집하거나 경험을 제공하는 방법을 검사, 증명, 시뮬레이션 및 확인할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 유효성 검사 편집기 | 유효성 검사 편집기에 대한 새로운 개선 사항이 추가되었습니다. 이러한 개선 사항에는 유효성 검사 열, 새 코드 작성 도구 및 향상된 보기가 포함됩니다. |

{style=&quot;table-layout:auto&quot;}

Assurance에 대한 자세한 내용은 [보증 설명서](https://developer.adobe.com/client-sdks/documentation/platform-assurance/).

## 데이터 수집 {#data-collection}

Adobe Experience Platform은 클라이언트측 고객 경험 데이터를 수집하고 Adobe Experience Platform Edge Network로 전송하여 Adobe 또는 비Adobe 대상으로 보강, 변환 및 배포할 수 있는 기술 세트를 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 신규 홈 화면 | 데이터 수집 UI의 홈 페이지가 생산성을 간소화하기 위해 유용한 온보딩 정보 및 링크를 포함하도록 업데이트되었습니다. 여기에는 다음 항목이 포함되어 있습니다.<ol><li>시작하는 설명서 및 권장 워크플로우</li><li>최근 속성, 규칙 및 데이터 요소</li><li>인기 있는 확장</li><li>빠른 설치 기능으로 새로운 확장 업데이트</li></ol> |
| 에 데이터 보내기 [!DNL Google Ads] 이벤트 전달 사용 | 이제 를 사용할 수 있습니다 [[!DNL Google Ads Enhanced Conversions] API 확장](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) 이벤트 전달에 대해 다음을 결합합니다. [Google Oauth 2 비밀](../../tags/ui/event-forwarding/secrets.md#google-oauth2)으로 데이터를 안전하게 [!DNL Google Ads] 실시간으로 |

{style=&quot;table-layout:auto&quot;}

## 대상 {#destinations}

[!DNL Destinations] 는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 구축된 통합입니다. 대상을 사용하여 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례에 대해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새 대상**

| 대상 | 설명 |
| ----------- | ----------- |
| [(베타) Adobe Experience Cloud 대상 연결](../../destinations/catalog/adobe/experience-cloud-audiences.md) | 를 사용하십시오 [!UICONTROL (베타) Adobe Experience Cloud 대상] Experience Platform에서 Audience Manager, Analytics, Advertising Cloud, Adobe Campaign, Target 또는 Marketo과 같은 다양한 Experience Platform 솔루션으로 세그먼트를 공유할 수 있는 연결입니다. |
| [Pega 프로필 연결](../../destinations/catalog/personalization/pega-profile.md) | 를 사용하십시오 [!DNL Pega Profile Connector] Adobe Experience Platform에서 를 통해 [!DNL Amazon] S3 저장소를 사용하여 프로필 데이터를 Adobe Experience Platform의 CSV 파일로 주기적으로 S3 버킷으로 내보냅니다. in [!DNL Pega Customer Decision Hub]로 지정하는 경우 데이터 작업을 예약하여 S3 저장소에서 이 프로필 데이터를 가져와 업데이트할 수 있습니다 [!DNL Pega Customer Decision Hub] 프로필 참조. |
| [(베타) Trade Desk CRM EU 연결](../../destinations/catalog/advertising/tradedesk-emails.md) | EUID(유럽 통합 ID)가 릴리스되면 이제 두 가지 기능이 표시됩니다 [!DNL The Trade Desk - CRM] 의 대상 [대상 카탈로그](/help/destinations/catalog/overview.md). <ul><li> EU에서 데이터를 소스에 사용하는 경우 **[!DNL The Trade Desk - CRM (EU)]** 대상.</li><li> APAC 또는 NAMEER 지역에서 데이터를 가져오는 경우 **[!DNL The Trade Desk - CRM (NAMER & APAC)]** 대상. </li></ul> |

**새 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ----------- | ----------- |
| 스트리밍 대상과의 통합을 위한 유료 미디어 동의 개선 사항 | 개선 사항 [동의 정책 시행](/help/data-governance/enforcement/auto-enforcement.md) on [스트리밍 대상](/help/destinations/destination-types.md#streaming-destinations) 유료 미디어 활성화 사용 사례의 경우. 특정 경험에서 동의를 철회한 프로필은 이제 이러한 대상에서 미리 제거됩니다. <br> <b>참고</b>: 이 기능은 **[!UICONTROL 개인 정보 및 보안 차단]**, 및 **[!UICONTROL 의료 보호]**. |
| 베타 클라우드 저장소 대상 커넥터에 대한 새로운 구분 기호 옵션 | 세 개의 새 구분 기호 옵션(콜론) `:`, 파이프, 세미콜론 `;`) 이제 새로운 베타 클라우드 스토리지 대상에 대해 사용할 수 있습니다. [(베타) Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md), [(베타) Azure Blob](/help/destinations/catalog/cloud-storage/azure-blob.md), [(베타) Azure Data Lake Storage Gen2](/help/destinations/catalog/cloud-storage/adls-gen2.md), [(베타) 데이터 랜딩 영역](/help/destinations/catalog/cloud-storage/data-landing-zone.md), [(베타) Google 클라우드 스토리지](/help/destinations/catalog/cloud-storage/google-cloud-storage.md), [(베타) SFTP](/help/destinations/catalog/cloud-storage/sftp.md). <br> 지원되는 항목에 대해 읽기 [파일 서식 옵션](/help/destinations/ui/batch-destinations-file-formatting-options.md) 파일 기반 대상. |
| 에서 사용할 수 있는 새로운 선택적 매개 변수 [고객 데이터 필드](/help/destinations/destination-sdk/destination-configuration.md#customer-data-fields) 구성 [Destination SDK](/help/destinations/destination-sdk/overview.md) | `unique`: 사용자 조직에서 설정한 모든 대상 데이터 흐름에서 값이 고유해야 하는 고객 데이터 필드를 만들어야 하는 경우 이 매개 변수를 사용하십시오. <br> 예: **[!UICONTROL 통합 별칭]** 의 필드 [[!UICONTROL 사용자 지정 개인화]](/help/destinations/catalog/personalization/custom-personalization.md#parameters) 대상은 고유해야 합니다. 즉, 이 대상에 대해 두 개의 개별 데이터 흐름이 이 필드에 대해 동일한 값을 가질 수 없습니다. |

**수정 사항 및 향상된 기능** {#destinations-fixes-and-enhancements}

<table>
    <tr>
        <td><b>수정 또는 개선 사항</b></td>
        <td><b>설명</b></td>
    </tr>
    <tr>
        <td>파일 기반 대상으로 내보내기 동작이 업데이트되었습니다(PLAT-123316).</td>
        <td>의 동작에서 문제가 해결되었습니다. <a href="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#mandatory-attributes">필수 속성</a> 데이터 파일을 배치 대상으로 내보낼 때 <br> 이전에는 출력 파일의 모든 레코드에 다음 두 항목이 모두 포함되어 있는지 확인했습니다. <ol><li>Null이 아닌 값 <code>mandatoryField</code> 열 및</li><li>다른 필수 필드가 아닌 필드 중 하나 이상에 null이 아닌 값입니다.</li></ol> 두 번째 조건이 제거되었습니다. 따라서 아래 예와 같이 내보낸 데이터 파일에 더 많은 출력 행을 볼 수 있습니다.<br> <b> 2023년 1월 릴리스 전 샘플 동작 </b> <br> 필수 필드: <code>emailAddress</code> <br> <b>활성화할 데이터 입력</b> <br><table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>존</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>제니퍼</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> <br> <b>활성화 출력</b> <br><table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>존</td><td>john@acme.com</td></tr><tr><td>제니퍼</td><td>jennifer@acme.com</td></tr></tbody></table> <br> <b> 2023년 1월 릴리스 이후 샘플 동작 </b> <br> <b>활성화 출력</b> <br> <table><thead><tr><th>firstName</th><th>emailAddress</th></tr></thead><tbody><tr><td>존</td><td>john@acme.com</td></tr><tr><td>null</td><td>peter@acme.com</td></tr><tr><td>제니퍼</td><td>jennifer@acme.com</td></tr><tr><td>null</td><td>diana@acme.com</td></tr></tbody></table> </td>
    </tr>
</table>

대상에 대한 자세한 내용은 [대상 개요](../../destinations/home.md).

## XDM(경험 데이터 모델) {#xdm}

XDM은 Adobe Experience Platform으로 가져온 데이터에 대한 일반적인 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수함으로써 모든 고객 경험 데이터를 공통 표현으로 통합하여 보다 빠르고 통합된 방식으로 통찰력을 제공할 수 있습니다. 고객 작업을 통해 유용한 통찰력을 얻을 수 있고, 세그먼트를 통해 고객 대상을 정의하고, 개인화를 위해 고객 속성을 사용할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 문자열 필드에 대해 제안된 값 비활성화 | 이제 다음을 수행할 수 있습니다 [문자열 필드에 대해 개별 제안 값 비활성화](../../xdm/ui/fields/enum.md) 에서 [!UICONTROL 스키마] 표준 구성 요소의 작업 공간을 포함합니다. 이 기능은 제안된 값이 있는 필드에만 사용할 수 있으며 열거형 제약 조건에는 지원되지 않습니다. |

**새로운 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 클래스 | [[!UICONTROL 전환]](https://github.com/adobe/xdm/blob/master/components/classes/conversion.schema.json) | 통화 전환과 같은 전환 데이터를 추적하는 클래스입니다. |
| 필드 그룹 | [[!UICONTROL 통화 변환율 상세내역]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/conversion/currency-conversion-details.schema.json) | 에 대한 필드 그룹 [!UICONTROL 전환] 분류, 통화 변환과 관련된 추가 세부 정보를 캡처합니다. |
| 필드 그룹 | [[!UICONTROL 동의 정책 평가 결과 및 메타데이터가 매핑됩니다]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResultsv2.schema.jsonn) | 동의 정책 입장 및 존재에 대한 메타데이터 정보를 포함하여 여러 동의 정책의 평가 결과에 대한 세부 정보를 캡처합니다. |

**업데이트된 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 데이터 유형 | [[!UICONTROL 광고 세부 사항 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json) | 다음 `ID` 필드의 이름이 `name`, 및 이전 `name` 이제 필드 `friendlyName`. |
| 데이터 유형 | [[!UICONTROL 의사 결정 제안 세부 정보]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-detail.schema.json) | 를 추가했습니다. `selectionStrategy` 선택 전략의 세부 사항을 캡처하는 필드입니다. |
| 필드 그룹 | [[!UICONTROL 경험 이벤트 - 제안 상호 작용]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/experienceevent-proposition-interaction.schema.json) | 이제 필드 그룹이 [!UICONTROL 여정 단계 이벤트] 클래스 이름을 지정합니다. |
| 데이터 유형 | [[!UICONTROL 오류 세부 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/errordetails.schema.json) | 다음 `ID` 필드의 이름이 `name`. |
| 데이터 유형 | [[!UICONTROL 미디어 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/media.schema.json) | 패턴의 변경 사항을 비디오 세그먼트 속성에 되돌렸습니다. |
| 데이터 유형 | [[!UICONTROL Qoe 데이터 세부 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | 제거된 `droppedFrameCount` 필드. |
| 데이터 유형 | [[!UICONTROL 세션 세부 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | 이름이 `isAuthorized` 필드 대상 `authorized`, 및 를 업데이트함 `type` 이전 JavaScript가 부울일 때 문자열로 가져와야 합니다. |
| 데이터 유형 | [[!UICONTROL 배송]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | 다음과 같은 몇 개의 새 필드가 추가되었습니다. `shipDate`, `trackingNumber`, 및 `trackingURL`. |
| 필드 그룹 | [[!UICONTROL AJO 엔티티 필드]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity-mixins.schema.json) | 다음과 같은 몇 개의 새 필드가 추가되었습니다. `journeyNodeID`, `journeyNodeName`, 및 `journeyModeType`. |
| 필드 그룹 | [[!UICONTROL 소비자 경험 이벤트]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/experienceevent-consumer.schema.json) | 이제 필드 그룹이 와 호환됩니다 [!UICONTROL 요약 지표] 클래스 이름을 지정합니다. |
| 필드 그룹 | [[!UICONTROL 제품 트리거]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/product-triggers.schema.json) | 다음 `productTriggers` 이제 필드가 아래의 중첩됩니다. `weather` 개체. |
| 필드 그룹 | [[!UICONTROL 상대 트리거]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/relative-triggers.schema.json) | 다음 `relativeTriggers` 이제 필드가 아래의 중첩됩니다. `weather` 개체. |
| 필드 그룹 | [[!UICONTROL 심각한 트리거]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | 다음 `severeTriggers` 이제 필드가 아래의 중첩됩니다. `weather` 개체. |
| 필드 그룹 | [[!UICONTROL 날씨 트리거]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/severe-triggers.schema.json) | 다음 `weatherTriggers` 이제 필드가 아래의 중첩됩니다. `weather` 개체. |
| 필드 그룹 | [[!UICONTROL XDM 관련 비즈니스 계정]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account/related-accounts.schema.json) | 필드 그룹은 이제 안정되었습니다. |

{style=&quot;table-layout:auto&quot;}

Platform의 XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md).

## 실시간 고객 프로필 {#profile}

Adobe Experience Platform을 사용하면 고객이 브랜드와 상호 작용하는 위치와 시기에 관계없이 고객을 위해 조정되고 일관되며 적절한 경험을 제공할 수 있습니다. 실시간 고객 프로필을 사용하면 온라인, 오프라인, CRM 및 타사 데이터를 포함하여 여러 채널의 데이터를 결합하는 각 개별 고객을 전체적으로 확인할 수 있습니다. 프로필을 사용하면 모든 고객 상호 작용을 실행 가능하고 타임스탬프가 지정된 계정을 제공하는 통합 보기에 고객 데이터를 통합할 수 있습니다.

**예정된 사용 중단** {#deprecation}

세그먼트 멤버십 라이프사이클에서 중복을 제거하려면 `Existing` 상태는 [세그먼트 멤버십 맵](../../xdm/field-groups/profile/segmentation.md) 2023년 3월 말 후속 발표에는 정확한 사용 중단 날짜가 포함됩니다.

사용 중단 후, 세그먼트에 자격을 갖춘 프로필은 로 표시됩니다 `Realized` 그리고 자격이 없는 프로필은 `Exited`. 이렇게 하면 다음과 같은 파일 기반 대상과 패리티가 생깁니다. `Active` 및 `Expired` 세그먼트 상태.

이 변경 사항은 [엔터프라이즈 대상](../../destinations/destination-types.md#streaming-profile-export) (Amazon Kinesis, Azure 이벤트 허브, HTTP API)를 통해 다음을 기반으로 자동화된 다운스트림 프로세스를 배치합니다 `Existing` 상태. 이러한 경우 다운스트림 통합을 검토하십시오. 특정 시간 이후에 새로 자격을 갖춘 프로필을 식별하는 데 관심이 있는 경우 `Realized` 상태 및 `lastQualificationTime` 세그먼트 멤버십 맵에서 공유할 수 있습니다. 자세한 내용은 Adobe 담당자에게 문의하십시오.

프로필 데이터 작업에 대한 자습서 및 모범 사례 등 실시간 고객 프로필에 대한 자세한 내용은 [실시간 고객 프로필 개요](../../profile/home.md).

## 세분화 서비스 {#segmentation}

[!DNL Segmentation Service] 고객 기반 내의 마케팅 가능한 사람 그룹을 구분하는 기준을 설명하여 특정 프로필 하위 집합을 정의합니다. 세그먼트는 브랜드와의 고객 상호 작용을 나타내는 레코드 데이터(예: 인구 통계 정보) 또는 시계열 이벤트를 기반으로 할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 플랫폼 생성 세그먼트 멤버십 만료 | 에 있는 모든 세그먼트 멤버십입니다 `Exited` 상태를 기준으로 30일 이상 `lastQualificationTime` 필드는 삭제될 수 있습니다. |
| 외부 대상 멤버십 만료 | 기본적으로 외부 대상 멤버십은 30일 동안 유지됩니다. 이를 더 오래 보관하려면 `validUntil` 대상 데이터를 수집하는 동안 필드를 생성합니다. |

{style=&quot;table-layout:auto&quot;}

자세한 내용은 [!DNL Segmentation Service]를 보려면 [세그먼테이션 개요](../../segmentation/home.md).

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

| 기능 | 설명 |
| --- | --- |
| 클라우드 스토리지 소스의 하위 폴더에 대한 사용자 액세스 허용 | 이제 새 계정을 만들 때 클라우드 저장소 소스의 특정 하위 폴더에 대한 액세스를 정의할 수 있습니다. 만든 후에는 허용되는 하위 폴더의 데이터만 액세스할 수 있습니다. 이 기능은 다음 클라우드 스토리지 소스에서 사용할 수 있습니다. [Azure Blob 저장소](../../sources/connectors/cloud-storage/blob.md), [Google 클라우드 스토리지](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md), 및 [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| 베타 가용성 [!DNL SugarCRM] | [!DNL SugarCRM] 이제 소스는 베타로 제공됩니다. 를 사용하십시오 [!DNL SugarCRM Accounts & Contacts] 그리고 [!DNL SugarCRM Events] 소스에서 데이터를 가져옵니다. [!DNL SugarCRM] Experience Platform 계정. 자세한 내용은 [[!DNL SugarCRM] 개요](../../sources/connectors/crm/sugarcrm.md). |