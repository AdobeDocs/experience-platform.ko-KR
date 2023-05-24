---
title: Adobe Experience Platform 릴리스 노트 2023년 3월
description: Adobe Experience Platform의 2023년 3월 릴리스 정보.
exl-id: 3f4d764a-77cd-4e4a-ae11-e97a23006a53
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '2206'
ht-degree: 4%

---

# Adobe Experience Platform 릴리스 노트

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

Adobe Experience Platform은 일별 스냅샷 중에 캡처한 대로 조직 데이터에 대한 중요한 통찰력을 볼 수 있는 여러 대시보드를 제공합니다.

**새 기능 또는 업데이트된 기능** {#dashboards-new-updated-features}

| 기능 | 설명 |
| --- | --- |
| 사용자 정의 대시보드 | 이제 다음을 수행할 수 있습니다. **샘플 속성 값** 사용자 정의 대시보드 위젯 작성기에서 위젯에 속성을 추가하기 전입니다. 위젯을 만들 때 개별 속성에 대해 해당 속성 열의 몇 가지 샘플 값을 사용할 수 있습니다.<br>이제 다음을 수행할 수 있습니다. **x축과 Y축 교체** 축 교체 버튼이 있는 위젯에서 를 참조하십시오. 이렇게 하면 시간이 절약되고 위젯에 속성을 추가할 때 보다 인체공학적 경험을 제공할 수 있습니다. 이렇게 하면 속성 패널에서 두 속성을 모두 다시 찾아야 합니다.<br> 이제 다음을 수행할 수 있습니다. **범례의 위치 및 제목 변경** 내 위젯에 매핑됩니다. 위젯에 범례가 있으면 차트 주위의 어디에나 해당 범례를 재배치하고 범례 제목의 이름을 변경할 수 있습니다. 축 레이블과 위젯 제목을 사용할 수 있습니다. |

{style="table-layout:auto"}

액세스 권한을 부여하고 사용자 정의 위젯을 만드는 방법을 포함하여 대시보드에 대한 자세한 내용은 [대시보드 개요](../../dashboards/home.md).

## 데이터 수집 {#data-collection}

Adobe Experience Platform은 클라이언트측 고객 경험 데이터를 수집하여 Adobe Experience Platform Edge Network로 전송하여 Adobe 또는 비 Adobe 대상으로 보강, 변환 및 배포할 수 있는 기술 제품군을 제공합니다.

**새 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 신규 메타 전환 API(베타)에 대한 빠른 시작 워크플로우 | 데이터 수집 홈 화면의 &quot;시작하기&quot;에서 새 빠른 시작 워크플로우에 액세스합니다! 다음 [메타 전환 API에 대한 빠른 시작 워크플로우](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start) 몇 가지 간단한 단계만으로 광고 전환을 위해 서버측에서 메타로 이벤트 데이터를 빠르게 수집하고 전달할 수 있습니다. |
| 모바일 SDK용 새로운 빠른 시작 워크플로우(베타) | 데이터 수집 홈 화면의 &quot;시작하기&quot;에서 새 빠른 시작 워크플로우에 액세스합니다! 다음 [모바일 SDK용 빠른 시작 워크플로우](https://developer.adobe.com/client-sdks/documentation/) 를 사용하면 몇 가지 간단한 단계만으로 Mobile SDK를 신속하게 구현하고 기본 모바일 이벤트를 확인할 수 있습니다. |
| [!DNL Braze] 이벤트 전달 확장 | 다음 [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 이벤트 전달 확장을 사용하면 Adobe Experience Platform Edge Network에 캡처된 데이터를 활용하여 로 전송할 수 있습니다. [!DNL Braze] 를 사용하는 서버측 이벤트 형식으로 [!DNL Braze] 사용자 추적 API. |
| [!DNL Epsilon] 이벤트 전달 확장 | 다음 [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/overview.html) 확장을 사용하면 이벤트 전달을 활용하여 Adobe Experience Platform Edge Network에서 이벤트 정보를 캡처하여 로 전송할 수 있습니다. [!DNL Epsilon] 사용 [!DNL Epsilon] 이벤트 API. |
| [!DNL Mixpanel] 이벤트 전달 확장 | 다음 [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 확장을 사용하면 이벤트 전달을 활용하여 Adobe Experience Platform Edge Network에서 이벤트 정보를 캡처하고 이벤트 추적 API를 사용하여 Mixpanel로 전송할 수 있습니다. |

{style="table-layout:auto"}

## 데이터 준비 {#data-prep}

데이터 준비를 통해 데이터 엔지니어는 데이터를 XDM(Experience Data Model)에 매핑하고, 변환하고, 유효성을 확인할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| Adobe Analytics 데이터 필터링의 일반 가용성 | 이제 실시간 고객 프로필로 수집하기 전에 데이터 준비 기능을 사용하여 규칙 및 조건을 적용하여 Analytics 데이터를 필터링할 수 있습니다. 자세한 내용은 의 안내서를 참조하십시오. [프로필 수집을 위한 Analytics 데이터 필터링](../../sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-profile). |
| URL 문자열 인코딩 및 디코딩에 대한 새로운 함수 | <ul><li>다음 `get_url_encoded` 함수는 URL을 입력으로 취하여 특수 문자를 ASCII 문자로 바꾸거나 인코딩합니다.</li><li>다음 `get_url_decoded` 함수는 URL을 입력으로 가져오고 ASCII 문자를 특수 문자로 디코딩합니다.</li></ul> 자세한 내용은 [데이터 준비 기능 안내서](../../data-prep/functions.md). 예약된 문자와 그에 해당하는 인코딩된 문자의 전체 목록은 의 안내서를 참조하십시오 [특수 문자](../../data-prep/functions.md#special-characters). |

데이터 준비에 대한 자세한 내용은 [데이터 준비 개요](../../data-prep/home.md).

## 대상 {#destinations}

[!DNL Destinations] 는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 빌드된 통합입니다. 대상을 사용하여 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 다양한 사용 사례에 대해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새 대상** {#new-destinations}

| 대상 | 설명 |
| ----------- | ----------- |
| [[!DNL Adobe Commerce] 연결 GA](../../destinations/catalog/personalization/adobe-commerce.md) | 다음 [!DNL Adobe Commerce] 대상 커넥터(이제 일반적으로 사용 가능)를 사용하면 하나 이상의 Real-Time CDP 대상을 선택하여 [!DNL Adobe Commerce] 은(는) 쇼핑객을 위한 동적 개인화된 경험을 제공할 계정입니다. |
| [[!DNL Snap Inc] 연결 GA](../../destinations/catalog/advertising/snap-inc.md) | 다음 [!DNL Snap Inc] 대상 커넥터(이제 일반적으로 사용 가능)를 사용하면 마케터가 Experience Platform에서 만든 사용자 세그먼트를 [!DNL Snapchat Ads] 광고를 타겟팅하는 데 사용합니다. |
| [(API) Oracle Eloqua 연결](../../destinations/catalog/email-marketing/oracle-eloqua-api.md) | API 기반 연결을 사용하여 다음을 수행할 수 있습니다 [!DNL Oracle Eloqua] 의 잠재 고객을 위해 개인화된 고객 경험을 제공하면서 캠페인을 계획 및 실행하려면 [!DNL Oracle Eloqua]. |
| [(베타) [!DNL Amazon Ads] 연결](../../destinations/catalog/advertising/amazon-ads.md) | 다음 [!DNL Amazon Ads] Adobe Experience Platform과의 통합을 통해 [!DNL Amazon Ads] 제품(다음의 것을 포함한다) [!DNL Amazon DSP (ADSP)]. 사용 [!DNL Amazon Ads] 대상 Adobe Experience Platform에서 사용자는 의 타겟팅 및 활성화를 위해 광고주 대상을 정의할 수 있습니다 [!DNL Amazon DSP]. |
| [[!DNL Marketo Measure Ultimate] 연결](../../destinations/catalog/adobe/marketo-measure-ultimate.md) | [!DNL Marketo Measure] (이전 Bizible)은 마케터에게 매출을 증대시키고 투자 수익률을 극대화하는 데 가장 효과적인 마케팅 활동을 파악하는 데 도움이 됩니다. 대상은 Adobe Experience Platform에서 (으)로 B2B(기업 간) 데이터 흐름을 활성화합니다. [!DNL Marketo Measure]. 이 카드는 다음 대상에서만 사용할 수 있습니다. [!DNL Marketo Measure Ultimate] 고객. |
| [TikTok 연결](../../destinations/catalog/social/tiktok.md) | 광고 캠페인으로 타깃팅할 데이터를 사용하여 TikTok에서 사용자 지정 대상을 작성합니다. |
| [Zendesk 연결](../../destinations/catalog/crm/zendesk.md) | 이 대상을 사용하여 세그먼트 내에서 연락처로 ID를 만들고 업데이트합니다. [!DNL Zendesk]. |

{style="table-layout:auto"}

**새로운 기능 또는 업데이트된 기능** {#destinations-new-updated-functionality}

| 기능 | 설명 |
| ----------- | ----------- |
| 대상에 대한 새로운 액세스 제어 권한: [[!DNL Activate Segments without Mapping]](../../access-control/home.md#permissions) | 새 권한을 통해 사용자는 세그먼트를 표시하지 않고 기존 대상에 활성화할 수 있습니다. [매핑 단계](../../destinations/ui/activate-batch-profile-destinations.md#mapping). 사용자는 활성화 워크플로에서 세그먼트를 추가하거나 제거할 수 있지만 매핑된 속성 또는 ID를 추가하거나 제거할 수 없습니다. |

{style="table-layout:auto"}

**수정 사항 및 개선 사항** {#destinations-fixes-and-enhancements}

실시간 CDP의 파일 기반 대상에서 PGP/GPG 암호화에 대한 버그 수정을 릴리스할 예정입니다. 이러한 변경 사항으로 현재 암호화를 사용하는 기존 파일 기반 대상은 이전과 다른 확장자의 파일 이름을 생성합니다.

- 암호화를 사용할 때의 현재 확장: `filename.csv`
- 암호화를 사용할 때의 향후 확장: `filename.csv.gpg`

대상에 대한 일반적인 정보는 [대상 개요](../../destinations/home.md).

## 경험 데이터 모델(XDM) {#xdm}

XDM은 Adobe Experience Platform으로 가져온 데이터에 대한 일반적인 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수함으로써 모든 고객 경험 데이터를 일반적인 표현에 통합하여 보다 빠르고 통합적인 방식으로 통찰력을 제공할 수 있습니다. 고객 작업에서 중요한 통찰력을 얻고, 세그먼트를 통해 고객 대상을 정의하고, 개인화 목적으로 고객 속성을 사용할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| CSV에서 스키마 추천으로 | 이제 로컬 파일을 업로드하여 수동으로 스키마를 생성할 필요가 없는 머신 러닝 생성 스키마를 생성할 수 있습니다. 다음에서 [!UICONTROL 소스] 작업 공간, 샘플 CSV 파일 업로드 및 머신 러닝 알고리즘 Adobe은 대상 필드를 기반으로 스키마를 제안합니다. 자세한 내용은 [설명서](../../ingestion/tutorials/map-csv/recommendations.md)를 참조하십시오.&quot; |

{style="table-layout:auto"}

**새로운 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 클래스 | [[!UICONTROL 오퍼 항목]](https://github.com/adobe/xdm/pull/1678/files) | 오퍼를 나타내는 클래스입니다. |
| 클래스 | [[!UICONTROL 결정 항목]](https://github.com/adobe/xdm/pull/1678/files) | 의사 결정 대상이 될 수 있는 항목입니다. 의사 결정 프로세스의 출력은 하나 이상의 의사 결정 항목입니다. |
| 클래스 | [[!UICONTROL 미디어 세션 서버 시간 초과]](https://github.com/adobe/xdm/pull/1676/files) | 마지막으로 알려진 사용자 인터랙션과 세션 종료 시점 사이에 경과한 시간(초)을 나타냅니다. |
| 필드 그룹 | [[!UICONTROL XDM 프로필 계산된 속성]](https://github.com/adobe/xdm/pull/1686/files) | 이렇게 하면 내부 Adobe 서비스의 계산된 속성이 수신 고객 데이터에 추가됩니다. 고객은 이 데이터를 사용하여 데이터를 수집해서는 안 됩니다. |
| 데이터 형식 | [[!UICONTROL 환불 항목]](https://github.com/adobe/xdm/pull/1685/files) | 환불이 주문과 연계되어 있는지 여부를 보여 주고 환불 유형, 금액 및 관련 통화를 정의합니다. |
| 데이터 형식 | [[!UICONTROL 범주 데이터]](https://github.com/adobe/xdm/pull/1677/files) | 이 새 데이터 유형은 제품의 범주를 나타냅니다. |
| 스키마 | [[!UICONTROL Adobe Target 분류 필드]](https://github.com/adobe/xdm/pull/1682/files) | Target 분류 데이터 세트에 대한 새 XDM 스키마를 만들었습니다. 여기에는 Target 활동 및 경험을 분류하는 메타데이터 필드 세트가 포함되어 있습니다. |

{style="table-layout:auto"}

**업데이트된 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 필드 그룹 | [[!UICONTROL 콘텐츠 구성 요소 세부 정보]](https://github.com/adobe/xdm/pull/1674/files) | `uri-reference` 이(가)에서 제거되었습니다. [!UICONTROL 콘텐츠 구성 요소 세부 정보] |
| 필드 그룹 | [[!UICONTROL AJO 엔티티 태그]](https://github.com/adobe/xdm/pull/1672/files) | 에 AJO 엔티티 태그가 추가되었습니다. [!UICONTROL AJO 엔티티 필드]여정 또는 캠페인에 해당하는 |
| 필드 그룹 | (여러 개) | 에 대한 여러 필드 추가됨 [[!UICONTROL Journey Orchestration 단계 이벤트 공통 필드]](https://github.com/adobe/xdm/pull/1671/files) |
| 필드 그룹 | (여러 개) | [에 대한 여러 XDM 이벤트 유형을 추가했습니다. [!UICONTROL 미디어 보고]](https://github.com/adobe/xdm/pull/1670/files). |
| 필드 그룹 | [!UICONTROL Workfront 변경 이벤트] | 다음 `Full Record` 및 `Accessor Employee Ids` 필드 그룹이 추가되었습니다. |
| 데이터 형식 | [[!UICONTROL 제품 목록 항목]](https://github.com/adobe/xdm/pull/1685/files) | 다음 [!UICONTROL 환불 금액] 항목이 있는 경우 해당 항목에 대해 환급된 금액을 표시하기 위해 가 추가되었습니다. |
| 데이터 형식 | [[!UICONTROL 주문 ]](https://github.com/adobe/xdm/pull/1685/files) | [!UICONTROL 환불 목록] 이(가) 이 주문에 대한 환불 목록에 추가되었습니다. |
| 데이터 형식 | [[!UICONTROL 제품 목록 항목 ]](https://github.com/adobe/xdm/pull/1677/files) | 이 제품의 범주 데이터 목록에 제품 범주가 추가되었습니다. |
| 데이터 유형 | [!UICONTROL 세션 세부 정보] | 을(를) 추가함 `pev3` 문자열 필드 [보고에 사용된 미디어 스트림 유형을 나타냅니다.](https://github.com/adobe/xdm/pull/1676/files). 이(가) 또한 을(를) 추가함 `pccr` 속성은 리디렉션이 발생했는지 여부를 나타냅니다. |
| 데이터 유형 | [!UICONTROL 구매요청 목록] | 다음을 제공합니다. [구매요청 목록 속성](https://github.com/adobe/xdm/pull/1675/files). 여기에는 이름, ID 및 설명이 포함됩니다. |
| 데이터 유형 | [!UICONTROL Commerce] | 다음 [상거래 데이터 유형이 업데이트되었습니다.](https://github.com/adobe/xdm/pull/1675/files) 포함할 항목 `requisitionListOpens`, `requisitionListAdds`, `requisitionListRemovals`, 및 `requisitionList`. |

{style="table-layout:auto"}

플랫폼의 XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md).

## 쿼리 서비스 {#query-service}

쿼리 서비스를 사용하면 표준 SQL을 사용하여 Adobe Experience Platform에서 데이터를 쿼리할 수 있습니다 [!DNL Data Lake]. 데이터 레이크에서 모든 데이터 세트에 참여하고 쿼리 결과를 보고 또는 Data Science Workspace에 사용하거나 실시간 고객 프로필에 수집하기 위한 새 데이터 세트로 캡처할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 가속화된 저장소에서 속성 기반 액세스 제어 | 속성 기반 액세스 제어를 Data Distiller과 함께 사용하여 가속화된 저장소의 모든 데이터 세트에 대한 액세스 제어를 정의합니다. 이렇게 하면 사용자가 만들고 가속화된 저장소에 저장된 사용자 지정 데이터 모델에 대한 액세스를 제어하여 사용자 지정 대시보드를 사용할 수 있습니다. |

{style="table-layout:auto"}

쿼리 서비스에 대한 자세한 내용은 [쿼리 서비스 개요](../../query-service/home.md).

## Real-Time Customer Data Platform B2B 에디션 {#b2b}

Real-time Customer Data Platform(Real-Time CDP)을 기반으로 구축된 Real-Time CDP B2B 에디션은 B2B 서비스 모델을 운영하는 마케터용으로 특별히 빌드되었습니다. 여러 소스에서 데이터를 취합하여 사람 및 계정 프로필에 대한 단일 보기에 결합합니다. 이 통합 데이터를 통해 마케터는 특정 대상을 정확하게 타겟팅하고 사용 가능한 모든 채널에서 해당 대상을 참여시킬 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 버그 수정 | 시스템에서 프로필을 보다 정확하게 표현하기 위해 총 프로필 수에 내부 프로필 또는 Real-time Customer Data Platform B2B 에디션의 대응 가능 대상 지표가 더 이상 포함되지 않습니다. 오늘부터 총 프로필 수/대응 가능 대상 지표가 한 번 감소할 수 있습니다. 데이터가 하나도 지워지지 않았습니다. 이는 단순히 카운트에 대한 변경입니다. 우려되는 사항이 있으면 Adobe 담당자에게 문의하십시오 |

{style="table-layout:auto"}

Real-Time CDP B2B 에디션에 대해 자세히 알아보려면 [Real-Time CDP B2B 에디션 개요](../../rtcdp/overview.md).

## 세분화 서비스 {#segmentation}

[!DNL Segmentation Service] 은 고객 기반 내에서 마케팅 가능한 사용자 그룹을 구분하는 기준을 설명하여 프로필의 특정 하위 집합을 정의합니다. 세그먼트는 브랜드와의 고객 상호 작용을 나타내는 레코드 데이터(예: 인구 통계학적 정보) 또는 시계열 이벤트를 기반으로 할 수 있습니다.

**새 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 프로필 지표 | 프로필 지표를 더 정확하게 표현하기 위해 멤버십 분류 및 이탈 지표가 결합되고 있으며 이제 24시간 동안 계산됩니다. 자세한 내용은 [세그멘테이션 UI 안내서](../../segmentation/ui/overview.md#browse) |

{style="table-layout:auto"}

에 대한 자세한 내용 [!DNL Segmentation Service], 다음을 참조하십시오. [세그먼테이션 개요](../../segmentation/home.md).

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 해당 데이터를 구조화하고, 레이블을 지정하고, 개선할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 서드파티 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 의 베타 가용성 [!DNL Chatlio] | 다음 [!DNL Chatlio] 이제 베타로 소스를 사용할 수 있습니다. 사용 [!DNL Chatlio] 스트리밍할 소스 [!DNL Chatlio] Experience Platform에 대한 이벤트 데이터. 자세한 내용은 [[!DNL Chatlio] 개요](../../sources/connectors/marketing-automation/chatlio-webhook.md). |
| 의 베타 가용성 [!DNL Customer.io] | 다음 [!DNL Customer.io] 이제 베타로 소스를 사용할 수 있습니다. 사용 [!DNL Customer.io] 소스 - 고객 이벤트 데이터를 Experience Platform으로 스트리밍합니다. 자세한 내용은 [[!DNL Customer.io] 개요](../../sources/connectors/marketing-automation/customerio-webhook.md). |
| 의 베타 가용성 [!DNL Pendo] | 다음 [!DNL Pendo] 이제 베타로 소스를 사용할 수 있습니다. 사용 [!DNL Pendo] 소스: 제품 분석 데이터를 Experience Platform으로 스트리밍합니다. 자세한 내용은 [[!DNL Pendo] 개요](../../sources/connectors/analytics/pendo-webhook.md). |
| 초안 데이터 흐름 지원 | 이제 흐름 서비스 API를 사용하여 데이터 흐름을 초안 상태로 설정할 수 있습니다. 초안 데이터 흐름은 나중에 새로운 정보로 업데이트하고 게시할 수 있습니다. 자세한 내용은 의 안내서를 참조하십시오. [소스 데이터 흐름을 초안으로 설정](../../sources/tutorials/api/draft.md). |

{style="table-layout:auto"}

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).
