---
title: Adobe Experience Platform 릴리스 노트 - 2022년 6월
description: Adobe Experience Platform에 대한 2022년 6월 릴리스 노트입니다.
source-git-commit: 492a05b24ec905de926d861f607a6e5d294d46e0
workflow-type: tm+mt
source-wordcount: '801'
ht-degree: 6%

---

# Adobe Experience Platform 릴리스 노트

**릴리스 날짜: 2022년 6월 22일**

Adobe Experience Platform의 기존 기능 업데이트:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [쿼리 서비스](#query-service)
- [소스](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 데이터 엔지니어가 XDM(Experience Data Model) 을 통해 데이터를 매핑, 변환 및 확인할 수 있습니다.

**업데이트된 기능**

| 기능 | 설명 |
| --- | --- |
| 개선 사항 [!DNL Data Prep] Recommendations | [!DNL Data Prep] Recommendations은 이제 더 똑똑하고 더 빠릅니다. 새 유효성 검사 기능을 통해 가장 일반적인 매핑 오류가 크게 줄어들어 시간-값 이 줄어듭니다. |

{style=&quot;table-layout:auto&quot;}

자세한 내용은 [!DNL Data Prep]를 보려면 [[!DNL Data Prep] 개요](../../data-prep/home.md).

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

{style=&quot;table-layout:auto&quot;}

**새 대상**

| 대상 | 설명 |
| ----------- | ----------- |
| [(베타) Google Ad Manager 360](../../destinations/catalog/advertising/google-ad-manager-360-connection.md) | 다음 [!DNL Google Ad Manager 360] 연결을 통해 일괄 업로드를 수행할 수 있습니다. [!DNL publisher provided identifiers] (PPID)을 [!DNL Google Ad Manager 360], 를 통해 [!DNL Google Cloud Storage] <br><br>이 대상은 현재 베타에 있으며 제한된 수의 고객만 사용할 수 있습니다. 액세스 권한을 요청하려면 [!DNL Google Ad Manager 360] 연결되면 Adobe 담당자에게 연락하여 [!DNL IMS Organization ID]. |
| [[!DNL Medallia]](/help/destinations/catalog/voice/medallia-connector.md) | 대상 Medallia 설문 조사 및 피드백 수집에 대한 프로필을 활성화하여 고객 요구 사항과 기대를 더 잘 이해합니다. |

{style=&quot;table-layout:auto&quot;}

대상에 대한 자세한 내용은 [대상 개요](../../destinations/home.md).

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
