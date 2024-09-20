---
title: Google BigQuery Source 커넥터 개요
description: API 또는 사용자 인터페이스를 사용하여 Google BigQuery를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 35c61382-a909-47f4-a937-15cb725ecbe3
source-git-commit: 1fa79b31b5a257ebb3cbd60246b757d8a4a63d7c
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# [!DNL Google BigQuery] 원본

>[!IMPORTANT]
>
>[!DNL Google BigQuery] 원본은 Real-time Customer Data Platform Ultimate를 구입한 사용자가 소스 카탈로그에서 사용할 수 있습니다.

Adobe Experience Platform을 사용하면 외부 소스에서 데이터를 수집할 수 있으며 Platform 서비스를 사용하여 들어오는 데이터를 구조화하고, 레이블을 지정하고, 향상시킬 수 있습니다. Adobe 애플리케이션, 클라우드 기반 스토리지, 데이터베이스 및 기타 여러 소스와 같은 다양한 소스에서 데이터를 수집할 수 있습니다.

[!DNL Google BigQuery] 계정을 Experience Platform에 연결하기 위해 완료해야 하는 필수 구성 요소 단계는 이 문서를 참조하십시오.

## 전제 조건 {#prerequisites}

다음 단원에서는 [!DNL Google BigQuery] 원본 연결을 만들기 전에 필요한 필수 구성 요소 설정에 대한 자세한 정보를 제공합니다.

### IP 주소 허용 목록

소스 커넥터로 작업하려면 먼저 IP 주소 목록을 허용 목록에 추가해야 합니다. 지역별 IP 주소를 허용 목록에 추가하지 않으면 소스 사용 시 오류가 발생하거나 성능이 저하될 수 있습니다. 자세한 내용은 [IP 주소 허용 목록](../../ip-address-allow-list.md) 페이지를 참조하세요.

### [!DNL Google BigQuery] 자격 증명 생성 {#credentials}

[!DNL Google BigQuery]을(를) Experience Platform에 연결하려면 다음 자격 증명에 대한 값을 생성해야 합니다.

>[!BEGINTABS]

>[!TAB 기본 인증]

OAuth 2.0과 기본 인증의 조합을 사용하여 인증하려면 다음 자격 증명에 적절한 값을 제공하십시오.

| 자격 증명 | 설명 |
| --- | --- |
| `project` | 프로젝트는 [!DNL Google BigQuery]을(를) 포함하여 [!DNL Google Cloud] 리소스에 대한 기본 수준 조직 엔터티입니다. |
| `clientID` | 클라이언트 ID는 [!DNL Google BigQuery] OAuth 2.0 자격 증명의 절반입니다. |
| `clientSecret` | 클라이언트 암호는 [!DNL Google BigQuery] OAuth 2.0 자격 증명의 나머지 절반입니다. |
| `refreshToken` | 새로 고침 토큰을 사용하면 API에 대한 새 액세스 토큰을 가져올 수 있습니다. 액세스 토큰의 수명은 제한되어 있으며 프로젝트 과정 중에 만료될 수 있습니다. 필요한 경우 새로 고침 토큰을 사용하여 프로젝트에 대한 후속 액세스 토큰을 인증하고 요청할 수 있습니다. |
| `largeResultsDataSetId` | (선택 사항) 큰 결과 집합에 대한 지원을 사용하도록 설정하는 데 필요한 미리 만들어진 [!DNL Google BigQuery] 데이터 집합 ID입니다. |

[!DNL Google] API에 대한 OAuth 2.0 자격 증명을 생성하는 방법에 대한 자세한 지침은 다음 [[!DNL Google] OAuth 2.0 인증 안내서](https://developers.google.com/identity/protocols/oauth2)를 참조하십시오.

>[!TAB 서비스 인증]

서비스 인증을 사용하여 인증하려면 다음 자격 증명에 적절한 값을 제공하십시오.

**참고**: 서비스 인증으로 인증하려면 서비스 계정에 **[!DNL BigQuery Job User]**, **[!DNL BigQuery Data Viewer]**, **[!DNL BigQuery Read Session User]** 및 **[!DNL BigQuery Data Owner]**&#x200B;과(와) 같은 충분한 권한이 있어야 합니다.

| 자격 증명 | 설명 |
| --- | --- |
| `projectId` | 쿼리할 [!DNL Google BigQuery]의 ID입니다. |
| `keyFileContent` | 서비스 계정을 인증하는 데 사용되는 키 파일입니다. [[!DNL Google Cloud service accounts] 대시보드](https://console.cloud.google.com)에서 이 값을 검색할 수 있습니다. 키 파일 콘텐츠는 JSON 형식입니다. Experience Platform에 인증할 때 [!DNL Base64]에서 이를 인코딩해야 합니다. |
| `largeResultsDataSetId` | (선택 사항) 큰 결과 집합에 대한 지원을 사용하도록 설정하는 데 필요한 미리 만들어진 [!DNL Google BigQuery] 데이터 집합 ID입니다. |

[!DNL Google BigQuery]에서 서비스 계정을 사용하는 방법에 대한 자세한 내용은 [에서 서비스 계정 사용 [!DNL Google BigQuery]](https://cloud.google.com/bigquery/docs/use-service-accounts)에 대한 안내서를 참조하십시오.

>[!ENDTABS]

## [!DNL Google BigQuery]을(를) 플랫폼에 연결

아래 설명서는 API 또는 사용자 인터페이스를 사용하여 [!DNL Google BigQuery]을(를) 플랫폼에 연결하는 방법에 대한 정보를 제공합니다.

### API 사용

- [흐름 서비스 API를 사용하여 Google BigQuery 기본 연결 만들기](../../tutorials/api/create/databases/bigquery.md)
- [흐름 서비스 API를 사용하여 데이터 테이블 탐색](../../tutorials/api/explore/tabular.md)
- [흐름 서비스 API를 사용하여 데이터베이스 소스에 대한 데이터 흐름 만들기](../../tutorials/api/collect/database-nosql.md)

### UI 사용

- [UI에서 Google BigQuery 소스 연결 만들기](../../tutorials/ui/create/databases/bigquery.md)
- [UI에서 데이터베이스 소스 연결을 위한 데이터 흐름 만들기](../../tutorials/ui/dataflow/databases.md)
