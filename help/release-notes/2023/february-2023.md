---
title: Adobe Experience Platform 릴리스 노트 - 2023년 2월
description: Adobe Experience Platform에 대한 2023년 2월 릴리스 노트입니다.
source-git-commit: 66ca8d3972045cffe4a1614f638546f4e7838680
workflow-type: tm+mt
source-wordcount: '1138'
ht-degree: 6%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2023년 2월 22일**

Adobe Experience Platform의 기존 기능 업데이트:

- [[!DNL Destinations]](#destinations)
- [XDM(경험 데이터 모델)](#xdm)
- [쿼리 서비스](#query-service)
- [Real-Time Customer Data Platform B2B 에디션](#b2b)
- [소스](#sources)

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 구축된 통합입니다. 대상을 사용하여 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례에 대해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 기능 또는 업데이트된 기능** {#destinations-new-updated-features}

| 기능 | 설명 |
| ----------- | ----------- |
| [동의 정책 개선 사항](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-enhancement) 통합 [파일 기반(배치) 대상](/help/destinations/destination-types.md#file-based) | <p> 이제 프로필이 더 이상 동의 정책에 대한 자격이 없는 경우 Experience Platform은 정책 종료를 파일 기반 대상으로 미리 통신합니다. 다음은 다음과 같습니다 [2023년 2월 릴리스](/help/release-notes/2023/january-2023.md#destinations-new-updated-functionality) 스트리밍 대상에 대해 동일한 기능을 사용할 수 있습니다. </p> <p> <b>참고</b>: 이 기능은 **[!UICONTROL 개인 정보 및 보안 차단]**, 및 **[!UICONTROL 의료 보호]**. </p> |

{style=&quot;table-layout:auto&quot;}

**새 설명서 또는 업데이트된 설명서** {#destinations-new-updated-documentation}

| 설명서 | 설명 |
| ----------- | ----------- |
| 대상 작동 방식 설명서 | <p>사용자의 일반적인 질문에 따라 대상이 작동하는 방식에 대한 세 가지 새로운 설명 문서를 게시했습니다.</p> <p><ul><li>[대상의 구성 및 공통 내보내기 설정](/help/destinations/how-destinations-work/destinations-configurations.md)</li><li>[다양한 대상 유형에 대한 프로필 내보내기 동작](/help/destinations/how-destinations-work/profile-export-behavior.md)</li><li>[대상 활성화 워크플로우의 ID 처리](/help/destinations/how-destinations-work/identity-handling.md)</li></p> |

대상에 대한 자세한 내용은 [대상 개요](../../destinations/home.md).

## XDM(경험 데이터 모델) {#xdm}

XDM은 Adobe Experience Platform으로 가져온 데이터에 대한 일반적인 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수함으로써 모든 고객 경험 데이터를 공통 표현으로 통합하여 보다 빠르고 통합된 방식으로 통찰력을 제공할 수 있습니다. 고객 작업을 통해 유용한 통찰력을 얻을 수 있고, 세그먼트를 통해 고객 대상을 정의하고, 개인화를 위해 고객 속성을 사용할 수 있습니다.

**업데이트된 기능**
&#x200B; | 기능 | 설명 | | — | — | | UI를 통한 필드 사용 중단 | 이제 다음을 수행할 수 있습니다. [데이터가 수집되면 스키마에서 필드를 사용하지 않습니다.](../../xdm/tutorials/field-deprecation-ui.md). XDM 필드 사용 중단 기능을 사용하면 UI 보기에서 필드를 제거할 수 있지만 필드를 사용할 수 있도록 유지할 수 있습니다. 필요한 경우 더 이상 사용되지 않는 필드를 다시 표시할 수 있으며 필드를 참조하는 모든 세그먼트, 쿼리 또는 다운스트림 솔루션은 평소대로 실행됩니다. |

{style=&quot;table-layout:auto&quot;}

**새로운 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 클래스 | [[!UICONTROL XDM 개별 잠재 고객 프로필]](https://github.com/adobe/xdm/pull/1669/files) | XDM 개별 잠재 고객 프로필 클래스는 파트너가 제공하는 ID를 가져옵니다. |

{style=&quot;table-layout:auto&quot;}

**업데이트된 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 필드 그룹 | [!UICONTROL 빈도 제한] | 다음 [!UICONTROL 빈도 제한] 필드 그룹이 생성되었습니다. [반복 및 사용자 지정 이벤트를 지원하도록 업데이트됨](https://github.com/adobe/xdm/pull/1641/files). |
| 데이터 유형 | [!UICONTROL 웹 레퍼러] | 웹 레퍼러 속성이 [을 포함하도록 업데이트됨 `xdm:linkName` 및 `xdm:linkRegion`](https://github.com/adobe/xdm/pull/1666/files). 각각 이전 페이지에서 선택한 HTML 요소의 이름과 영역입니다. |
| 필드 그룹 | [!UICONTROL Adobe CJM ExperienceEvent - 메시지 상호 작용 세부 사항] | [다음 [!UICONTROL 추적기 URL] 필드가 추가되었습니다](https://github.com/adobe/xdm/pull/1665/files) 변환 후 [!UICONTROL Adobe CJM ExperienceEvent]. 이 추적기는 사용자가 선택한 URL을 제공합니다. |
| 필드 그룹 | [!UICONTROL Adobe CJM ExperienceEvent - 메시지 상호 작용 세부 사항] | [빈 `meta:enum` 속성이 제거되었습니다.](https://github.com/adobe/xdm/pull/1668/files) URL에서 [!UICONTROL 추적 유형] 필드. |
| 데이터 유형 | [!UICONTROL 미디어 정보] | [다음에서 가져온 정규식 패턴 `videoSegment` 속성 [!UICONTROL 미디어 정보] 데이터 형식이 제거되었습니다.](https://github.com/adobe/xdm/pull/1667/files). |

{style=&quot;table-layout:auto&quot;}

플랫폼의 XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md)&#x200B;.

## 쿼리 서비스 {#query-service}

Query Service를 사용하면 표준 SQL을 사용하여 Adobe Experience Platform에서 데이터를 쿼리할 수 있습니다 [!DNL Data Lake]. Data Lake의 모든 데이터 세트에 참여하고 쿼리 결과를 보고 또는 Data Science Workspace에 사용하거나 실시간 고객 프로필에 수집하기 위한 새 데이터 세트로 캡처할 수 있습니다.

**업데이트된 기능**
&#x200B; | 기능 | 설명 | | — | — | | SQL을 사용하여 프로필용 데이터 세트 활성화 | CTAS 쿼리의 LABEL을 사용하여 데이터 세트를 &#39;profile enabled&#39;로 만들거나, ALTER를 사용하여 프로필에 대해 활성화할 기존 데이터 세트를 업데이트합니다. | | 예약된 쿼리 모니터링 | 예약된 쿼리 탭을 사용하여 쿼리 실행에 대한 중요한 정보를 찾고 경고를 구독합니다. 실패한 경우 일정 세부 사항, 상태 및 오류 메시지/코드에 대한 쿼리를 모니터링합니다.  | | 자동 완성 기능 전환 | 쿼리 편집기 자동 완료 기능을 전환하여 특정 메타데이터 명령을 제거하고 처리 시간을 개선합니다. 이 기능은 작성할 때 쿼리에 대한 잠재적 SQL 키워드와 테이블 세부 정보를 자동으로 제안합니다. | | 데이터 집합 샘플 | 쿼리에서 샘플링 속도를 지정하고 데이터 세트 샘플을 사용하여 균일한 임의 샘플을 만들거나 특정 기준에 따라 조건부 샘플을 만듭니다. |

{style=&quot;table-layout:auto&quot;} &#x200B; Query Services에 대한 자세한 내용은 [쿼리 서비스 개요](../../query-service/home.md). &#x200B;
<!-- Links for QS feature docs after release day: -->
<!-- Enable datasets for profile with SQL link: https://experienceleague.adobe.com/docs/experience-platform/query/sql/syntax.html#create-table-as-select -->
<!-- Monitor scheduled queries link: https://experienceleague.adobe.com/docs/experience-platform/query/monitor-queries.html  -->
<!-- Toggle auto-complete feature link: https://experienceleague.adobe.com/docs/experience-platform/query/ui/user-guide.html#auto-complete -->
<!-- dataset samples: https://experienceleague.adobe.com/docs/experience-platform/query/essential-concepts/dataset-samples.html -->

## Real-Time Customer Data Platform B2B 에디션 {#b2b}

Real-time Customer Data Platform(Real-Time CDP)에 구축된 Real-Time CDP B2B Edition은 비즈니스-비즈니스 서비스 모델로 운영되는 마케터를 위해 특별히 빌드되었습니다. 여러 소스의 데이터를 가져와서 사람 및 계정 프로필에 대한 단일 보기로 결합합니다. 이러한 통합 데이터를 통해 마케터는 특정 대상을 정확하게 타겟팅하고 사용 가능한 모든 채널에서 그러한 대상을 선택할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 관련 계정 서비스 활성화 | 새로운 전환 기능을 사용하면 계정에서 관련 계정 서비스를 활성화할 수 있습니다. 자세한 내용은 다음 안내서를 참조하십시오. [관련 계정 서비스 활성화](../../rtcdp/b2b-ai-ml-services/related-accounts.md#enable). |

{style=&quot;table-layout:auto&quot;}

Real-Time CDP B2B Edition에 대해 자세히 알아보려면 [Real-Time CDP B2B Edition 개요](../../rtcdp/overview.md).

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 다음 방법으로 구독 수준 액세스 지정 [!DNL Google PubSub] | 이제 [!DNL Google PubSub] 인증 시 구독 ID를 제공하여 소스를 만듭니다. 자세한 내용은 [!DNL Google PubSub] 인증 자습서 [흐름 서비스 API 사용](../../sources/tutorials/api/create/cloud-storage/google-pubsub.md) 또는 [플랫폼 UI](../../sources/tutorials/ui/create/cloud-storage/google-pubsub.md). |
| 에서 사용자 지정 활동 데이터 수집 [!DNL Marketo] | 이제 사용자 지정 활동 데이터를 [!DNL Marketo] 인스턴스를 Experience Platform에 추가합니다. 사용자 지정 활동 데이터를 수집하려면 B2B 활동 스키마에서 사용자 지정 활동 필드 그룹을 설정하고 활동 데이터 세트를 사용하여 데이터 흐름을 만들어야 합니다. 데이터 흐름이 완료되면 수집된 데이터 세트에 표준 및 사용자 지정 활동이 모두 포함됩니다 [!DNL Marketo] 인스턴스. 그런 다음 를 사용할 수 있습니다 [쿼리 서비스](../../query-service/home.md) 을 눌러 Platform에서 사용자 지정 활동 레코드에 액세스합니다. 자세한 내용은 다음 안내서를 참조하십시오. [사용자 지정 활동 데이터에 대한 데이터 흐름 만들기](../../sources/tutorials/ui/create/adobe-applications/marketo-custom-activities.md). |
| 미청구 계정 제외 [!DNL Marketo] | 이제 회사 데이터에 대한 데이터 흐름을 만들 때 미청구 계정을 수집에서 제외 또는 포함할지 여부를 구성할 수 있습니다. 자세한 내용은 다음 안내서를 참조하십시오. [소스 연결 및 데이터 흐름 만들기 [!DNL Marketo]](../../sources/tutorials/ui/create/adobe-applications/marketo.md). |

{style=&quot;table-layout:auto&quot;}

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).