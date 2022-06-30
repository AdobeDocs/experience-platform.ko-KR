---
title: Adobe Experience Platform 릴리스 정보
description: Adobe Experience Platform에 대한 최신 릴리스 노트입니다.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: def32d9667c4630de760d228c88676eb9d5a6de4
workflow-type: tm+mt
source-wordcount: '1786'
ht-degree: 4%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2022년 6월 22일**

Adobe Experience Platform의 기존 기능 업데이트:

- [[!DNL Data Collection]](#data-collection)
- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [XDM(경험 데이터 모델)](#xdm)
- [쿼리 서비스](#query-service)
- [소스](#sources)

## 데이터 수집 {#data-collection}

Platform은 클라이언트측 고객 경험 데이터를 수집하고 Adobe Experience Platform Edge Network로 전송하여 Adobe 또는 비Adobe 대상으로 보강, 변환 및 배포할 수 있는 기술 세트를 제공합니다.

**새로운 기능**

| 기능 | 설명 |
| --- | --- |
| [데이터 세트에 대한 액세스 유형 구성](../../edge/datastreams/overview.md#create) | 이제 새 데이터 스트림을 만들 때 Edge Network에서 허용할 요청 유형을 선택할 수 있습니다. <ul><li>**[!UICONTROL 혼합 인증]**: 이 옵션을 선택하면 Edge Network에서 인증된 요청과 인증되지 않은 요청을 모두 허용합니다. 웹 SDK를 사용할 계획이나 [Mobile SDK](https://aep-sdks.gitbook.io/docs/)와 함께 [서버 API](../../server-api/overview.md). </li><li>**[!UICONTROL 인증만]**: 이 옵션을 선택하면 에지 네트워크에서 인증된 요청만 허용합니다. 서버 API만 사용하고 인증되지 않은 요청이 에 의해 처리되지 않도록 하려면 이 옵션을 선택합니다 [!DNL Edge Network]. </li></ul> |
| [프로젝트 렌더링](../../edge/personalization/rendering-personalization-content.md#applypropositions) 지표를 증가시키지 않고 단일 페이지 애플리케이션에서 를 생성합니다. | 새로 추가된 `applyPropositions` 명령 를 사용하면 [!DNL Target] 단일 페이지 애플리케이션에 [!DNL Analytics] 및 [!DNL Target] 지표 를 참조하십시오. 따라서 보고 정확도가 높아집니다. |
| [모바일-투-웹 및 도메인 간 ID 공유](../../edge/identity/id-sharing.md) | 이제 Adobe Experience Platform Web SDK는 방문자 ID 공유 기능을 지원하므로 모바일 앱과 모바일 웹 콘텐츠 간, 도메인 간에 보다 정확하게 개인화된 경험을 제공할 수 있습니다. |

Platform의 데이터 수집에 대한 자세한 내용은 [데이터 수집 개요](../../collection/home.md).

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace는 기계 학습 및 인공 지능을 사용하여 데이터를 통해 통찰력을 제공합니다. Adobe Experience Platform에 통합된 Data Science Workspace을 사용하면 Adobe 솔루션에서 컨텐츠 및 데이터 자산을 사용하여 예측을 할 수 있습니다. Data Science Workspace가 이를 수행하는 방법 중 하나는 JupiterLab을 사용하는 것입니다. JupiterLab 은 웹 기반 사용자 인터페이스로서 <a href="https://jupyter.org/" target="_blank">프로젝트 선택기</a> 와 Adobe Experience Platform은 긴밀하게 통합되어 있습니다. 데이터 과학자들이 Jupiter 노트북, 코드 및 데이터를 사용하여 작업할 수 있는 대화형 개발 환경을 제공합니다.

| 기능 | 설명 |
| --- | --- |
| JupiterLab Launcher | 이제 JupiterLab Launcher에 Spark 3.2 노트북의 새로운 제품이 포함됩니다. Spark 2.4 노트북 제품이 Spark 3.2 노트북으로 교체되었으며 이번 릴리스의 일부가 됩니다. |
| Spark 3.2 | New Scala(Spark) 및 PySpark 레시피에서 Spark 3.2 사용 |
| 커널들 | Scala(Spark) 노트북은 이제 Scala 커널을 통해 작성됩니다. 이제 PySpark 노트북은 Python 커널을 통해 작성됩니다. Spark 및 PySpark 커널은 사용되지 않으며 이후 릴리스에서 제거되도록 설정됩니다. |
| 레서피 | 새로운 PySpark 및 Spark 레시피가 Python 및 R 레서피와 유사한 Docker 워크플로우를 따릅니다. |

{style=&quot;table-layout:auto&quot;}

Data Science Workspace에 대한 일반적인 정보는 [개요 설명서](../../data-science-workspace/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 는 Adobe Experience Platform에서 데이터를 원활하게 활성화할 수 있도록 대상 플랫폼과의 사전 구축된 통합입니다. 대상을 사용하여 크로스 채널 마케팅 캠페인, 이메일 캠페인, 타겟팅 광고 및 기타 많은 사용 사례에 대해 알려진 데이터와 알 수 없는 데이터를 활성화할 수 있습니다.

**새로운 기능 또는 업데이트된 기능**

| 기능 | 설명 |
| ----------- | ----------- |
| (베타) Destination SDK 지원 [[!DNL Google Cloud Storage]](../../destinations/destination-sdk/server-and-file-configuration.md#gcs-example) 파일 기반 대상 및 [구성 가능한 파일 이름](../../destinations/destination-sdk/file-based-destination-configuration.md#file-name-configuration). | 이제 Destination SDK을 사용하여 Google Cloud 저장소 대상을 만들고 파일 이름 매크로를 통해 내보낸 파일에 대한 사용자 지정 파일 이름을 정의할 수 있습니다. <br><br> Adobe Experience Platform Destination SDK의 파일 기반 대상 지원은 현재 베타에 있습니다. 설명서 및 기능은 변경될 수 있습니다. |
| 데이터 흐름의 세그먼트 열은 배치 대상으로 실행됩니다 | 이제 데이터 흐름에서 배치 대상으로 실행하는 경우 UI에 각 데이터 흐름 실행과 연결된 세그먼트의 이름이 표시됩니다. 자세한 내용 [데이터 흐름에서 배치 대상에 실행](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations). |

{style=&quot;table-layout:auto&quot;}

**새 대상**

| 대상 | 설명 |
| ----------- | ----------- |
| [(베타) Google Ad Manager 360](../../destinations/catalog/advertising/google-ad-manager-360-connection.md) | 다음 [!DNL Google Ad Manager 360] 연결을 통해 일괄 업로드를 수행할 수 있습니다. [!DNL publisher provided identifiers] (PPID)을 [!DNL Google Ad Manager 360], 를 통해 [!DNL Google Cloud Storage] <br><br>이 대상은 현재 베타에 있으며 제한된 수의 고객만 사용할 수 있습니다. 액세스 권한을 요청하려면 [!DNL Google Ad Manager 360] 연결되면 Adobe 담당자에게 연락하여 [!DNL IMS Organization ID]. |
| [[!DNL Medallia]](/help/destinations/catalog/voice/medallia-connector.md) | 대상 Medallia 설문 조사 및 피드백 수집에 대한 프로필을 활성화하여 고객 요구 사항과 기대를 더 잘 이해합니다. |
| [[!DNL Adobe Advertising Cloud DSP]](../../destinations/catalog/advertising/adobe-advertising-cloud-connection.md) | Adobe Advertising Cloud [!DNL Demand-Side Platform] (DSP) 대상을 사용하면 DSP과 캠페인 활성화를 위해 승인된 자사 세그먼트를 승인된 광고주 및 사용자와 공유할 수 있습니다. |

{style=&quot;table-layout:auto&quot;}

대상에 대한 자세한 내용은 [대상 개요](../../destinations/home.md).

## XDM(경험 데이터 모델) {#xdm}

XDM은 Adobe Experience Platform으로 가져온 데이터에 대한 일반적인 구조 및 정의(스키마)를 제공하는 오픈 소스 사양입니다. XDM 표준을 준수함으로써 모든 고객 경험 데이터를 공통 표현으로 통합하여 보다 빠르고 통합된 방식으로 통찰력을 제공할 수 있습니다. 고객 작업을 통해 유용한 통찰력을 얻을 수 있고, 세그먼트를 통해 고객 대상을 정의하고, 개인화를 위해 고객 속성을 사용할 수 있습니다.

**새로운 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 |
| --- | --- | --- |
| 클래스 | [[!UICONTROL 약물]](https://github.com/adobe/xdm/blob/master/components/classes/medication.schema.json) | 의료용 물질, 특히 약이나 약물에 대한 자세한 내용을 캡처하는 의료 산업 클래스. |
| 클래스 | [[!UICONTROL 계획]](https://github.com/adobe/xdm/blob/master/components/classes/plan.schema.json) | 의료 계획이나 보험 계획과 같은 의료 계획에 대한 세부 사항을 캡처하는 의료 산업 등급. |
| 클래스 | [[!UICONTROL 공급자]](https://github.com/adobe/xdm/blob/master/components/classes/provider.schema.json) | 의료 기관에 대한 세부 정보를 캡처하는 의료 산업 클래스 |
| 클래스 | [[!UICONTROL 지급인]](https://github.com/adobe/xdm/blob/master/components/classes/payer.schema.json) | 보험 회사에 대한 세부 사항을 캡처하는 의료 산업 클래스. |
| 클래스 | [[!UICONTROL 라이브 이벤트 일정]](https://github.com/adobe/xdm/blob/master/components/classes/live-event-schedule.json) | 여행 콘서트 일정이나 스포츠 팀의 일정과 같은 라이브 행사 일정에 대한 세부 사항을 캡처하는 스포츠 및 엔터테인먼트 업계 클래스입니다. |
| 클래스 | [[!UICONTROL 위치]](https://github.com/adobe/xdm/blob/master/components/classes/location.json) | 콘서트 홀이나 스포츠 경기장과 같은 라이브 이벤트의 위치를 캡처하는 스포츠 및 엔터테인먼트 업계 클래스입니다. |
| 필드 그룹 | [[!UICONTROL 의료용 약물]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/medication/healthcare-medication.schema.json) | 에 대한 필드 그룹 [!UICONTROL 약물] 브랜드 이름, 로트 번호, 수량 등 약물에 대한 세부 사항을 캡처하는 분류 |
| 필드 그룹 | [[!UICONTROL 의료 계획 세부 정보]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/plan/healthcare-plan-details.schema.json) | 에 대한 필드 그룹 [!UICONTROL 계획] 네트워크, 유형 및 활성 상태 등의 세부 정보를 캡처하는 클래스입니다. |
| 필드 그룹 | [[!UICONTROL 의료 기관]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/provider/healthcare-provider-details.schema.json) | 에 대한 필드 그룹 [!UICONTROL 공급자] 보건의료 진단 및 치료 서비스를 제공할 수 있는 허가를 받은 개인 건강 전문가 또는 건강 시설 조직의 세부 사항을 캡처하는 클래스입니다. |
| 필드 그룹 | [[!UICONTROL 의료 구성원 세부 정보]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/provider/healthcare-provider-details.schema.json) | 에 대한 필드 그룹 [!UICONTROL XDM 개별 프로필] 연락처 정보, 1차 진료 의사 및 계획 정보 등 서비스 또는 의료 서비스를 받거나 받게 될 사람의 세부 정보를 캡처하는 클래스입니다. |
| 필드 그룹 | [[!UICONTROL Sitetool 세부 정보]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-healthcare-sitetool.schema.json) | 에 대한 필드 그룹 [!UICONTROL XDM ExperienceEvent] chatbot, survey 등과 같은 사이트 도구에 의해 수집된 정보를 캡처하는 클래스입니다. |
| 필드 그룹 | [[!UICONTROL 라이브 이벤트 티켓 구매]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-live-event-ticket-purchase.json) | 에 대한 필드 그룹 [!UICONTROL XDM ExperienceEvent] 콘서트 또는 스포츠 게임과 같은 라이브 이벤트 티켓 구매 내역을 캡처하는 클래스입니다. |
| 필드 그룹 | [[!UICONTROL 스포츠 및 엔터테인먼트 이벤트 일정]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/live-event-schedule/sports-entertainment-event-schedule.schema.json) | 에 대한 필드 그룹 [!UICONTROL 라이브 이벤트 일정] 명소 이름, 도어 개설 시간 등 일정에 대한 세부 정보를 캡처하는 클래스. |
| 필드 그룹 | [[!UICONTROL 스포츠 엔터테인먼트 행사 장소]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/location/sports-entertainment-event-venue.schema.json) | 에 대한 필드 그룹 [!UICONTROL 위치] 좌석 용량 및 DMA(지정 시장 지역)와 같은 이벤트 장소에 대한 자세한 내용을 캡처하는 클래스입니다. |
| 전역 스키마 | (여러 개) | RTCDP Insights의 대상 지표에 새로운 전역 스키마를 사용할 수 있습니다. 다음을 참조하십시오 [가져오기 요청](https://github.com/adobe/xdm/pull/1560) 자세한 내용 |

{style=&quot;table-layout:auto&quot;}

**업데이트된 XDM 구성 요소**

| 구성 요소 유형 | 이름 | 설명 업데이트 |
| --- | --- | --- |
| 비헤이비어 | [[!UICONTROL 시계열 스키마]](https://github.com/adobe/xdm/blob/master/components/behaviors/time-series.schema.json) | 미디어 상태 업데이트 이벤트 유형을 추가했습니다. |
| 필드 그룹 | [[!UICONTROL 숙박예약]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.schema.json) | 숙박 체크아웃 속성을 추가했습니다. |
| 데이터 유형 | [[!UICONTROL 미디어 정보]](https://github.com/adobe/xdm/blob/master/components/datatypes/media.schema.json) | 상태 시작 및 상태 종료 필드가 추가되었습니다. |
| 확장 | [[!UICONTROL Workfront 변경 이벤트]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/changeevent.schema.json) | 사용자 및 이벤트 만들기 시간을 식별하는 데 도움이 되는 속성을 저장하는 데 사용되는 두 개의 필드를 추가했습니다. |
| 확장 | [[!UICONTROL Adobe CJM ExperienceEvent - 메시지 상호 작용 세부 사항]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/message-interaction.schema.json) | 구독, 동의, 사용자 지정 이메일 및 추가 데이터 정보를 랜딩 페이지 개체에 추가했습니다. |

{style=&quot;table-layout:auto&quot;}

Platform의 XDM에 대한 자세한 내용은 [XDM 시스템 개요](../../xdm/home.md).

## 쿼리 서비스 {#query-service}

Query Service를 사용하면 표준 SQL을 사용하여 Adobe Experience Platform에서 데이터를 쿼리할 수 있습니다 [!DNL Data Lake]. 에서 모든 데이터 세트에 가입할 수 있습니다 [!DNL Data Lake] 쿼리 결과를 보고 또는 Data Science Workspace에 사용하거나 실시간 고객 프로필에 수집하기 위한 새로운 데이터 세트로 캡처합니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 애드혹 스키마 레이블 지정 | Query Service CTAS 쿼리를 통해 자동으로 생성된 Ad Hoc 스키마의 데이터 필드에 레이블을 적용하여 중요한 데이터에 대한 액세스를 관리합니다. 임시 스키마의 특정 필드 또는 데이터 세트의 사용을 제한하여 중요한 개인 데이터와 개인 식별 정보 모두에 대한 액세스를 제어할 수 있습니다. 특성 기반 액세스 제어 기능을 사용하면 플랫폼 UI를 통해 임시 스키마 필드에 레이블을 지정할 수 있습니다. |
| `FLATTEN` 설정 | 타사 BI 도구를 통해 데이터베이스에 연결할 때 `FLATTEN` 중첩 데이터 구조를 병합하면 속성 이름이 행 값을 포함하는 열 이름이 되는 별도의 열로 병합됩니다. 따라서 Ad Hoc 스키마의 유용성이 개선되고, 중첩된 데이터 구조를 지원하지 않는 BI 도구에서 데이터를 검색, 분석, 변환 및 보고하는 데 필요한 작업 로드가 줄어듭니다. |

{style=&quot;table-layout:auto&quot;}

쿼리 서비스에 대한 자세한 내용은 [쿼리 서비스 개요](../../query-service/home.md).

## 소스 {#sources}

Adobe Experience Platform은 외부 소스에서 데이터를 수집하면서도 Platform 서비스를 사용하여 해당 데이터를 구조화, 레이블 지정 및 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 타사 소프트웨어 및 CRM 시스템과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

Experience Platform은 다양한 데이터 공급자에 대한 소스 연결을 쉽게 설정할 수 있는 RESTful API 및 대화형 UI를 제공합니다. 이러한 소스 연결을 통해 외부 스토리지 시스템 및 CRM 서비스를 인증 및 연결하고, 수집 실행 시간을 설정하고, 데이터 수집 처리량을 관리할 수 있습니다.

| 기능 | 설명 |
| --- | --- |
| 베타 릴리스 [!DNL Mixpanel] 소스 | 이제 를 사용할 수 있습니다 [!DNL Mixpanel] 소스에서 analytics 데이터 수집 [!DNL Mixpanel] Experience Platform 계정. 자세한 내용은 [[!DNL Mixpanel] 소스 설명서](../../sources/connectors/analytics/mixpanel.md) 추가 정보. |

{style=&quot;table-layout:auto&quot;}

소스에 대해 자세히 알아보려면 [소스 개요](../../sources/home.md).
