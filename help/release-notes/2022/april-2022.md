---
title: Adobe Experience Platform 릴리스 노트 - 2022년 4월
description: Adobe Experience Platform에 대한 2022년 4월 릴리스 노트입니다.
source-git-commit: 4bbf7642a456f36ea0fe7fc1c8d68ad37351ff4c
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 4%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 일자: 2022년 4월 27일**

Adobe Experience Platform의 기존 기능 업데이트:

- [XDM(경험 데이터 모델)](#xdm)

## XDM(경험 데이터 모델) {#xdm}

XDM은 Adobe Experience Platform으로 가져온 데이터에 대한 일반적인 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수함으로써 모든 고객 경험 데이터를 공통 표현으로 통합하여 보다 빠르고 통합된 방식으로 통찰력을 제공할 수 있습니다. 고객 작업을 통해 유용한 통찰력을 얻을 수 있고, 세그먼트를 통해 고객 대상을 정의하고, 개인화를 위해 고객 속성을 사용할 수 있습니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| 스키마에 대한 개별 표준 필드 추가 또는 제거 | 이제 스키마 편집기 UI를 사용하여 스키마에 표준 필드 그룹 부분을 추가할 수 있으므로, 사용자 지정 리소스를 처음부터 빌드하지 않아도 포함하도록 선택한 필드에 더 유연하게 대처할 수 있습니다.<br><br>이제 스키마 구조 내에서 직접 임시 사용자 지정 필드를 정의하고 필드 그룹을 미리 만들거나 편집할 필요 없이 새 사용자 지정 필드 그룹에 할당할 수도 있습니다.<br><br>다음 안내서를 참조하십시오. [UI에서 스키마 만들기 및 편집](../../xdm/ui/resources/schemas.md) 를 참조하십시오. |

{style=&quot;table-layout:auto&quot;}

**새로운 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 전역 스키마 | [[!UICONTROL 데이터 위생 작업 요청]](https://github.com/adobe/xdm/blob/master/schemas/hygiene/aep-hygiene-ops-record.schema.json) | 지정된 데이터 세트 또는 샌드박스에서 레코드를 삭제하거나 수정하기 위한 데이터 정리 요청의 세부 정보를 캡처합니다. |
| 설명자 | [[!UICONTROL 시계열 세부기간 설명자]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/time-series/descriptorTimeSeriesGranularity.schema.json) | 시계열 및 요약 데이터의 세부기간을 나타냅니다. 스키마에 적용할 경우 스키마는 `timestamp` 필드는 이 세부 기간 동안의 첫 번째 타임스탬프입니다. |
| 클래스 | [[!UICONTROL XDM 요약 지표]](https://github.com/adobe/xdm/blob/master/components/classes/summary_metrics.schema.json) | SQL SELECT를 GROUP BY로 사용한 결과와 같은 그룹 차원과 함께 사전 요약된 지표를 제공합니다. |
| 필드 그룹 | [[!UICONTROL 동의 정책 평가 결과 맵]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | 개인에게 대한 동의 정책 평가 결과를 캡처합니다. |
| 필드 그룹 | [[!UICONTROL 사이트 검색]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | 검색 쿼리, 필터링 및 순서 지정과 같은 사이트 검색 관련 정보를 캡처합니다. |
| 필드 그룹 | [[!UICONTROL 리드 병합]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/merge-leads.schema.json) | 두 개 이상의 리드가 병합되는 이벤트의 세부 정보를 캡처합니다. |
| 필드 그룹 | [[!UICONTROL 이메일 전송됨]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/emailsent.schema.json) | 수신자에게 이메일이 전송되는 이벤트의 세부 정보를 캡처합니다. |
| 필드 그룹 | [[!UICONTROL 결합 필드]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-stitching.schema.json) | 이벤트에 대한 ID 결합 프로세스를 통해 계산된 값을 캡처합니다. |
| 필드 그룹 | [[!UICONTROL 감사를 위한 보조 수신자 세부 정보]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/secondary-recipient-detail.schema.json) | 감사에 대한 보조 수신자 세부 정보를 캡처하는 Adobe Journey Optimizer 필드 그룹입니다. |
| 필드 그룹 | [[!UICONTROL XDM 비즈니스 계정 개인 관계 세부 정보]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | 계정-개인 관계와 관련된 세부 정보를 캡처합니다. |
| 필드 그룹 | [[!UICONTROL 계정 개인 세부 정보]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | 계정-개인 관계와 관련된 세부 정보를 캡처합니다. |
| 데이터 유형 | [[!UICONTROL 장바구니]](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json) | 전자 상거래 장바구니에 대한 정보를 캡처합니다. |
| 데이터 유형 | [[!UICONTROL 배송]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | 하나 이상의 제품에 대한 배송 정보를 캡처합니다. |
| 데이터 유형 | [[!UICONTROL 사이트 검색]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | 사이트 검색 활동에 대한 정보를 캡처합니다. |
| 확장(Workfront) | [[!UICONTROL 작업 작업 속성]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/opTask.schema.json) | 작업 작업과 관련된 세부 정보를 캡처합니다. |
| 확장(Workfront) | [[!UICONTROL 작업 Portfolio 속성]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/portfolio.schema.json) | 작업 포트폴리오와 관련된 세부 정보를 캡처합니다. |
| 확장(Workfront) | [[!UICONTROL 작업 프로그램 속성]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/program.schema.json) | 작업 프로그램과 관련된 세부 정보를 캡처합니다. |
| 확장(Workfront) | [[!UICONTROL 작업 프로젝트 속성]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/project.schema.json) | 작업 프로젝트와 관련된 세부 정보를 캡처합니다. |

{style=&quot;table-layout:auto&quot;}

**업데이트된 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 업데이트 |
| --- | --- | --- |
| 전역 스키마 | [[!UICONTROL 대상]](https://github.com/adobe/xdm/blob/master/schemas/destinations/destination.schema.json) | 에 대한 새 열거형 값 `destinationCategory`. |
| 설명자 | [[!UICONTROL 이름 설명자]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/display/alternateDisplayInfo.schema.json) | 추천 값(`meta:enum`) 포함되어 있어야 합니다. |
| 필드 그룹 | [[!UICONTROL 사용자 로그인 프로세스]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-user-login-details.schema.json) | `createProfile` 필드가 추가되었습니다. |
| 데이터 유형 | [[!UICONTROL 상거래]](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json) | 장바구니 관련 필드가 몇 개 추가되었습니다. |
| 데이터 유형 | [[!UICONTROL 제품 목록 항목]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | 선택한 옵션 및 할인 금액에 대해 새 필드가 추가되었습니다. |
| 확장(Intelligent Services) | [[!UICONTROL Intelligent Services JourneyAI 전송 시간 최적화]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/intelligentServices/profile-journeyai-sendtimeoptimization.schema.json) | 전송 시간 점수를 위한 스토리지 형식을 최적화합니다. |
| 확장(Workfront) | [[!UICONTROL Workfront 변경 이벤트]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/changeevent.schema.json) | 여러 필드가 `workfront:customData` 사용자 지정 양식 필드에 대한 필드입니다. |
| 확장(Workfront) | [[!UICONTROL 작업 작업 특성]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/task.schema.json) | 여러 필드가 추가되었습니다. |
| 확장(Workfront) | [[!UICONTROL 작업 개체]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobject.schema.json) | 상위 개체 유형 및 사용자 지정 양식 필드에 대한 새 필드입니다. |

{style=&quot;table-layout:auto&quot;}

Platform의 XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md).
