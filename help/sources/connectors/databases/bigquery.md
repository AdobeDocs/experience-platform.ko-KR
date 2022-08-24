---
keywords: Experience Platform;홈;인기 항목;빅 쿼리;bigquery;Google BigQuery;google bigquery
solution: Experience Platform
title: Google BigQuery Source Connector 개요
topic-legacy: overview
description: API 또는 사용자 인터페이스를 사용하여 Google BigQuery를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: 7a62dcf1e9712d3c0c0d148b953e50dc11c91f1b
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# [!DNL Google BigQuery]

Adobe Experience Platform을 사용하면 Platform 서비스를 사용하여 들어오는 데이터를 구조화, 레이블 지정 및 향상시키는 기능을 제공하면서 외부 소스에서 데이터를 수집할 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 등과 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

[!DNL Experience Platform] 에서는 타사 데이터베이스에서 데이터를 수집하기 위한 지원을 제공합니다. 플랫폼은 관계형, NoSQL 또는 데이터 웨어하우스와 같은 다양한 유형의 데이터베이스에 연결할 수 있습니다. 데이터베이스 공급자에 대한 지원은 다음과 같습니다 [!DNL Google BigQuery].

## IP 주소 허용 목록

소스 커넥터로 작업하기 전에 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스를 사용할 때 오류나 성능이 저하될 수 있습니다. 자세한 내용은 [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지를 참조하십시오.

## 전제 조건

다음 섹션에서는 생성 전에 필요한 전제 조건 설정에 대한 추가 정보를 제공합니다 [!DNL Google BigQuery] 소스 연결.

### 생성 [!DNL Google BigQuery] 자격 증명

연결하려면 [!DNL Google BigQuery] 플랫폼을 사용하려면 다음 자격 증명에 대한 값을 생성해야 합니다.

| 자격 증명 | 설명 |
| ---------- | ----------- |
| `project` | 프로젝트는 사용자의 기본 수준 구성 엔티티입니다 [!DNL Google Cloud] 다음을 포함한 리소스 [!DNL Google BigQuery]. |
| `clientID` | 클라이언트 ID가 사용자의 절반 [!DNL Google BigQuery] OAuth 2.0 자격 증명. |
| `clientSecret` | 클라이언트 비밀번호가 [!DNL Google BigQuery] OAuth 2.0 자격 증명. |
| `refreshToken` | 새로 고침 토큰을 사용하면 API에 대한 새 액세스 토큰을 가져올 수 있습니다. 액세스 토큰은 수명이 제한되어 있으며 프로젝트 진행 중에 만료될 수 있습니다. 필요한 경우 새로 고침 토큰을 사용하여 프로젝트에 대한 후속 액세스 토큰을 인증하고 요청할 수 있습니다. |
| `largeResultsDataSetId` | 미리 만들어진  [!DNL Google BigQuery] 큰 결과 세트에 대한 지원을 활성화하기 위해 필요한 데이터 세트 ID입니다. |

에 대한 OAuth 2.0 자격 증명을 생성하는 방법에 대한 자세한 지침은 [!DNL Google] API의 경우 다음을 참조하십시오 [[!DNL Google] OAuth 2.0 인증 안내서](https://developers.google.com/identity/protocols/oauth2).

## Connect [!DNL Google BigQuery] 플랫폼

아래 설명서에서는 연결 방법에 대한 정보를 제공합니다 [!DNL Google BigQuery] API 또는 사용자 인터페이스를 사용하여 플랫폼:

### API 사용

- [Flow Service API를 사용하여 Google BigQuery 기본 연결을 만듭니다](../../tutorials/api/create/databases/bigquery.md)
- [Flow Service API를 사용하여 데이터 테이블 탐색](../../tutorials/api/explore/tabular.md)
- [Flow Service API를 사용하여 데이터베이스 소스에 대한 데이터 흐름 만들기](../../tutorials/api/collect/database-nosql.md)

### UI 사용

- [UI에서 Google BigQuery 소스 연결 만들기](../../tutorials/ui/create/databases/bigquery.md)
- [UI에서 데이터베이스 소스 연결을 위한 데이터 흐름 만들기](../../tutorials/ui/dataflow/databases.md)
