---
title: Adobe Experience Platform 릴리스 정보
description: Adobe Experience Platform에 대한 2023년 3월 릴리스 노트입니다.
source-git-commit: 1aeaf832f6cb2acf65c25199693b06669682883b
workflow-type: tm+mt
source-wordcount: '2345'
ht-degree: 4%

---

# Adobe Experience Platform 릴리스 노트

>[!IMPORTANT]
>
>2023년 4월 5일부터 `Existing` 세그먼트 멤버십 라이프사이클에서 중복을 제거하기 위해 상태는 세그먼트 멤버십 맵에서 더 이상 사용되지 않습니다. 이 변경 후 세그먼트에 자격을 갖춘 프로필은 로 표시됩니다 `Realized` 그리고 자격이 없는 프로필은 `Exited`. 이 변경 사항에 대한 자세한 내용은 [세분화 서비스 섹션](#segmentation).

**릴리스 일자: 2023년 3월 29일**

Adobe Experience Platform의 기존 기능 업데이트:

- [대시보드](#dashboards)
- [데이터 수집](#data-collection)
- [데이터 준비](#data-prep)
- [대상](#destinations)
- [경험 데이터 모델](#xdm)
- [쿼리 서비스](#query-service)
- [Real-Time Customer Data Platform B2B 에디션](#b2b)
- [세분화 서비스](#segmentation)
- [소스](#sources)

## 대시보드 {#dashboards}

Adobe Experience Platform은 일별 스냅샷 중에 캡처된 대로 조직의 데이터에 대한 중요한 통찰력을 볼 수 있는 여러 개의 대시보드를 제공합니다.

**새로운 기능 또는 업데이트된 기능** {#dashboards-new-updated-features}

| 기능 | 설명 |
| --- | --- |
| 사용자 정의 대시보드 | 이제 다음을 수행할 수 있습니다 **샘플 속성 값** 사용자 정의 대시보드 위젯 작성기에서 위젯에 속성을 추가하기 전에 위젯을 만들 때 해당 속성 열의 몇 가지 샘플 값을 개별 속성에 사용할 수 있습니다.<br>이제 다음을 수행할 수 있습니다 **X축과 Y축 교체** 위젯에서 축 교체 단추를 사용합니다. 따라서 시간을 절약할 수 있고, 위젯에 속성을 추가할 때 보다 인체공학적 경험을 제공할 수 있습니다. 이렇게 하면 속성 패널에서 두 속성을 다시 찾아야 합니다.<br>이제 다음을 수행할 수 있습니다 **범례의 위치 및 제목 변경** 위젯 내에서 사용할 수 있습니다. 위젯에 범례가 있으면 차트 주위의 어느 곳에서든 해당 범례를 재배치하고 축 레이블과 위젯 제목을 사용할 수 있으므로 범례 제목도 다시 지정할 수 있습니다. |

{style="table-layout:auto"}

액세스 권한을 부여하고 사용자 지정 위젯을 만드는 방법 등 대시보드에 대한 자세한 내용은 [대시보드 개요](../../dashboards/home.md).

## 데이터 수집 {#data-collection}

Adobe Experience Platform은 클라이언트측 고객 경험 데이터를 수집하고 Adobe Experience Platform Edge Network로 전송하여 Adobe 또는 비Adobe 대상으로 보강, 변환 및 배포할 수 있는 기술 세트를 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 신규 메타 전환 API(베타)에 대한 빠른 시작 워크플로우 | 데이터 수집 홈 화면에서 &quot;시작하기&quot;에서 새로운 빠른 시작 워크플로우에 액세스합니다. 다음 [메타 전환 API에 대한 빠른 시작 워크플로우](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start) 에서는 몇 가지 간단한 단계로 이벤트 데이터를 서버 측에서 Meta로 수집하여 전송할 수 있습니다. |
| [!DNL Braze] 이벤트 전달 확장 | 다음 [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 이벤트 전달 확장을 사용하면 Adobe Experience Platform Edge Network에서 캡처한 데이터를 활용하여 로 보낼 수 있습니다 [!DNL Braze] 를 사용하여 서버측 이벤트 형태로 [!DNL Braze] 사용자 추적 API. |
| [!DNL Epsilon] 이벤트 전달 확장 | 다음 [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/overview.html) 확장 기능을 사용하면 이벤트 전달을 활용하여 Adobe Experience Platform Edge Network에서 이벤트 정보를 캡처하고 로 전송할 수 있습니다 [!DNL Epsilon] 사용 [!DNL Epsilon] 이벤트 API. |
| [!DNL Mixpanel] 이벤트 전달 확장 | 다음 [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 확장 을 사용하면 이벤트 전달을 활용하여 Adobe Experience Platform Edge Network에서 이벤트 정보를 캡처하고 이벤트 추적 API를 사용하여 Mixpanel에 전송할 수 있습니다. |

{style="table-layout:auto"}

## 데이터 준비 {#data-prep}

데이터 준비를 통해 데이터 엔지니어가 XDM(Experience Data Model) 간 데이터를 매핑, 변환 및 확인할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| Adobe Analytics 데이터 필터링의 일반 가용성 | 이제 데이터 준비 기능을 사용하여 규칙 및 조건을 적용하여 실시간 고객 프로필에 수집하기 전에 Analytics 데이터를 필터링할 수 있습니다. 자세한 내용은 다음 안내서를 참조하십시오. [프로필 수집을 위한 Analytics 데이터 필터링](../../sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-profile). |
| URL 문자열 인코딩 및 디코딩의 새로운 함수 | <ul><li>다음 `get_url_encoded` 함수는 URL을 입력으로 사용하고 특수 문자를 ASCII 문자로 바꾸거나 인코딩합니다.</li><li>다음 `get_url_decoded` 함수는 URL을 입력으로 사용하고 ASCII 문자를 특수 문자로 디코딩합니다.</li></ul> 자세한 내용은 [데이터 준비 함수 안내서](../../data-prep/functions.md). 예약된 문자와 해당 인코딩된 문자의 전체 목록을 보려면 다음 안내서를 읽어 보십시오 [특수 문자](../../data-prep/functions.md#special-characters). |

데이터 준비에 대한 자세한 내용은 [데이터 준비 개요](../../data-prep/home.md).

## 대상 {#destinations}

[!DNL Destinations] 는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 구축된 통합입니다. 대상을 사용하여 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례에 대해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새 대상** {#new-destinations}

| 대상 | 설명 |
| ----------- | ----------- |
| [[!DNL Adobe Commerce] 연결 GA](../../destinations/catalog/personalization/adobe-commerce.md) | 다음 [!DNL Adobe Commerce] 대상 커넥터 (현재 일반적으로 사용 가능)를 사용하여 하나 이상의 Real-Time CDP 대상을 선택하여 [!DNL Adobe Commerce] 고객을 위한 동적 개인화된 경험을 제공하기 위한 계정입니다. |
| [[!DNL Snap Inc] 연결 GA](../../destinations/catalog/advertising/snap-inc.md) | 다음 [!DNL Snap Inc] 대상 커넥터(현재 일반적으로 사용 가능)를 통해 마케터는 Experience Platform에서 만든 사용자 세그먼트를 [!DNL Snapchat Ads] 광고를 타겟팅하는 데 사용합니다. |
| [(API) Oracle Eloqua 연결](../../destinations/catalog/email-marketing/oracle-eloqua-api.md) | API 기반 연결을 사용하여 다음을 수행할 수 있습니다 [!DNL Oracle Eloqua] 잠재 고객을 위한 개인화된 고객 경험을 제공하면서 캠페인을 계획 및 실행하는 방법 [!DNL Oracle Eloqua]. |
| [(베타) [!DNL Amazon Ads] 연결](../../destinations/catalog/advertising/amazon-ads.md) | 다음 [!DNL Amazon Ads] Adobe Experience Platform와의 통합을 통해 [!DNL Amazon Ads] 다음을 포함한 제품 [!DNL Amazon DSP (ADSP)]. 사용 [!DNL Amazon Ads] Adobe Experience Platform에서 사용자는 타깃팅 및 활성화를 위한 광고주 대상을 정의할 수 있습니다 [!DNL Amazon DSP]. |
| [[!DNL Marketo Measure Ultimate] 연결](../../destinations/catalog/adobe/marketo-measure-ultimate.md) | [!DNL Marketo Measure] (이전 Bizible)은 마케터에게 기업의 매출을 증대하고 투자 수익을 극대화하는 데 가장 효과적인 마케팅 활동을 파악하는 데 도움이 됩니다. 대상을 사용하면 B2B(Business-to-Business) 데이터가 Adobe Experience Platform에서 로 이동할 수 있습니다 [!DNL Marketo Measure]. 카드만 사용할 수 있습니다 [!DNL Marketo Measure Ultimate] 고객. |
| [TikTok 연결](../../destinations/catalog/social/tiktok.md) | 광고 캠페인으로 타겟팅할 데이터를 사용하여 TikTok에서 사용자 지정 대상을 만듭니다. |
| [Zendesk 연결](../../destinations/catalog/crm/zendesk.md) | 세그먼트 내에서 연락처로 ID를 만들고 업데이트하려면 이 대상을 사용합니다 [!DNL Zendesk]. |

{style="table-layout:auto"}

**새 기능 또는 업데이트된 기능** {#destinations-new-updated-functionality}

| 기능 | 설명 |
| ----------- | ----------- |
| 대상에 대한 새 액세스 제어 권한: [[!DNL Activate Segments without Mapping]](../../access-control/home.md#permissions) | 새 권한을 통해 사용자는 세그먼트를 표시하지 않고 기존 대상에 활성화할 수 있습니다 [매핑 단계](../../destinations/ui/activate-batch-profile-destinations.md#mapping). 활성화 워크플로우에서 세그먼트를 추가 및 제거할 수 있지만 매핑된 속성 또는 ID를 추가 또는 제거할 수 없습니다. |

{style="table-layout:auto"}

**수정 사항 및 향상된 기능** {#destinations-fixes-and-enhancements}

실시간 CDP를 위한 파일 기반 대상에서 PGP/GPG 암호화에 대한 버그 수정이 해제되었습니다. 이러한 변경 사항으로 현재 암호화를 사용하는 기존 파일 기반 대상은 이전보다 확장자가 다른 파일 이름을 생성합니다.

- 암호화를 사용할 때의 현재 확장: `filename.csv`
- 암호화 사용 시 향후 확장: `filename.csv.gpg`

대상에 대한 자세한 내용은 [대상 개요](../../destinations/home.md).

## XDM(경험 데이터 모델) {#xdm}

XDM은 Adobe Experience Platform으로 가져온 데이터에 대한 일반적인 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수함으로써 모든 고객 경험 데이터를 공통 표현으로 통합하여 보다 빠르고 통합된 방식으로 통찰력을 제공할 수 있습니다. 고객 작업을 통해 유용한 통찰력을 얻을 수 있고, 세그먼트를 통해 고객 대상을 정의하고, 개인화를 위해 고객 속성을 사용할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| CSV로 스키마 권장 사항 | 이제 로컬 파일을 업로드하여 기계 학습을 통해 생성된 스키마를 만들어 수동으로 스키마를 생성할 필요가 없습니다. 에서 [!UICONTROL 소스] 작업 공간, 샘플 CSV 파일 업로드 및 Adobe 기계 학습 알고리즘은 대상 필드를 기반으로 하는 스키마를 제안합니다. 자세한 내용은 [설명서](../../ingestion/tutorials/map-csv/recommendations.md)를 참조하십시오.&quot; |

{style="table-layout:auto"}

**새로운 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 클래스 | [[!UICONTROL 오퍼 항목]](https://github.com/adobe/xdm/pull/1678/files) | 오퍼를 나타내는 클래스입니다. |
| 클래스 | [[!UICONTROL 의사 결정 항목]](https://github.com/adobe/xdm/pull/1678/files) | 의사 결정을 내릴 수 있는 항목입니다. 의사 결정 프로세스의 출력은 하나 이상의 의사 결정 항목입니다. |
| 클래스 | [[!UICONTROL 미디어 세션 서버 시간 초과]](https://github.com/adobe/xdm/pull/1676/files) | 이는 사용자의 마지막으로 알려진 상호 작용과 세션이 닫히는 시간(초)을 나타냅니다. |
| 필드 그룹 | [[!UICONTROL XDM 프로필 계산 속성]](https://github.com/adobe/xdm/pull/1686/files) | 이렇게 하면 내부 Adobe 서비스에서 계산된 속성이 들어오는 고객 데이터에 추가됩니다. 고객이 데이터를 수집하는 데 사용해서는 안 됩니다. |
| 데이터 형식 | [[!UICONTROL 환불 품목]](https://github.com/adobe/xdm/pull/1685/files) | 환불이 주문과 연관되어 있는지 여부를 나타내며 환불 유형, 금액 및 관련 통화를 정의합니다. |
| 데이터 형식 | [[!UICONTROL 카테고리 데이터]](https://github.com/adobe/xdm/pull/1677/files) | 이 새 데이터 유형은 제품의 카테고리를 나타냅니다. |
| 스키마 | [[!UICONTROL Adobe Target 분류 필드]](https://github.com/adobe/xdm/pull/1682/files) | Target 분류 데이터 세트에 대한 새 XDM 스키마를 만들었습니다. 여기에는 Target 활동 및 경험을 분류하는 메타데이터 필드 세트가 포함되어 있습니다. |

{style="table-layout:auto"}

**업데이트된 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 필드 그룹 | [[!UICONTROL 컨텐츠 구성 요소 세부 사항]](https://github.com/adobe/xdm/pull/1674/files) | `uri-reference` 에서 제거됨 [!UICONTROL 컨텐츠 구성 요소 세부 사항] |
| 필드 그룹 | [[!UICONTROL AJO 엔티티 태그]](https://github.com/adobe/xdm/pull/1672/files) | 에 AJO 엔티티 태그가 추가되었습니다. [!UICONTROL AJO 엔티티 필드]여정 또는 캠페인에 해당하는 경우 |
| 필드 그룹 | (복수) | 에 대한 여러 필드가 추가되었습니다 [[!UICONTROL Journey Orchestration 단계 이벤트 공통 필드]](https://github.com/adobe/xdm/pull/1671/files) |
| 필드 그룹 | (복수) | [에 대한 여러 XDM 이벤트 유형이 추가되었습니다. [!UICONTROL 미디어 보고]](https://github.com/adobe/xdm/pull/1670/files). |
| 필드 그룹 | [!UICONTROL Workfront 변경 이벤트] | 다음 `Full Record` 및 `Accessor Employee Ids` 필드 그룹이 추가되었습니다. |
| 데이터 형식 | [[!UICONTROL 제품 목록 항목]](https://github.com/adobe/xdm/pull/1685/files) | 다음 [!UICONTROL 환불 금액] 가 추가되어 있는 경우 해당 품목에 대해 환급된 금액이 있습니다. |
| 데이터 형식 | [[!UICONTROL 주문 ]](https://github.com/adobe/xdm/pull/1685/files) | [!UICONTROL 환불 목록] 이 주문에 대한 환불 목록에 추가되었습니다. |
| 데이터 형식 | [[!UICONTROL 제품 목록 항목 ]](https://github.com/adobe/xdm/pull/1677/files) | 제품 카테고리가 이 제품의 카테고리 데이터 목록에 추가되었습니다. |
| 데이터 유형 | [!UICONTROL 세션 세부 정보] | 가 추가되었습니다. `pev3` 문자열 필드 [보고에 사용되는 미디어 스트림의 유형을 나타냅니다](https://github.com/adobe/xdm/pull/1676/files). 또한 `pccr` 속성은 리디렉션이 발생했는지 여부를 나타냅니다. |
| 데이터 유형 | [!UICONTROL 구매요청 목록] | 다음을 제공합니다. [구매요청 목록 등록 정보](https://github.com/adobe/xdm/pull/1675/files). 여기에는 이름, ID 및 설명이 포함됩니다. |
| 데이터 유형 | [!UICONTROL Commerce] | 다음 [상거래 데이터 유형이 업데이트되었습니다](https://github.com/adobe/xdm/pull/1675/files) 다음을 포함합니다. `requisitionListOpens`, `requisitionListAdds`, `requisitionListRemovals`, 및 `requisitionList`. |

{style="table-layout:auto"}

플랫폼의 XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md).

## 쿼리 서비스 {#query-service}

Query Service를 사용하면 표준 SQL을 사용하여 Adobe Experience Platform에서 데이터를 쿼리할 수 있습니다 [!DNL Data Lake]. Data Lake의 모든 데이터 세트에 참여하고 쿼리 결과를 보고 또는 Data Science Workspace에 사용하거나 실시간 고객 프로필에 수집하기 위한 새 데이터 세트로 캡처할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 가속 스토어의 속성 기반 액세스 제어 | Data Distiller과 함께 속성 기반 액세스 제어 를 사용하여 가속화된 저장소의 모든 데이터 세트에 대한 액세스 제어를 정의합니다. 사용자가 만들고 가속 스토어에 저장된 사용자 정의 데이터 모델에 대한 액세스를 제어하여 사용자 정의 대시보드를 구현합니다. |

{style="table-layout:auto"}

쿼리 서비스에 대한 자세한 내용은 [쿼리 서비스 개요](../../query-service/home.md).

## Real-Time Customer Data Platform B2B 에디션 {#b2b}

Real-time Customer Data Platform(Real-Time CDP)에 구축된 Real-Time CDP B2B Edition은 비즈니스-비즈니스 서비스 모델로 운영되는 마케터를 위해 특별히 빌드되었습니다. 여러 소스의 데이터를 가져와서 사람 및 계정 프로필에 대한 단일 보기로 결합합니다. 이러한 통합 데이터를 통해 마케터는 특정 대상을 정확하게 타겟팅하고 사용 가능한 모든 채널에서 그러한 대상을 선택할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 버그 수정 | 시스템에서 프로필을 보다 정확하게 표시하기 위해 시스템은 더 이상 총 프로필 수 또는 Real-time Customer Data Platform B2B Edition에 대한 지정 대상 지표에 내부 프로필을 포함하지 않습니다. 오늘부터 총 프로필 수/대응 가능 대상 지표에 1회 감소가 표시될 수 있습니다. 데이터가 지워지지 않은 상태이며 이는 카운트의 변경입니다. 우려사항이 있으면 Adobe 담당자에게 문의하십시오 |

{style="table-layout:auto"}

Real-Time CDP B2B Edition에 대해 자세히 알아보려면 [Real-Time CDP B2B Edition 개요](../../rtcdp/overview.md).

## 세분화 서비스 {#segmentation}

[!DNL Segmentation Service] 고객 기반 내의 마케팅 가능한 사람 그룹을 구분하는 기준을 설명하여 특정 프로필 하위 집합을 정의합니다. 세그먼트는 브랜드와의 고객 상호 작용을 나타내는 레코드 데이터(예: 인구 통계 정보) 또는 시계열 이벤트를 기반으로 할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 프로필 지표 | 프로필 지표를 더 정확하게 표현하기 위해 멤버십 분류 및 이탈 지표가 결합되고 이제 24시간 동안 계산됩니다. 자세한 내용은 [세그멘테이션 UI 안내서](../../segmentation/ui/overview.md#browse) |
| 세그먼트 멤버십 맵 | 2023년 4월 5일 2월의 이전 발표에 대한 후속 발표로서, `Existing` 세그먼트 멤버십 라이프사이클에서 중복을 제거하기 위해 상태는 세그먼트 멤버십 맵에서 더 이상 사용되지 않습니다. 이 변경 후 세그먼트에 자격을 갖춘 프로필은 로 표시됩니다 `Realized` 그리고 자격이 없는 프로필은 `Exited`.<br/><br/> 이 변경 사항은 [엔터프라이즈 대상](../../destinations/destination-types.md#streaming-profile-export) (Amazon Kinesis, Azure 이벤트 허브, HTTP API) 및 은(는) `Existing` 상태. 이러한 경우 다운스트림 통합을 검토하십시오. 특정 시간 이후에 새로 자격을 갖춘 프로필을 식별하는 데 관심이 있는 경우 `Realized` 상태 및 `lastQualificationTime` 세그먼트 멤버십 맵에서 공유할 수 있습니다. 자세한 내용은 Adobe 담당자에게 문의하십시오. |

{style="table-layout:auto"}

자세한 내용은 [!DNL Segmentation Service]를 보려면 [세그먼테이션 개요](../../segmentation/home.md).

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 베타 가용성 [!DNL Chatlio] | 다음 [!DNL Chatlio] 이제 베타 버전으로 소스를 사용할 수 있습니다. 를 사용하십시오 [!DNL Chatlio] 스트리밍할 소스 [!DNL Chatlio] 이벤트 데이터를 Experience Platform에 추가합니다. 자세한 내용은 [[!DNL Chatlio] 개요](../../sources/connectors/marketing-automation/chatlio-webhook.md). |
| 베타 가용성 [!DNL Customer.io] | 다음 [!DNL Customer.io] 이제 베타 버전으로 소스를 사용할 수 있습니다. 를 사용하십시오 [!DNL Customer.io] Experience Platform으로 고객 이벤트 데이터를 스트리밍할 소스입니다. 자세한 내용은 [[!DNL Customer.io] 개요](../../sources/connectors/marketing-automation/customerio-webhook.md). |
| 베타 가용성 [!DNL Pendo] | 다음 [!DNL Pendo] 이제 베타 버전으로 소스를 사용할 수 있습니다. 를 사용하십시오 [!DNL Pendo] 제품 분석 데이터를 Experience Platform으로 스트리밍할 소스입니다. 자세한 내용은 [[!DNL Pendo] 개요](../../sources/connectors/analytics/pendo-webhook.md). |
| 초안 데이터 흐름 지원 | 이제 Flow Service API를 사용하여 데이터 흐름을 초안 상태로 설정할 수 있습니다. 초안 데이터 흐름은 나중에 새로운 정보를 사용하여 업데이트 및 게시할 수 있습니다. 자세한 내용은 다음 안내서를 참조하십시오. [소스 데이터 흐름을 초안으로 설정](../../sources/tutorials/api/draft.md). |

{style="table-layout:auto"}

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).
