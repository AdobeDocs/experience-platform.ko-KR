---
title: Adobe Experience Platform 릴리스 정보 2023년 2월
description: Adobe Experience Platform의 2023년 2월 릴리스 정보입니다.
exl-id: 1c30a646-d9f8-4749-ac25-40bc48365a40
source-git-commit: 5bf54374773fd95ae1c40dd00b5dbe633031b70e
workflow-type: tm+mt
source-wordcount: '1255'
ht-degree: 97%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 일자: 2023년 2월 22일**

Adobe Experience Platform의 기존 기능 업데이트:

- [데이터 수집](#data-collection)
- [[!DNL Destinations]](#destinations)
- [경험 데이터 모델 (XDM)](#xdm)
- [쿼리 서비스](#query-service)
- [Real-Time Customer Data Platform B2B 에디션](#b2b)
- [소스](#sources)

## 데이터 수집 {#data-collection}

Adobe Experience Platform은 클라이언트측 고객 경험 데이터를 수집하여 Adobe 또는 비 Adobe 대상으로 보강, 변환 및 배포가 가능한 Adobe Experience Platform Edge Network로 보낼 수 있는 기술 제품군을 제공합니다.

### 보증 {#assurance}

Adobe Assurance를 사용하면 모바일 앱에서 데이터를 수집하거나 경험을 제공하는 방식을 검사하고, 증명하고, 시뮬레이션하고, 검증할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 공개 APIs | 이제 Adobe Assurance API를 사용할 수 있습니다. Assurance API는 Mobile SDK와 함께 Adobe Assurance 확장 기능을 갖춘 경우 사용자가 자신의 웹 및 모바일 앱을 테스트하고 디버깅할 수 있도록 지원하는 API 모음입니다. Assurance API에 대한 자세한 내용은 [Assurance API 개요](https://developer.adobe.com/adobe-assurance-public-apis/)를 참조하십시오. |

{style="table-layout:auto"}

Assurance에 대한 자세한 내용은 [Assurance 설명서](https://developer.adobe.com/client-sdks/documentation/platform-assurance/)를 참조하십시오.

## [!DNL Destinations] {#destinations}

[!DNL Destinations]는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있는 대상 플랫폼과 사전 설치된 통합입니다. 대상을 사용해 교차 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 기능 또는 업데이트된 기능** {#destinations-new-updated-features}

| 기능 | 설명 |
| ----------- | ----------- |
| [파일 기반의 (일괄 처리) 대상](/help/destinations/destination-types.md#file-based)과의 통합을 위한 [동의 정책 개선](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) | <p> 프로필이 더 이상 동의 정책에 적합하지 않은 경우 Experience Platform은 이제 해당 정책 종료를 파일 기반 대상에 미리 전달합니다. 이는 스트리밍 대상에 대해 동일한 기능을 지원하는 [2023년 2월 릴리스](/help/release-notes/2023/january-2023.md#destinations-new-updated-functionality)에 따른 것입니다. </p> <p> <b>참고</b>: 이 기능은 **[!UICONTROL Privacy and Security Shield]** 및 **[!UICONTROL Healthcare Shield]** 고객에게만 제공됩니다 </p> |

{style="table-layout:auto"}

**새로운 대상 또는 업데이트된 설명서** {#destinations-new-updated-documentation}

| 설명서 | 설명 |
| ----------- | ----------- |
| 대상 작동 방식 설명서 | <p>사용자의 일반적인 질문을 기반으로 대상 작동 방식에 대한 세 가지 새로운 설명 기사를 게시했습니다.</p> <p><ul><li>[대상의 구성 가능한 공통 내보내기 설정](/help/destinations/how-destinations-work/destinations-configurations.md)</li><li>[서로 다른 대상 유형에 대한 프로필 내보내기 동작](/help/destinations/how-destinations-work/profile-export-behavior.md)</li><li>[대상 활성화 워크플로의 ID 처리](/help/destinations/how-destinations-work/identity-handling.md)</li></p> |

대상에 대한 일반적인 정보는 [대상 개요](../../destinations/home.md)를 참조하십시오.

## 경험 데이터 모델 (XDM) {#xdm}

XDM은 Adobe Experience Platform으로 가져오는 데이터에 대한 공통 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수하여 모든 고객 경험 데이터를 공통된 표현에 통합해 보다 빠르고 통합된 방식으로 인사이트를 제공할 수 있습니다. 고객 조치에서 귀중한 인사이트를 얻고, 세그먼트를 통해 고객 대상자를 정의하고, 개인 설정 목적으로 고객 속성을 사용할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| UI를 통한 필드 사용 중단 | 이제 [데이터가 수집된 후 스키마에서 필드 사용이 중단](../../xdm/tutorials/field-deprecation-ui.md)될 수 있습니다. XDM 필드 사용 중단을 통해 UI 보기에서 필드를 제거하고 사용을 위해 유지할 수 있습니다. 필요한 경우 더 이상 사용되지 않는 필드를 다시 표시할 수 있으며, 해당 필드를 참조하는 모든 세그먼트, 쿼리 또는 다운스트림 솔루션은 평소대로 실행됩니다. |

{style="table-layout:auto"}

**새로운 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 클래스 | [[!UICONTROL XDM 개별 잠재 고객 프로필]](https://github.com/adobe/xdm/pull/1669/files) | XDM 개별 잠재 고객 프로필 클래스는 파트너가 제공한 ID를 가져옵니다. |

{style="table-layout:auto"}

**업데이트된 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 필드 그룹 | [!UICONTROL 빈도 설정 제한] | [반복 및 사용자 정의 이벤트를 지원](https://github.com/adobe/xdm/pull/1641/files)하도록 [!UICONTROL 빈도 설정 제한] 필드 그룹이 업데이트되었습니다 |
| 데이터 유형 | [!UICONTROL 웹 레퍼러] | `xdm:linkName` 및 `xdm:linkRegion`](https://github.com/adobe/xdm/pull/1666/files)을 포함하도록 웹 레퍼러 속성이 [업데이트되었습니다. 각각 이전 페이지에서 선택한 HTML 요소의 이름 및 영역입니다. |
| 필드 그룹 | [!UICONTROL Adobe CJM ExperienceEvent - 메시지 상호 작용 세부 사항] | [[!UICONTROL 추적기 URL] 필드가 [!UICONTROL Adobe CJM ExperienceEvent]에 ](https://github.com/adobe/xdm/pull/1665/files)추가되었습니다. 이 추적기는 사용자가 선택한 URL을 제공합니다. |
| 필드 그룹 | [!UICONTROL Adobe CJM ExperienceEvent - 메시지 상호 작용 세부 사항] | [](https://github.com/adobe/xdm/pull/1668/files)URL [!UICONTROL 추적 유형] 필드에서 비어 있는 `meta:enum` 속성이 제거되었습니다. |
| 데이터 유형 | [!UICONTROL 미디어 정보] | [[!UICONTROL 미디어 정보] 데이터 유형의 `videoSegment` 속성에서 정규 표현식 패턴이 제거](https://github.com/adobe/xdm/pull/1667/files)되었습니다 |

{style="table-layout:auto"}

Platform의 XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md)를 살펴보십시오.&#x200B;

## 쿼리 서비스 {#query-service}

쿼리 서비스를 사용하면 표준 SQL로 Adobe Experience Platform [!DNL Data Lake]에서 데이터를 쿼리할 수 있습니다. 데이터 레이크의 데이터 세트에 참여하고 쿼리 결과를 보고 또는 Data Science Workspace에 사용하거나 실시간 고객 프로필에 수집하기 위한 새 데이터 세트로 캡처할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| SQL로 프로필용 데이터 세트 활성화 | [CTAS 쿼리에서 레이블을 사용하여 데이터 세트를 &#39;프로필 활성화됨&#39;으로 만들거나](../../query-service/sql/syntax.md#create-table-as-select) ALTER를 사용하여 프로필에 대해 활성화할 기존 데이터 세트를 업데이트합니다. 이 확장된 SQL 구성을 사용하여 실시간 고객 프로필 비즈니스 사용 사례에 대해 파생된 데이터 세트를 매끄럽게 지원할 수 있습니다. 자세한 내용은 [파생 데이터 세트에 대한 원활한 SQL 흐름](../../query-service/data-distiller/derived-datasets/create-derived-datasets-with-sql.md)을 참조하십시오. |
| 예약된 쿼리 모니터링 | [예약된 쿼리 탭](../../query-service/ui/monitor-queries.md)을 사용하여 쿼리 실행에 대한 중요 정보를 찾고 경고를 구독합니다. 일정 세부 정보, 상태 및 실패 시 오류 메시지/코드에 대한 쿼리를 모니터링합니다. |
| 자동 완성 기능 전환 | [쿼리 편집기 자동 완성 기능을 전환](../../query-service/ui/user-guide.md#auto-complete)하여 특정 메타데이터 명령을 제거하고 처리 시간을 단축합니다. 이 기능은 쿼리를 작성할 때 잠재적인 SQL 키워드 및 테이블 세부 정보를 자동으로 제안합니다. |
| 데이터 세트 샘플 | 쿼리에서 샘플링 속도를 지정하고 [데이터 세트 샘플을 사용하여 균일한 무작위 샘플을 만들거나](../../query-service/key-concepts/dataset-samples.md) 특정 기준에 따라 조건부 샘플을 만듭니다. |

{style="table-layout:auto"}

쿼리 서비스에 대한 자세한 내용은 [쿼리 서비스 개요](../../query-service/home.md)를 참조하십시오.


## Real-Time Customer Data Platform B2B 에디션 {#b2b}

Real-Time Customer Data Platform(Real-Time CDP)을 기반으로 구축된 Real-Time CDP B2B 에디션은 business-to-business 서비스 모델에서 운영하는 마케터를 위해 특별히 설계되었습니다. 여러 소스의 데이터를 함께 가져와서 사람 및 계정 프로필의 단일 보기로 결합합니다. 마케터는 이 통합 데이터를 통해 특정 대상자를 정확하게 타겟팅하고 사용 가능한 모든 채널에서 해당 대상자를 참여시킬 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 관련 계정 서비스 활성화 | 새 전환 기능을 사용하면 계정에서 관련 계정 서비스를 활성화할 수 있습니다. 자세한 내용은 [관련 계정 서비스 활성화](../../rtcdp/b2b-ai-ml-services/related-accounts.md#enable)에 관한 안내서를 참조하십시오. |

{style="table-layout:auto"}

Real-Time CDP B2B 에디션에 대한 자세한 내용은 [Real-Time CDP B2B 에디션 개요](../../rtcdp/overview.md)를 참조하십시오.

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 해당 데이터를 구조화하고, 라벨링하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 서드파티 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [!DNL Google PubSub]를 사용하여 구독 수준의 액세스 지정 | 이제 인증할 때 구독 ID를 제공하여 [!DNL Google PubSub] 소스를 사용할 경우 특정 주제 구독에 대한 액세스 권한을 정의할 수 있습니다. 자세한 내용은 [Flow Service API](../../sources/tutorials/api/create/cloud-storage/google-pubsub.md) 또는 [Platform UI](../../sources/tutorials/ui/create/cloud-storage/google-pubsub.md)를 사용한 [!DNL Google PubSub]인증 튜토리얼을 참조하십시오. |
| [!DNL Marketo]에서 사용자 정의된 활동 데이터 수집 | 이제 [!DNL Marketo] 인스턴스의 사용자 정의 활동 데이터를 Experience Platform으로 가져올 수 있습니다. 사용자 정의된 활동 데이터를 수집하려면 B2B 활동 스키마에서 사용자 정의된 활동 필드 그룹을 설정하고 활동 데이터 세트를 사용하여 데이터 흐름을 생성해야 합니다. 데이터 흐름이 완료되면 수집된 데이터 집합에는 [!DNL Marketo] 인스턴스의 표준 활동 및 사용자 정의 활동이 모두 포함됩니다. 그런 다음 [쿼리 서비스](../../query-service/home.md)를 사용하여 Platform의 사용자 정의 활동 레코드에 액세스할 수 있습니다. 자세한 내용은 [사용자 정의 활동 데이터의 데이터 흐름 생성](../../sources/tutorials/ui/create/adobe-applications/marketo-custom-activities.md)에 대한 안내서를 참조하십시오. |
| [!DNL Marketo]에서 요청되지 않은 계정 제외 | 이제 회사 데이터에 대한 데이터 흐름을 만들 때 요청되지 않은 계정을 수집에서 제외할지 또는 포함할지 여부를 구성할 수 있습니다. 자세한 내용은 [ [!DNL Marketo]](../../sources/tutorials/ui/create/adobe-applications/marketo.md)에 대한 소스 연결 및 데이터 흐름 생성에 관한 안내서를 참조하십시오. |

{style="table-layout:auto"}

소스에 대해 자세히 알아보려면 [소스 개요 ](../../sources/home.md)를 참조하십시오.
