---
title: Adobe Experience Platform 릴리스 노트 - 2023년 1월
description: Adobe Experience Platform에 대한 2023년 1월 릴리스 노트입니다.
source-git-commit: 3fd3e96d5db6b1e63df338efe383d209690eb1f6
workflow-type: tm+mt
source-wordcount: '936'
ht-degree: 6%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2023년 1월 25일**

Adobe Experience Platform의 기존 기능 업데이트:

- [데이터 수집](#data-collection)
- [XDM(경험 데이터 모델)](#xdm)
- [소스](#sources)

## 데이터 수집 {#data-collection}

Adobe Experience Platform은 클라이언트측 고객 경험 데이터를 수집하고 Adobe Experience Platform Edge Network로 전송하여 Adobe 또는 비Adobe 대상으로 보강, 변환 및 배포할 수 있는 기술 세트를 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 신규 홈 화면 | 데이터 수집 UI의 홈 페이지가 생산성을 간소화하기 위해 유용한 온보딩 정보 및 링크를 포함하도록 업데이트되었습니다. 여기에는 다음 항목이 포함되어 있습니다.<ol><li>시작하는 설명서 및 권장 워크플로우</li><li>최근 속성, 규칙 및 데이터 요소</li><li>인기 있는 확장</li><li>빠른 설치 기능으로 새로운 확장 업데이트</li></ol> |
| 에 데이터 보내기 [!DNL Google Ads] 이벤트 전달 사용 | 이제 를 사용할 수 있습니다 [[!DNL Google Ads Enhanced Conversions] API 확장](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) 이벤트 전달에 대해 다음을 결합합니다. [Google Oauth 2 비밀](../../tags/ui/event-forwarding/secrets.md#google-oauth2)으로 데이터를 안전하게 [!DNL Google Ads] 실시간으로 |

{style=&quot;table-layout:auto&quot;}

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

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

| 기능 | 설명 |
| --- | --- |
| 클라우드 스토리지 소스의 하위 폴더에 대한 사용자 액세스 허용 | 이제 새 계정을 만들 때 클라우드 저장소 소스의 특정 하위 폴더에 대한 액세스를 정의할 수 있습니다. 만든 후에는 허용되는 하위 폴더의 데이터만 액세스할 수 있습니다. 이 기능은 다음 클라우드 스토리지 소스에서 사용할 수 있습니다. [Azure Blob 저장소](../../sources/connectors/cloud-storage/blob.md), [Google 클라우드 스토리지](../../sources/connectors/cloud-storage/google-cloud-storage.md), [Google PubSub](../../sources/connectors/cloud-storage/google-pubsub.md), 및 [SFTP](../../sources/connectors/cloud-storage/sftp.md). |
| 베타 가용성 [!DNL SugarCRM] | [!DNL SugarCRM] 이제 소스는 베타로 제공됩니다. 를 사용하십시오 [!DNL SugarCRM Accounts & Contacts] 그리고 [!DNL SugarCRM Events] 소스에서 데이터를 가져옵니다. [!DNL SugarCRM] Experience Platform 계정. 자세한 내용은 [[!DNL SugarCRM] 개요](../../sources/connectors/crm/sugarcrm.md). |
