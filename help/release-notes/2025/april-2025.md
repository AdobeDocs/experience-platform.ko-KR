---
title: Adobe Experience Platform 릴리스 노트 2025년 4월
description: Adobe Experience Platform에 대한 2025년 4월 릴리스 정보입니다.
exl-id: a3b1e2e8-d780-4e23-b323-37e1a631f716
source-git-commit: b0ed9e38dbc3b4a4f4f7cde5751c2edd35355b59
workflow-type: tm+mt
source-wordcount: '2197'
ht-degree: 28%

---

# Adobe Experience Platform 릴리스 정보

>[!TIP]
>
>다른 Adobe Experience Platform 애플리케이션의 릴리스 노트는 다음 설명서를 참조하십시오.
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/ko/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/en/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/ko/docs/analytics-platform/using/releases/latest)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/en/docs/real-time-cdp-collaboration/using/latest)

**릴리스 일자: 2025년 4월 29일 수요일**

Adobe Experience Platform의 기존 기능 및 설명서 업데이트:

- [Experience League](#experience-league)
- [데이터 수집](#data-collection)
- [대상](#destinations)
- [경험 데이터 모델](#xdm)
- [ID 서비스](#identity)
- [쿼리 서비스](#query-service)
- [실시간 고객 프로필](#profile)
- [샌드박스](#sandboxes)
- [소스](#sources)
- [사용 사례 플레이북](#use-case-playbooks)

## Experience League {#experience-league}

Experience League은 Adobe 제품을 통해 기술을 향상시킬 수 있도록 설계된 포괄적인 학습 플랫폼입니다. 과정, 설명서, 커뮤니티 페이지, 이벤트 및 인증 액세스 등 다양한 리소스를 제공합니다.

| 기능 | 설명 |
| --- | --- |
| 개인화된 홈 페이지 | [Experience League](https://experienceleague.adobe.com/en/home#)에서 개인 맞춤화된 홈 페이지에 액세스하고 사용자 지정하세요. Adobe 자격 증명으로 로그인한 다음 상단 메뉴에서 **[!UICONTROL Experience League]**&#x200B;을(를) 선택하여 학습 환경을 최적화합니다. <ul><li>**책갈피**: [!UICONTROL 책갈피] 기능을 사용하여 좋아하는 리소스를 한 곳에 저장하고 수집합니다. 플레이리스트, 문서 및 튜토리얼을 비롯한 다양한 콘텐츠를 저장할 수 있습니다.</li><li>**학습 사용자 지정**: 사용자의 요구 사항에 가장 적합한 역할, 업계, 제품 및 경험 수준으로 Experience League 프로필을 업데이트하여 학습 환경을 향상시킵니다.</li><li>**권장 사항**: 최근 활동에 따라 권장되는 학습 콘텐츠를 봅니다.</li><li>**최근에 본 항목**: [!UICONTROL 최근에 본 항목] 섹션을 사용하여 문서 및 비디오와 같은 최근에 본 콘텐츠로 빠르게 다시 이동합니다.</li><li>**학습 리소스**: [!UICONTROL 모든 학습 리소스] 패널을 사용하여 튜토리얼, 설명서, 커뮤니티, 이벤트 및 인증으로 이동합니다.</li><li>**새로운 기능**: Experience League의 최신 콘텐츠 스트림에 대한 [!UICONTROL 새로운 기능] 섹션을 봅니다.</li><li>**필요 시 이전 이벤트 보기**: [!UICONTROL 필요 시 이전 이벤트 보기] 섹션에서 제품 스포트라이트, 사용 사례 및 튜토리얼에 대해 이전에 기록된 실시간 스트림을 봅니다.</li></ul><br> Experience League에서 ![개인 설정된 홈 페이지입니다.](../2025/assets/april/personalized-home-page.png "Experience League에서 개인 맞춤화된 홈 페이지입니다."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

## 데이터 수집 {#data-collection}

Adobe Experience Platform은 클라이언트측 고객 경험 데이터를 수집하여 Adobe 또는 비 Adobe 대상으로 보강, 변환 및 배포가 가능한 Adobe Experience Platform Edge Network로 보낼 수 있는 기술 제품군을 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [!DNL Adform] 확장 기능 | [!DNL Adform] 서버측 확장을 사용하면 브랜드가 ECID를 사용하여 오프사이트에서 대상자를 쉽게 재타겟팅할 수 있습니다. 이 서버측 확장은 서드파티 쿠키 또는 쿠키 대체 ID에 의존하지 않습니다. 또한 이 작업은 전적으로 서버측에서 수행되므로 추가 픽셀이나 다른 클라이언트측 변경 사항이 필요하지 않습니다. 자세한 내용은 [Adform 확장 개요](/help/tags/extensions/server/adform/overview.md)를 참조하십시오. |
| [!DNL Amazon] 웹 이벤트 API 확장 | [!DNL Amazon] 전환 API 확장을 사용하면 광고주가 웹 사이트 상호 작용을 [!DNL Amazon]과(와) 직접 공유할 수 있으므로 향상된 속성, 데이터 안정성 및 캠페인 최적화를 제공합니다. 이 확장은 이벤트 전달을 지원하므로 정확한 보고를 위해 적절한 중복 제거를 보장하는 동시에 구매, 장바구니 추가 등과 같은 전환 이벤트를 전송할 수 있습니다. 자세한 내용은 [Amazon 확장 개요](/help/tags/extensions/server/amazon/overview.md)를 참조하십시오. |

{style="table-layout:auto"}

## 대상 {#destinations}

[!DNL Destinations]는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있는 대상 플랫폼과 사전 설치된 통합입니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타기팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새 대상 또는 업데이트된 대상** {#new-updated-destinations}

| 대상 | 설명 |
| --- | --- |
| [Marketo Engage 사용자 동기화](/help/destinations/catalog/adobe/marketo-engage-person-sync.md) | Adobe은 id 맵에 여러 전자 메일이 있을 때 고객에게 영향을 미치는 문제를 해결하기 위해 [!DNL Marketo Engage Person Sync] 대상을 업데이트했습니다. |
| [(V2) 페가 CDH 실시간 대상 연결](/help/destinations/catalog/personalization/pega-v2.md) | Adobe Experience Platform Pega 계정에 여러 개의 Pega 고객 결정 허브 응용 프로그램이 구성되어 있는 경우, 프로필 속성 및 대상자 멤버십 데이터를 Pega 고객 결정 허브로 보내어 차선책을 결정하십시오.[!DNL (V2) Pega Customer Decision Hub Realtime Audience] |

**새로운 기능 또는 업데이트된 기능** {#destinations-new-updated-functionality}

| 기능 | 설명 |
| --- | --- |
| 전체 파일 내보내기를 위한 **주별** 및 **월별** 예약 옵션 | 이제 클라우드 스토리지 파일 기반 대상으로 활성화할 때 사용자 및 잠재 고객에 대한 전체 파일 내보내기를 주별 또는 월별 기준으로 예약할 수 있습니다. 예약 옵션에 대해 [자세히 읽어보기](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files). |

{style="table-layout:auto"}

**수정 사항, 개선 사항 및 기타 공지** {#destinations-fixes-and-enhancements}

- **데이터 세트 내보내기 종료 날짜 적용 지연 2025년 9월 1일**\
  [2024년 9월 릴리스](/help/release-notes/2024/september-2024.md#destinations-new-updated-functionality)의 일부로, Adobe은 해당 릴리스 *전에 만들어진 데이터 세트 내보내기 데이터 흐름*&#x200B;에 대해 기본 종료 날짜를 2025년 5월 1일로 설정했습니다. 이제 Adobe에서 이 시행 기한을 **2025년 9월 1일**(으)로 연장하여 고객에게 일정을 업데이트할 추가 시간을 제공합니다. 데이터 세트 내보내기 데이터 흐름의 종료 날짜를 편집하는 방법에 대한 자세한 내용은 [데이터 세트 내보내기 자습서](../../destinations/ui/export-datasets.md#schedule-dataset-export)의 예약 섹션을 참조하십시오.

- **LiveRamp 온보딩에 대한 실패한 SFTP 전송 처리 개선**\
  Adobe은 SFTP를 통해 [LiveRamp 온보딩](/help/destinations/catalog/advertising/liveramp-onboarding.md) 대상으로 파일 내보내기에 영향을 주는 문제에 대한 수정 사항을 구현했습니다. 때때로 일시적인 서버측 문제로 인해 파일 전송이 실패하고 실패한 시도에서 임시 파일이 서버에 남아 있습니다. Adobe에 덮어쓸 수 있는 권한이 없으므로 이러한 삭제할 수 없는 파일은 후속 재시도를 차단했습니다.\
  이 문제를 수정하여 다시 시도에서 임시 파일을 삭제할 수 없는 경우 Adobe은 다시 시도가 성공적으로 완료되도록 접미사 `attempt2`이(가) 추가된 새 파일을 생성합니다.

## 경험 데이터 모델 (XDM) {#xdm}

XDM은 Adobe Experience Platform으로 가져오는 데이터에 대한 공통 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수하여 모든 고객 경험 데이터를 공통된 표현에 통합해 보다 빠르고 통합된 방식으로 인사이트를 제공할 수 있습니다. 고객 조치에서 귀중한 인사이트를 얻고, 세그먼트를 통해 고객 대상자를 정의하고, 개인 설정 목적으로 고객 속성을 사용할 수 있습니다.

**업데이트된 XDM 구성 요소**

| 기능 | 설명 |
| --- | --- |
| 문자열 필드는 최소값 1을 받습니다. | 새 문자열 필드에는 기본적으로 최소 1의 길이가 제공됩니다. 필수가 아닌 필드에 대한 Null 값은 여전히 사용할 수 있습니다. 모범 사례에 대한 자세한 내용은 [데이터 모델링 모범 사례](../../xdm/schema/best-practices.md#data-integrity-tips)에 대한 안내서를 참조하십시오. |

{style="table-layout:auto"}

Experience Platform의 XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md)를 참조하십시오.

## ID 서비스 {#identity}

Adobe Experience Platform ID 서비스를 사용하여 여러 디바이스 및 시스템에 걸쳐 ID를 연결하여 고객과 고객의 행동을 종합적으로 파악할 수 있으므로, 실시간으로 효과적인 개인 디지털 환경을 제공할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [!BADGE 제한된 가용성]{type=Informative} [!DNL Identity Graph Linking Rules] | ID 그래프 연결 규칙은 이제 제한된 가용성에 있으며 개발 샌드박스에서 모든 고객이 액세스할 수 있습니다. <ul><li>**활성화 요구 사항**: 이 기능은 [!DNL Identity Settings]을(를) 구성하고 저장할 때까지 비활성 상태로 유지됩니다. 이 구성이 없으면 시스템이 동작을 변경하지 않고 계속 정상적으로 작동합니다.</li><li>**중요 정보**: 이 제한된 가용성 단계에서 Edge 세그먼테이션을 수행하면 예기치 않은 세그먼트 멤버십 결과가 발생할 수 있습니다. 하지만 스트리밍 및 배치 세분화는 예상대로 작동합니다.</li><li>**다음 단계**: 프로덕션 샌드박스에서 이 기능을 활성화하는 방법에 대한 자세한 내용은 Adobe 계정 팀에 문의하십시오.</li></ul> |

{style="table-layout:auto"}

자세한 내용은 [[!DNL Identity Graph Linking Rules] 설명서](../../identity-service/identity-graph-linking-rules/overview.md)를 참조하세요.

## 쿼리 서비스 {#query-service}

쿼리 서비스가 포함된 표준 SQL을 사용하여 Adobe Experience Platform 데이터 레이크에서 데이터를 쿼리합니다. 데이터 세트를 원활하게 결합하고 쿼리 결과에서 새로운 데이터 세트를 생성하여 보고를 강화하고, 데이터 과학 워크플로를 활성화하거나, 실시간 고객 프로필로 수집할 수 있습니다. 예를 들어 고객 거래 데이터와 행동 데이터를 병합하여 타기팅된 마케팅 캠페인의 가치가 높은 대상자를 파악할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| SQL 대상자 덮어쓰기 | 새 SQL 쿼리의 결과로 기존 프로필을 덮어써서 대상 멤버십을 새로 고칩니다. 이렇게 하면 오래된 레코드를 제거하고 업데이트된 레코드를 단일 작업에 삽입하여 동적 대상을 보다 효율적으로 관리할 수 있습니다. 자세한 내용은 [SQL 대상자 확장 안내서](../../query-service/data-distiller-audiences/overview.md#replace-audience)를 참조하십시오. |
| 쿼리 결과 다운로드 및 복사 | [쿼리 편집기에서 직접 쿼리 결과를 다운로드](../../query-service/ui/overview.md#download-query-results)하거나 CSV, XLSX 또는 JSON 파일로 [클립보드에 결과 복사](../../query-service/ui/overview.md#copy-results)를 쉼표로 구분된 값(CSV)으로 사용하여 Excel과 같은 스프레드시트 애플리케이션에서 빠르게 사용할 수 있습니다. 이러한 개선 사항을 통해 오프라인 분석, 보고 및 데이터 유효성 검사 워크플로우가 간소화됩니다. |
| 전체 화면에서 쿼리 결과 보기 | [쿼리 결과를 미리 보면 전체 화면 대화 상자가 표시됩니다](../../query-service/ui/overview.md#view-results) 가독성을 높이고 대용량 데이터 세트를 쉽게 스캔하며 복사할 행을 선택할 수 있습니다. 전체 화면 보기는 크기 조정 가능한 그리드 레이아웃을 제공하므로 넓은 표와 세부 출력을 보다 효율적으로 검토할 수 있습니다. |
| 모델 예측의 향상된 열 선택 | 특정 열을 선택하고 확장된 `model_predict` 구문을 사용하여 별칭을 적용합니다. 특징 벡터 및 확률 점수와 같은 중간 예측 결과를 검색합니다. 향상된 선택을 수행하려면 기능 플래그 활성화가 필요합니다. 구문 예 및 기능 플래그 세부 정보는 [모델 라이프사이클 설명서](../../query-service/advanced-statistics/models.md#select-specific-output-fields)를 참조하십시오. |
| 테이블 생성 및 삽입을 사용하여 모델 예측 출력 저장 | [CREATE TABLE AS SELECT를 사용하여 선택한 예측 출력을 새 테이블에 저장하거나 INSERT INTO SELECT를 사용하여 기존 테이블에 삽입](../../query-service/advanced-statistics/models.md#predict). 향상된 열 선택이 활성화되면 피쳐 벡터 및 확률과 같은 중간 결과가 최종 예측과 함께 지속될 수도 있습니다. 사용 예제는 [SQL 구문 설명서](../../query-service/sql/syntax.md#create-table-as-select)를 참조하세요. |

[!DNL Query Service]에 대한 자세한 내용은 [[!DNL Query Service] 개요](../../query-service/home.md)를 참조하십시오.

## 실시간 고객 프로필 {#profile}

Adobe Experience Platform을 사용하면 고객이 언제 어디서 브랜드와 상호 작용하는지에 관계없이 고객을 위한 조직화되고 일관되며 관련성 높은 경험을 제공할 수 있습니다. 실시간 고객 프로필을 사용하면 온라인, 오프라인, CRM 및 서드파티 데이터를 비롯한 여러 채널의 데이터를 결합하여 각 개별 고객에 대한 거시적인 보기를 확인할 수 있습니다. 프로필을 사용하면 모든 고객의 상호 작용에 대해 실행 가능한 타임스탬프가 지정된 계정을 제공하는 통합 보기로 고객 데이터를 통합할 수 있습니다.

| 기능 | 설명 |
| ------- | ----------- |
| 익명 프로필 데이터 만료 | 프로필 대시보드에서 익명 프로필 데이터 만료를 관리합니다. 이 기능과 익명 프로필에 대한 자세한 내용은 [익명 프로필 데이터 만료 안내서](../../profile/pseudonymous-profiles.md)를 참조하십시오. |

{style="table-layout:auto"}

실시간 고객 프로필에 대해 자세히 알아보려면 [프로필 개요](../../profile/home.md)를 참조하십시오.

## 샌드박스 {#sandboxes}

Adobe Experience Platform은 전 세계적으로 디지털 체험 애플리케이션을 풍부하게 제공하기 위해 구축되었습니다. 기업은 여러 디지털 경험 애플리케이션을 동시에 실행하는 경우가 많으며, 운영 규정 준수를 보장하면서 이러한 애플리케이션의 개발, 테스트 및 배포를 처리해야 합니다. 이러한 요구 사항을 처리하기 위해 Experience Platform은 디지털 경험 애플리케이션을 개발하고 발전시키는 데 도움이 되는 단일 Experience Platform 인스턴스를 별도의 가상 환경으로 분류해 주는 샌드박스를 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 샌드박스 도구 플러그인 지원 확장 | 이제 샌드박스 툴에서 사용자 지정 작업을 여정 개체를 복제할 때 종속 개체로 복사할 수 있습니다. 또한 대상 샌드박스에서 재사용할 기존 작업을 선택할 수 있습니다. 패키지에 개별적으로 추가할 수도 있습니다. 지원되는 Adobe Journey Optimizer 개체에 대한 자세한 내용은 [샌드박스 도구](../../sandboxes/ui/sandbox-tooling.md#adobe-journey-optimizer-objects) 안내서를 참조하십시오. |

{style="table-layout:auto"}

샌드박스에 대한 자세한 내용은 [샌드박스 개요](../../sandboxes/home.md)를 참조하십시오.

## 소스 {#sources}

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

Experience Platform의 소스를 사용하여 Adobe 애플리케이션 또는 서드파티 데이터 소스에서 데이터를 수집합니다.

**새로운 소스**

| 기능 | 설명 |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Algolia User Profiles] | 이제 [[!DNL Algolia User Profiles]](../../sources/connectors/data-partners/algolia-user-profiles.md) 원본을 사용할 수 있습니다. 이 소스를 사용하여 [!DNL Algolia] 사용자 프로필 관심도 데이터를 Experience Platform으로 가져옵니다. 그런 다음 이 데이터를 사용하여 웹 사이트, 전자 상거래 플랫폼 및 애플리케이션에 대한 고성능 검색 솔루션을 제공함으로써 사용자 참여, 전환율 및 전반적인 고객 경험을 향상시킬 수 있습니다. 자세한 내용은 Experience Platform에 데이터를 [수집 [!DNL Algolia User Profiles] 하는 방법](../../sources/tutorials/ui/create/data-partners/algolia-user-profiles.md)에 대한 안내서를 참조하십시오. |
| [!DNL Azure Databricks]에 대한 [!BADGE Beta]{type=Informative} API 지원 | 이제 API에서 [!DNL Azure Databricks] 소스를 사용할 수 있습니다. [!DNL Flow Service] API를 사용하여 [!DNL Databricks] 계정을 연결하고 [!DNL Databricks] 데이터를 Experience Platform으로 가져옵니다. 자세한 내용은 [[!DNL Azure Databricks]](../../sources/connectors/databases/databricks.md)의 설명서를 참조하십시오. |

{style="table-layout:auto"}

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 스트리밍 미디어 데이터를 Experience Platform으로 수집하기 위한 XDM 필드가 업데이트되었습니다. | 이제 새로운 XDM 필드 그룹 `mediaReporting`을(를) 사용하여 Adobe Analytics 소스를 통해 Experience Platform으로 스트리밍 미디어 데이터를 수집할 수 있습니다. 이 필드는 `media.mediaTimed` 필드를 대체합니다.</br> <br>3개월의 전환 기간 동안 `media.mediaTimed` 필드에 대한 데이터 수집이 계속됩니다. 그러나 2025년 7월 말부터 `media.mediaTimed` 필드는 완전히 사용되지 않으며 더 이상 Experience Platform 스키마 UI에 표시되지 않으며, 데이터는 `mediaReporting` 필드를 사용해서만 전송됩니다.</br><br>2025년 4월 22일 이전에 스트리밍 미디어 데이터를 플랫폼으로 수집하도록 Analytics 소스를 구현한 경우 새 필드 그룹을 사용하여 데이터를 보내려면 기존 구성을 마이그레이션해야 합니다. 이 마이그레이션은 2025년 7월 말까지 완료해야 합니다. Adobe 계정 팀에 문의하여 마이그레이션 지원을 받으십시오. |
| [!DNL MariaDB] 및 [!DNL PostgreSQL]에 대한 새 인증 유형 | 이제 기본 인증을 사용하여 Experience Platform에서 [!DNL MariaDB] 및 [!DNL PostgreSQL] 소스를 인증할 수 있습니다. 자세한 내용은 다음 설명서를 참조하십시오. <ul><li>[[!DNL MariaDB]](../../sources/connectors/databases/mariadb.md)</li><li>[[!DNL PostgreSQL]](../../sources/connectors/databases/postgres.md) |
| [!DNL Amazon Redshift]에 대한 행 수준 필터링 지원 | Experience Platform에서 [!DNL Amazon Redshift] 데이터에 행 수준 필터링 기능을 사용할 수 있습니다. 자세한 내용은 [API의 소스에 대한 행 수준 데이터 필터링](../../sources/tutorials/api/filter.md)에 대한 안내서를 참조하십시오. |

{style="table-layout:auto"}

자세한 내용은 [소스 개요](../../sources/home.md)를 참조하십시오.

## 사용 사례 플레이북 {#use-case-playbooks}

사용 사례 플레이북은 원래 Real-Time Customer Data Platform 또는 Adobe Journey Optimizer을 시작할 때 문제를 해결하는 데 도움이 되도록 설계되었습니다. 이러한 기능은 지속적으로 발전하고 있으며, 이제 주요 마케팅 사용 사례를 점프하고 테스트하고 프로덕션으로 이동할 수 있는 영감과 사전 구축된 에셋을 제공할 수 있습니다.

사용 사례 플레이북이 검색 도구에서 공동 작업 프레임워크로 전환되었습니다. 이제 다양한 조직에서 나만의 플레이북을 만들고, 관리하고, 공유할 수 있도록 지원합니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [!BADGE Beta]{type=Informative} 플레이북을 작성하고 공유합니다. | 새로운 플레이북 작성 프레임워크를 사용하여 고유한 사용 사례 플레이북을 만들고, 관리하고, 공유할 수 있습니다. 여기에는 주요 메타데이터 캡처, 여정 맵 편집 및 관련 기술 에셋 연결에 대한 지원이 포함됩니다. 조직 간에 플레이북을 공유하여 마케팅 접근 방식을 표준화하고 일관성을 유지할 수 있습니다. |

{style="table-layout:auto"}

플레이북을 직접 작성하고 공유하는 방법에 대해 알아보려면 [작성자 및 공유하기](/help/use-case-playbooks/playbooks/author.md) 문서를 읽어보세요.

자세한 내용은 인스턴스를 만들고 생성된 에셋을 다른 샌드박스 환경으로 가져오는 방법을 포함하여 플레이북의 기능, 용도 및 엔드투엔드 데모에 대한 개요를 제공하는 [사용 사례 플레이북 개요](/help/use-case-playbooks/playbooks/overview.md)를 읽어 보십시오.