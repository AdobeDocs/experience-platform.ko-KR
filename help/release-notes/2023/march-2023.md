---
title: Adobe Experience Platform 릴리스 정보 2023년 3월
description: Adobe Experience Platform의 2023년 3월 릴리스 정보입니다.
exl-id: 3f4d764a-77cd-4e4a-ae11-e97a23006a53
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2081'
ht-degree: 97%

---

# Adobe Experience Platform 릴리스 정보

**릴리스 일자: 2023년 3월 29일**

Adobe Experience Platform의 기존 기능 업데이트:

- [대시보드](#dashboards)
- [데이터 수집](#data-collection)
- [데이터 준비](#data-prep)
- [대상](#destinations)
- [경험 데이터 모델](#xdm)
- [쿼리 서비스](#query-service)
- [Real-Time Customer Data Platform B2B 에디션](#b2b)
- [Segmentation Service](#segmentation)
- [소스](#sources)

## 대시보드 {#dashboards}

Adobe Experience Platform은 일일 스냅샷 중에 캡처된 조직 데이터에 대한 중요한 인사이트를 볼 수 있는 여러 대시보드를 제공합니다.

**새로운 기능 또는 업데이트된 기능** {#dashboards-new-updated-features}

| 기능 | 설명 |
| --- | --- |
| 사용자 정의 대시보드 | 이제 사용자 정의된 대시보드 위젯 작성기에서 위젯에 속성을 추가하기 전에 **속성 값을 샘플링**&#x200B;할 수 있습니다. 위젯을 만들 때 해당 속성 열의 몇 가지 샘플 값을 개별 속성에 사용할 수 있습니다.<br>이제 축 교체 버튼을 사용하여 위젯에서 **X축과 Y축을 교체**&#x200B;할 수 있습니다. 이를 통해 위젯에 속성을 추가할 때 시간을 단축하고 보다 인체 공학적인 경험을 제공합니다. 이렇게 하면 속성 패널에서 두 가지 속성을 다시 찾아야 하는 필요성이 줄어듭니다.<br> 이제 위젯 내에서 **범례의 위치와 제목을 변경**&#x200B;할 수 있습니다. 위젯에 범례가 표시되면 해당 범례를 차트 주변의 아무 곳에나 재배치할 수 있으며, 축 레이블 및 위젯 제목 등과 같이 범례 제목의 이름을 변경할 수도 있습니다. |

{style="table-layout:auto"}

액세스 권한을 부여하고 사용자 정의 위젯을 만드는 방법을 포함해 대시보드에 대한 자세한 내용은 [대시보드 개요](../../dashboards/home.md)를 읽어 보십시오.

## 데이터 수집 {#data-collection}

Adobe Experience Platform은 클라이언트측 고객 경험 데이터를 수집하여 Adobe 또는 비 Adobe 대상으로 보강, 변환 및 배포가 가능한 Adobe Experience Platform Edge Network로 보낼 수 있는 기술 제품군을 제공합니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 메타 전환 API에 대한 새로운 빠른 시작 워크플로우(Beta) | 데이터 수집 홈 화면의 “시작하기” 아래에 있는 새로운 빠른 시작 워크플로에 액세스할 수 있습니다! 고객은 [Meta Conversions API를 위한 빠른 시작 워크플로](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=ko#quick-start)를 사용하여 이벤트 데이터를 신속하게 수집하여 단 몇 번의 간단한 단계로 광고 전환을 위해 서버측에서 Meta로 전달할 수 있습니다. |
| Mobile SDK(Beta)용 새로운 빠른 시작 워크플로 | 데이터 수집 홈 화면의 “시작하기” 아래에 있는 새로운 빠른 시작 워크플로에 액세스할 수 있습니다! [Mobile SDK를 위한 새로운 빠른 시작 워크플로](https://developer.adobe.com/client-sdks/documentation/)를 사용하여 단 몇 번의 간단한 단계로 Mobile SDK를 신속하게 구현하고 기본적인 모바일 이벤트를 확인할 수 있습니다. |
| [!DNL Braze] 이벤트 전달 확장 기능 | [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=ko) 이벤트 전달 확장 기능을 사용하면 Adobe Experience Platform Edge Network에서 캡처된 데이터를 활용하여 [!DNL Braze] User Track API를 통해 서버측 이벤트의 형태로 [!DNL Braze]로 전송할 수 있습니다 |
| [!DNL Epsilon] 이벤트 전달 확장 기능 | [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/overview.html?lang=ko) 확장 기능을 사용하면 이벤트 전달을 통해 Adobe Experience Platform Edge Network의 이벤트 정보를 캡처하고 [!DNL Epsilon] Event API를 통해 [!DNL Epsilon]로 전송할 수 있습니다 |
| [!DNL Mixpanel] 이벤트 전달 확장 기능 | [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=ko) 확장 기능을 사용하면 이벤트 전달을 통해 Adobe Experience Platform Edge Network의 이벤트 정보를 캡처하고 Track Event API를 통해 Mixpanel로 전송할 수 있습니다 |

{style="table-layout:auto"}

## 데이터 준비 {#data-prep}

데이터 준비를 사용하면 데이터 엔지니어가 XDM(Experience Data Model)과의 데이터를 매핑, 변환 및 확인할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| Adobe Analytics 데이터에 대한 필터링의 일반 가용성 | 이제 데이터 준비 기능을 사용하여 실시간 고객 프로필로 수집하기 전에 규칙과 조건을 적용하여 분석 데이터를 필터링할 수 있습니다. 자세한 내용은 [프로필 수집을 위한 분석 데이터 필터링](../../sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-profile)에 대한 안내서를 참조하십시오. |
| URL 문자열 인코딩 및 디코딩을 위한 새로운 기능 | <ul><li>`get_url_encoded` 함수는 URL을 입력으로 사용하고 특수 문자를 ASCII 문자로 대체하거나 인코딩합니다.</li><li>`get_url_decoded` 함수는 URL을 입력으로 사용하고 ASCII 문자를 특수 문자로 디코딩합니다.</li></ul> 자세한 내용은 [데이터 준비 기능 안내서](../../data-prep/functions.md)를 참조하십시오. 예약된 문자 및 인코딩된 해당 문자의 전체 목록에 대한 내용은 [특수 문자](../../data-prep/functions.md#special-characters)에 관한 안내서를 참조하십시오. |

데이터 준비에 대한 자세한 내용은 [데이터 준비 개요](../../data-prep/home.md)를 참조하십시오.

## 대상 {#destinations}

[!DNL Destinations]는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있는 대상 플랫폼과 사전 설치된 통합입니다. 대상을 사용해 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례를 위해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 대상** {#new-destinations}

| 대상 | 설명 |
| ----------- | ----------- |
| [[!DNL Adobe Commerce] 연결 GA](../../destinations/catalog/personalization/adobe-commerce.md) | [!DNL Adobe Commerce] 대상 커넥터(현재 일반적으로 사용 가능)로 하나 이상의 Real-Time CDP 대상자를 선택하여 [!DNL Adobe Commerce] 계정으로 활성화해서 쇼핑객에게 개인 설정된 동적 경험을 제공할 수 있습니다. |
| [[!DNL Snap Inc] 연결 GA](../../destinations/catalog/advertising/snap-inc.md) | 마케터는 [!DNL Snap Inc] 대상 커넥터(현재 일반적으로 사용 가능)를 사용하여 Experience Platform에서 만든 사용자 세그먼트를 [!DNL Snapchat Ads]로 가져와서 광고 대상으로 사용할 수 있습니다. |
| [(API) Oracle Eloqua 연결](../../destinations/catalog/email-marketing/oracle-eloqua-api.md) | [!DNL Oracle Eloqua]에 대한 API 기반 연결을 사용하여 캠페인을 계획하고 실행하는 동시에 [!DNL Oracle Eloqua]의 잠재 고객을 위한 맞춤형 고객 경험을 제공합니다. |
| [(Beta) [!DNL Amazon Ads] 연결](../../destinations/catalog/advertising/amazon-ads.md) | Adobe Experience Platform과 [!DNL Amazon Ads]를 통합하면 [!DNL Amazon DSP (ADSP)]를 포함한 [!DNL Amazon Ads] 제품에 턴키 통합을 제공합니다. 사용자는 Adobe Experience Platform의 [!DNL Amazon Ads] 대상을 사용하여 [!DNL Amazon DSP]에서 타겟팅 및 활성화를 위한 광고주 대상자를 정의할 수 있습니다. |
| [[!DNL Marketo Measure Ultimate] 연결](../../destinations/catalog/adobe/marketo-measure-ultimate.md) | [!DNL Marketo Measure]&#x200B;(이전의 Bizible)는 마케터에게 매출을 늘리고 기업 투자 수익률을 증대시키는 데 가장 효과적인 마케팅 활동을 파악하는 인사이트를 제공합니다. 대상은 Adobe Experience Platform에서 [!DNL Marketo Measure]로 B2B(Business-to-Business) 데이터 흐름을 활성화합니다. 이 카드는 [!DNL Marketo Measure Ultimate] 고객만 사용할 수 있습니다. |
| [TikTok 연결](../../destinations/catalog/social/tiktok.md) | 광고 캠페인의 타겟팅용 데이터로 TikTok에서 맞춤형 대상자를 구축합니다. |
| [Zendesk 연결](../../destinations/catalog/crm/zendesk.md) | 이 대상을 사용하여 세그먼트에서 [!DNL Zendesk] 내의 연락처로 ID를 만들고 업데이트합니다. |

{style="table-layout:auto"}

**새로운 기능 또는 업데이트된 기능** {#destinations-new-updated-functionality}

| 기능 | 설명 |
| ----------- | ----------- |
| 대상에 대한 새로운 액세스 제어 권한: [[!DNL Activate Segments without Mapping]](../../access-control/home.md#permissions) | 사용자는 새로운 권한을 통해 [매핑 단계](../../destinations/ui/activate-batch-profile-destinations.md#mapping)를 표시하지 않고, 세그먼트를 기존 대상으로 활성화할 수 있습니다. 사용자는 활성화 워크플로에서 세그먼트를 추가 및 제거할 수 있지만, 매핑된 속성 또는 ID를 추가하거나 제거할 수는 없습니다. |

{style="table-layout:auto"}

**수정 사항 및 개선 사항** {#destinations-fixes-and-enhancements}

Real-Time CDP의 파일 기반 대상에서 PGP/GPG 암호화에 대한 버그 수정을 릴리스할 예정입니다. 이 변경 사항으로 현재 암호화를 사용하는 기존의 파일 기반 대상은 이전과 다른 확장자를 가진 파일 이름을 생성합니다.

- 암호화 사용 시 현재 확장자: `filename.csv`
- 암호화 사용 시 향후 확장자: `filename.csv.gpg`

대상에 대한 일반적인 정보는 [대상 개요](../../destinations/home.md)를 참조하십시오.

## 경험 데이터 모델 (XDM) {#xdm}

XDM은 Adobe Experience Platform으로 가져오는 데이터에 대한 공통 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수하여 모든 고객 경험 데이터를 공통된 표현에 통합해 보다 빠르고 통합된 방식으로 인사이트를 제공할 수 있습니다. 고객 조치에서 귀중한 인사이트를 얻고, 세그먼트를 통해 고객 대상자를 정의하고, 개인 설정 목적으로 고객 속성을 사용할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| CSV에서 스키마로 전환 권장 사항 | 이제 로컬 파일을 업로드하여 수동으로 스키마를 만들 필요가 없는 머신 러닝으로 생성된 스키마를 만들 수 있습니다. [!UICONTROL 소스] 작업 영역에서 샘플 CSV 파일을 업로드하면 Adobe 머신 러닝 알고리즘이 대상 필드를 기반으로 스키마를 제안합니다. 자세한 내용은 [설명서](../../ingestion/tutorials/map-csv/recommendations.md)를 참조하십시오. |

{style="table-layout:auto"}

**새로운 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 클래스 | [[!UICONTROL 오퍼 항목]](https://github.com/adobe/xdm/pull/1678/files) | 오퍼를 나타내는 클래스입니다. |
| 클래스 | [[!UICONTROL 결정 항목]](https://github.com/adobe/xdm/pull/1678/files) | 결정 대상이 될 수 있는 항목입니다. 결정 프로세스의 출력은 하나 이상의 결정 항목입니다. |
| 클래스 | [[!UICONTROL 미디어 세션 서버 시간 초과]](https://github.com/adobe/xdm/pull/1676/files) | 마지막으로 알려진 사용자의 상호 작용과 세션이 닫힌 순간 사이에 경과된 시간을 초 단위로 나타냅니다. |
| 필드 그룹 | [[!UICONTROL XDM 프로필 계산된 속성]](https://github.com/adobe/xdm/pull/1686/files) | 이를 통해 내부 Adobe 서비스에서 계산된 속성이 수신 고객 데이터에 추가됩니다. 고객이 데이터를 수집하는 데 사용하면 안 됩니다. |
| 데이터 유형 | [[!UICONTROL 환불 항목]](https://github.com/adobe/xdm/pull/1685/files) | 환불이 주문과 연결되어 있는지 여부를 나타내며 환불 유형, 금액 및 관련 통화를 정의합니다. |
| 데이터 유형 | [[!UICONTROL 카테고리 데이터]](https://github.com/adobe/xdm/pull/1677/files) | 새로운 이 데이터 유형은 제품 카테고리를 나타냅니다. |
| 스키마 | [[!UICONTROL Adobe Target 분류 필드]](https://github.com/adobe/xdm/pull/1682/files) | Target 분류 데이터 세트에 대한 새 XDM 스키마가 생성되었습니다. Target 활동 및 경험을 분류하는 메타데이터 필드 집합이 포함됩니다. |

{style="table-layout:auto"}

**업데이트된 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 필드 그룹 | [[!UICONTROL 콘텐츠 구성 요소 세부 정보]](https://github.com/adobe/xdm/pull/1674/files) | `uri-reference`가 [!UICONTROL 콘텐츠 구성 요소 세부 정보]에서 제거됨 |
| 필드 그룹 | [[!UICONTROL AJO 엔티티 태그]](https://github.com/adobe/xdm/pull/1672/files) | 여정 또는 캠페인에 해당하는 [!UICONTROL AJO 엔티티 필드]에 AJO 엔티티 태그가 추가됨 |
| 필드 그룹 | (다수) | [[!UICONTROL Journey Orchestration 단계 이벤트 공통 필드]](https://github.com/adobe/xdm/pull/1671/files)에 대한 여러 필드가 추가됨 |
| 필드 그룹 | (다수) | [[!UICONTROL 미디어 보고]](https://github.com/adobe/xdm/pull/1670/files)에 대한 여러 XDM 이벤트 유형이 추가되었습니다. |
| 필드 그룹 | [!UICONTROL Workfront 변경 이벤트] | `Full Record` 및 `Accessor Employee Ids` 필드 그룹이 추가되었습니다. |
| 데이터 유형 | [[!UICONTROL 제품 목록 항목]](https://github.com/adobe/xdm/pull/1685/files) | 품목의 환불 금액을 표시하기 위해(해당하는 경우) [!UICONTROL 환불 금액]이 추가되었습니다. |
| 데이터 유형 | [[!UICONTROL 주문 &#x200B;]](https://github.com/adobe/xdm/pull/1685/files) | 이 주문에 대한 환불 목록에 [!UICONTROL 환불 목록]이 추가되었습니다. |
| 데이터 유형 | [[!UICONTROL 제품 목록 항목 &#x200B;]](https://github.com/adobe/xdm/pull/1677/files) | 이 제품의 카테고리 데이터 목록에 제품 카테고리가 추가되었습니다. |
| 데이터 유형 | [!UICONTROL 세션 세부 정보] | [보고에 사용되는 미디어 스트림 유형을 나타내는](https://github.com/adobe/xdm/pull/1676/files) `pev3` 문자열 필드가 추가되었습니다. 또한 `pccr` 속성이 추가되어 리디렉션이 발생했는지 여부를 나타냅니다. |
| 데이터 유형 | [!UICONTROL 요청 목록] | [요청 목록 속성](https://github.com/adobe/xdm/pull/1675/files)을 제공합니다. 여기에는 이름, ID 및 설명이 포함됩니다. |
| 데이터 유형 | [!UICONTROL 상거래] | `requisitionListOpens`, `requisitionListAdds`, `requisitionListRemovals` 및 `requisitionList`를 포함하도록 [상거래 데이터 유형이 업데이트](https://github.com/adobe/xdm/pull/1675/files)되었습니다. |

{style="table-layout:auto"}

Experience Platform의 XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md)를 참조하십시오.

## 쿼리 서비스 {#query-service}

쿼리 서비스를 사용하면 표준 SQL로 Adobe Experience Platform [!DNL Data Lake]에서 데이터를 쿼리할 수 있습니다. 데이터 레이크의 데이터 세트에 참여하고 쿼리 결과를 보고 또는 Data Science Workspace에 사용하거나 실시간 고객 프로필에 수집하기 위한 새 데이터 세트로 캡처할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 가속화된 스토어에 대한 속성 기반의 액세스 제어 | Data Distiller와 함께 속성 기반의 액세스 제어를 사용하여 가속화된 스토어의 모든 데이터 세트에 대한 액세스 제어를 정의합니다. 사용자가 생성하고 가속화된 스토어에 저장되어 사용자 정의 대시보드를 구동하는 사용자 정의 데이터 모델에 대한 액세스를 제어합니다. |

{style="table-layout:auto"}

쿼리 서비스에 대한 자세한 내용은 [쿼리 서비스 개요](../../query-service/home.md)를 참조하십시오.

## Real-Time Customer Data Platform B2B 에디션 {#b2b}

Real-Time Customer Data Platform(Real-Time CDP)을 기반으로 구축된 Real-Time CDP B2B 에디션은 business-to-business 서비스 모델에서 운영하는 마케터를 위해 특별히 설계되었습니다. 여러 소스의 데이터를 함께 가져와서 사람 및 계정 프로필의 단일 보기로 결합합니다. 마케터는 이 통합 데이터를 통해 특정 대상자를 정확하게 타겟팅하고 사용 가능한 모든 채널에서 해당 대상자를 참여시킬 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 버그 수정 | 시스템에서 프로필을 보다 정확하게 표현하기 위해 시스템은 더 이상 총 프로필 수 또는 Real-Time Customer Data Platform B2B 에디션의 지정 가능한 대상자 지표에 내부 프로필을 포함하지 않습니다. 오늘부터 총 프로필 수/지정 가능한 대상자 지표가 일회성으로 감소할 수 있습니다. 사용자 데이터는 지워지지 않았으며, 이는 단순히 수가 변경된 것입니다. 우려 사항이 있으면 Adobe 경영진에 문의하십시오. |

{style="table-layout:auto"}

Real-Time CDP B2B 에디션에 대한 자세한 내용은 [Real-Time CDP B2B 에디션 개요](../../rtcdp/overview.md)를 참조하십시오.

## Segmentation Service {#segmentation}

[!DNL Segmentation Service]는 고객 기반 내에서 마케팅 가능한 사용자 그룹을 구분하는 기준을 설명하여 프로필의 특정 하위 집합을 정의합니다. 세그먼트는 기록 데이터(예: 인구 통계 정보) 또는 고객과 브랜드의 상호 작용을 나타내는 시계열 이벤트를 기반으로 할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ------- | ----------- |
| 프로필 지표 | 프로필 지표를 보다 정확하게 나타내기 위해 멤버십 분류 및 이탈 지표가 결합되어 24시간 동안 계산됩니다. 자세한 내용은 [세분화 UI 안내서](../../segmentation/ui/overview.md#browse)를 참조하십시오. |

{style="table-layout:auto"}

[!DNL Segmentation Service]에 대한 자세한 내용은 [세분화 개요](../../segmentation/home.md)를 참조하십시오.

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집할 수 있으며 Experience Platform 서비스를 사용하여 해당 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 서드파티 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스에 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| [!DNL Chatlio]의 Beta 가용성 | 이제 [!DNL Chatlio] 소스는 베타 버전으로 제공됩니다. [!DNL Chatlio] 소스를 사용하여 사용자의 [!DNL Chatlio] 이벤트 데이터를 Experience Platform으로 스트리밍합니다. 자세한 내용은 [[!DNL Chatlio] 개요](../../sources/connectors/marketing-automation/chatlio-webhook.md)를 참조하십시오. |
| [!DNL Customer.io]의 Beta 가용성 | 이제 [!DNL Customer.io] 소스는 베타 버전으로 제공됩니다. [!DNL Customer.io] 소스를 사용하여 사용자의 고객 이벤트 데이터를 Experience Platform으로 스트리밍합니다. 자세한 내용은 [[!DNL Customer.io] 개요](../../sources/connectors/marketing-automation/customerio-webhook.md)를 참조하십시오. |
| [!DNL Pendo]의 Beta 가용성 | 이제 [!DNL Pendo] 소스는 베타 버전으로 제공됩니다. [!DNL Pendo] 소스를 사용하여 사용자의 제품 분석 데이터를 Experience Platform으로 스트리밍합니다. 자세한 내용은 [[!DNL Pendo] 개요](../../sources/connectors/analytics/pendo-webhook.md)를 참조하십시오. |
| 초안 데이터 흐름 지원 | 이제 Flow Service API를 사용하여 데이터 흐름을 초안 상태로 설정할 수 있습니다. 초안 데이터 흐름은 나중에 업데이트하고 새 정보로 게시할 수 있습니다. 자세한 내용은 [소스 데이터 흐름을 초안으로 설정](../../sources/tutorials/api/draft.md)에 관한 안내서를 참조하십시오. |

{style="table-layout:auto"}

소스에 대해 자세히 알아보려면 [소스 개요 ](../../sources/home.md)를 참조하십시오.
