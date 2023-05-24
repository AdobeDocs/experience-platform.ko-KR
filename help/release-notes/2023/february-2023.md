---
title: Adobe Experience Platform 릴리스 노트 2023년 2월
description: Adobe Experience Platform의 2023년 2월 릴리스 정보.
exl-id: 1c30a646-d9f8-4749-ac25-40bc48365a40
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1293'
ht-degree: 4%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 일자: 2023년 2월 22일**

Adobe Experience Platform의 기존 기능 업데이트:

- [데이터 수집](#data-collection)
- [[!DNL Destinations]](#destinations)
- [경험 데이터 모델(XDM)](#xdm)
- [쿼리 서비스](#query-service)
- [Real-Time Customer Data Platform B2B 에디션](#b2b)
- [소스](#sources)

## 데이터 수집 {#data-collection}

Adobe Experience Platform은 클라이언트측 고객 경험 데이터를 수집하여 Adobe Experience Platform Edge Network로 전송하여 Adobe 또는 비 Adobe 대상으로 보강, 변환 및 배포할 수 있는 기술 제품군을 제공합니다.

### 보증 {#assurance}

Adobe 보증을 통해 모바일 앱에서 데이터를 수집하거나 경험을 제공하는 방법을 검사, 증명, 시뮬레이션 및 확인할 수 있습니다.

**새 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 공개 API | 이제 Adobe 보증 API를 사용할 수 있습니다. Assurance API는 Mobile SDK로 Adobe 보증 확장을 설치하면 사용자가 자신의 웹 및 모바일 앱을 테스트하고 디버깅할 수 있는 API 컬렉션입니다. Assurance API에 대한 자세한 내용은 [Assurance API 개요](https://developer.adobe.com/adobe-assurance-public-apis/). |

{style="table-layout:auto"}

Assurance에 대한 자세한 내용은 [보증 설명서](https://developer.adobe.com/client-sdks/documentation/platform-assurance/).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 빌드된 통합입니다. 대상을 사용하여 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 다양한 사용 사례에 대해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새 기능 또는 업데이트된 기능** {#destinations-new-updated-features}

| 기능 | 설명 |
| ----------- | ----------- |
| [동의 정책 개선](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) 와 통합하기 위한 [파일 기반(일괄 처리) 대상](/help/destinations/destination-types.md#file-based) | <p> 프로필이 더 이상 동의 정책에 적합하지 않을 때 이제 Experience Platform은 정책 종료를 파일 기반 대상으로 미리 전달합니다. 다음 단계를 따릅니다. [2023년 2월 릴리스](/help/release-notes/2023/january-2023.md#destinations-new-updated-functionality) 스트리밍 대상에 대해 동일한 기능. </p> <p> <b>참고</b>: 이 기능은 다음 고객에게만 제공됩니다. **[!UICONTROL 개인 정보 보호 및 보안 보호]**&#x200B;및 **[!UICONTROL 헬스케어 실드]**. </p> |

{style="table-layout:auto"}

**신규 또는 업데이트된 설명서** {#destinations-new-updated-documentation}

| 설명서 | 설명 |
| ----------- | ----------- |
| 대상 작동 방식 설명서 | <p>사용자의 일반적인 질문을 기반으로 대상의 작동 방식에 대한 세 가지 새로운 설명자 문서를 게시했습니다.</p> <p><ul><li>[대상에서 구성 및 공통 내보내기 설정](/help/destinations/how-destinations-work/destinations-configurations.md)</li><li>[다양한 대상 유형에 대한 프로필 내보내기 동작](/help/destinations/how-destinations-work/profile-export-behavior.md)</li><li>[대상 활성화 워크플로에서의 ID 처리](/help/destinations/how-destinations-work/identity-handling.md)</li></p> |

대상에 대한 일반적인 정보는 [대상 개요](../../destinations/home.md).

## 경험 데이터 모델(XDM) {#xdm}

XDM은 Adobe Experience Platform으로 가져온 데이터에 대한 일반적인 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수함으로써 모든 고객 경험 데이터를 일반적인 표현에 통합하여 보다 빠르고 통합적인 방식으로 통찰력을 제공할 수 있습니다. 고객 작업에서 중요한 통찰력을 얻고, 세그먼트를 통해 고객 대상을 정의하고, 개인화 목적으로 고객 속성을 사용할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| UI를 통한 필드 사용 중단 | 이제 다음을 수행할 수 있습니다. [데이터를 수집한 후 스키마에서 필드 사용 중단](../../xdm/tutorials/field-deprecation-ui.md). XDM 필드 사용 중단을 사용하면 필드를 그대로 유지하면서 UI 보기에서 제거할 수 있습니다. 필요한 경우 더 이상 사용되지 않는 필드를 다시 표시할 수 있으며 해당 필드를 참조하는 모든 세그먼트, 쿼리 또는 다운스트림 솔루션은 평소와 같이 실행됩니다. |

{style="table-layout:auto"}

**새로운 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 클래스 | [[!UICONTROL XDM 개별 잠재 고객 프로필]](https://github.com/adobe/xdm/pull/1669/files) | XDM 개별 잠재 고객 프로필 클래스는 파트너가 제공한 ID를 가져옵니다. |

{style="table-layout:auto"}

**업데이트된 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 필드 그룹 | [!UICONTROL 빈도 제한 조건] | 다음 [!UICONTROL 빈도 제한 조건] 필드 그룹이 [반복 및 사용자 지정 이벤트를 지원하도록 업데이트됨](https://github.com/adobe/xdm/pull/1641/files). |
| 데이터 유형 | [!UICONTROL 웹 레퍼러] | 웹 레퍼러 속성이 [을(를) 포함하도록 업데이트됨 `xdm:linkName` 및 `xdm:linkRegion`](https://github.com/adobe/xdm/pull/1666/files). 각각 이전 페이지에서 선택한 HTML 요소의 이름과 영역입니다. |
| 필드 그룹 | [!UICONTROL Adobe CJM ExperienceEvent - 메시지 상호 작용 세부 정보] | [다음 [!UICONTROL 추적기 URL] 필드가 추가됨](https://github.com/adobe/xdm/pull/1665/files) (으)로 [!UICONTROL CJM ExperienceEvent Adobe]. 이 추적기는 사용자가 선택한 URL을 제공합니다. |
| 필드 그룹 | [!UICONTROL Adobe CJM ExperienceEvent - 메시지 상호 작용 세부 정보] | [비어 있음 `meta:enum` 속성이 제거됨](https://github.com/adobe/xdm/pull/1668/files) URL에서 [!UICONTROL 추적 유형] 필드. |
| 데이터 유형 | [!UICONTROL 미디어 정보] | [의 정규 표현식 패턴 `videoSegment` 의 속성 [!UICONTROL 미디어 정보] 데이터 형식이 제거되었습니다.](https://github.com/adobe/xdm/pull/1667/files). |

{style="table-layout:auto"}

플랫폼의 XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md). &#x200B;

## 쿼리 서비스 {#query-service}

쿼리 서비스를 사용하면 표준 SQL을 사용하여 Adobe Experience Platform에서 데이터를 쿼리할 수 있습니다 [!DNL Data Lake]. 데이터 레이크에서 모든 데이터 세트에 참여하고 쿼리 결과를 보고 또는 Data Science Workspace에 사용하거나 실시간 고객 프로필에 수집하기 위한 새 데이터 세트로 캡처할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| SQL을 사용하여 프로필에 데이터 세트 활성화 | [CTAS 쿼리의 LABEL을 사용하여 데이터 세트를 &#39;프로필 활성화&#39;로 만들기](../../query-service/sql/syntax.md#create-table-as-select)또는 ALTER를 사용하여 프로필에 사용할 수 있는 기존 데이터 세트를 업데이트합니다. 이 확장된 SQL 구문을 사용하여 실시간 고객 프로필 비즈니스 사용 사례에 대해 파생된 속성을 원활하게 지원할 수 있습니다. 다음을 참조하십시오. [파생 특성 문서에 대한 원활한 SQL 흐름](../../query-service/data-distiller/derived-attributes/seamless-sql-flow.md) 을 참조하십시오. |
| 예약된 쿼리 모니터링 | 사용 [예약된 쿼리 탭](../../query-service/ui/monitor-queries.md) 를 사용하여 쿼리 실행에 대한 중요한 정보를 찾고 경고를 구독할 수 있습니다. 일정 세부 정보, 상태 및 오류 메시지/코드가 실패할 경우 쿼리를 모니터링합니다. |
| 자동 완성 기능 전환 | 다음을 통해 특정 메타데이터 명령을 제거하고 처리 시간 개선 [쿼리 편집기 자동 완성 기능 전환](../../query-service/ui/user-guide.md#auto-complete). 이 기능은 쿼리를 작성할 때 쿼리에 대한 잠재적인 SQL 키워드와 테이블 세부 정보를 자동으로 제안합니다. |
| 데이터 세트 샘플 | 쿼리에서 샘플링 속도를 지정하고 [데이터 세트 샘플을 사용하여 균일한 무작위 샘플 만들기](../../query-service/essential-concepts/dataset-samples.md)또는 특정 기준을 기반으로 조건부 샘플을 만들 수 있습니다. |

{style="table-layout:auto"}

쿼리 서비스에 대한 자세한 내용은 [쿼리 서비스 개요](../../query-service/home.md).


## Real-Time Customer Data Platform B2B 에디션 {#b2b}

Real-time Customer Data Platform(Real-Time CDP)을 기반으로 구축된 Real-Time CDP B2B 에디션은 B2B 서비스 모델을 운영하는 마케터용으로 특별히 빌드되었습니다. 여러 소스에서 데이터를 취합하여 사람 및 계정 프로필에 대한 단일 보기에 결합합니다. 이 통합 데이터를 통해 마케터는 특정 대상을 정확하게 타겟팅하고 사용 가능한 모든 채널에서 해당 대상을 참여시킬 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 관련 계정 서비스 활성화 | 새로운 토글 기능을 사용하면 계정에서 관련 계정 서비스를 활성화할 수 있습니다. 자세한 내용은 의 안내서를 참조하십시오. [관련 계정 서비스 활성화](../../rtcdp/b2b-ai-ml-services/related-accounts.md#enable). |

{style="table-layout:auto"}

Real-Time CDP B2B 에디션에 대해 자세히 알아보려면 [Real-Time CDP B2B 에디션 개요](../../rtcdp/overview.md).

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 해당 데이터를 구조화하고, 레이블을 지정하고, 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 서드파티 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 을 사용하여 구독 수준 액세스 지정 [!DNL Google PubSub] | 이제 를 사용할 때 특정 주제 구독에 대한 액세스 권한을 정의할 수 있습니다. [!DNL Google PubSub] 인증 시 구독 ID를 제공하여 소스. 자세한 내용은 [!DNL Google PubSub] 인증 자습서 [흐름 서비스 API 사용](../../sources/tutorials/api/create/cloud-storage/google-pubsub.md) 또는 [플랫폼 UI](../../sources/tutorials/ui/create/cloud-storage/google-pubsub.md). |
| 에서 사용자 지정 활동 데이터 수집 [!DNL Marketo] | 이제 다음에서 사용자 지정 활동 데이터를 가져올 수 있습니다. [!DNL Marketo] Experience Platform 인스턴스. 사용자 지정 활동 데이터를 수집하려면 B2B 활동 스키마에서 사용자 지정 활동 필드 그룹을 설정하고 활동 데이터 세트를 사용하여 데이터 흐름을 만들어야 합니다. 데이터 흐름이 완료되면 수집된 데이터 세트에는 의 표준 활동과 사용자 지정 활동이 모두 포함됩니다. [!DNL Marketo] 인스턴스. 그런 다음 을 사용할 수 있습니다. [쿼리 서비스](../../query-service/home.md) 를 사용하여 Platform에서 사용자 지정 활동 레코드에 액세스할 수 있습니다. 자세한 내용은 의 안내서를 참조하십시오. [사용자 지정 활동 데이터에 대한 데이터 흐름 만들기](../../sources/tutorials/ui/create/adobe-applications/marketo-custom-activities.md). |
| 다음에서 미청구 계정 제외 [!DNL Marketo] | 이제 회사 데이터에 대한 데이터 흐름을 만들 때 수집에서 미청구 계정을 제외할지 또는 포함할지 여부를 구성할 수 있습니다. 자세한 내용은 의 안내서를 참조하십시오. [소스 연결 및 데이터 흐름 만들기 [!DNL Marketo]](../../sources/tutorials/ui/create/adobe-applications/marketo.md). |

{style="table-layout:auto"}

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).
