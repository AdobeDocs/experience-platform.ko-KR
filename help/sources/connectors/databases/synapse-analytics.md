---
title: Azure Synapse Analytics Source 커넥터 개요
description: API 또는 사용자 인터페이스를 사용하여 Azure Synapse Analytics를 Adobe Experience Platform에 연결하는 방법을 알아봅니다.
badgeUltimate: label="Ultimate" type="Positive"
last-substantial-update: 2025-06-17T00:00:00Z
exl-id: 5b94ae74-e5a7-40e9-a952-41eddf06dcde
source-git-commit: f8eb8640360205e8ae9579d4b664d4880bf8a368
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 3%

---

# [!DNL Azure Synapse Analytics]

>[!IMPORTANT]
>
>[!DNL Azure Synapse Analytics] 소스는 Real-Time Customer Data Platform Ultimate을 구매한 사용자가 소스 카탈로그에서 사용할 수 있습니다.

[!DNL Azure Synapse Analytics]은(는) 빅 데이터와 데이터 웨어하우징을 통합하는 클라우드 기반 분석 서비스입니다. SQL, [!DNL Spark] 또는 실시간 도구를 사용하여 데이터를 이동 없이 수집, 탐색, 준비 및 분석할 수 있습니다.

[!DNL Azure Synapse Analytics] 원본을 사용하여 계정을 연결하고 데이터를 Adobe Experience Platform으로 가져올 수 있습니다.

## 전제 조건 {#prerequisites}

[!DNL Azure Synapse Analytics] 계정을 Experience Platform에 연결하기 전에 필수 구성 요소 설정을 완료하려면 다음 섹션을 참조하십시오.

### 허용 목록에 추가하다 IP 주소

소스를 Experience Platform에 연결하기 전에 지역별 IP 주소를 허용 목록에 추가하다에 추가해야 합니다. 자세한 내용은 [Experience Platform에 연결하기 위한 IP 주소 허용 목록에 추가](../../ip-address-allow-list.md)에 대한 안내서를 참조하십시오.

### 권한 구성

소스 계정을 Experience Platform에 연결하려면 계정에 다음 권한이 모두 활성화되어 있어야 합니다.

* **소스 보기**
* **소스 관리**

이러한 권한이 없는 경우 제품 관리자에게 문의하여 액세스 권한을 요청하십시오. 자세한 내용은 [액세스 제어 UI 안내서](../../../access-control/ui/overview.md)를 참조하십시오.

### Experience Platform 인증

계정 키 인증 또는 서비스 주체 키 인증을 사용하여 [!DNL Azure Synapse Analytics]을(를) Experience Platform에 연결할 수 있습니다.

>[!BEGINTABS]

>[!TAB 계정 키 인증]

계정 키 인증을 사용하여 [!DNL Azure Synapse Analytics] 데이터베이스를 Experience Platform에 연결하려면 다음 자격 증명에 대한 값을 제공하십시오.

| 자격 증명 | 설명 |
| --- | --- |
| 연결 문자열 | [!DNL Azure Synapse Analytics]&#x200B;(으)로 인증하는 데 사용되는 **연결 문자열**&#x200B;입니다. 표준 형식은 `Server=tcp:{SERVER_NAME}.database.windows.net,1433;Database={DATABASE};User ID={USERNAME}@{SERVER_NAME};Password={PASSWORD};Trusted_Connection=False;Encrypt=True;Connection Timeout=30`입니다. 자리 표시자를 실제 연결 세부 정보로 바꿔야 합니다. |
| 연결 사양 ID | **연결 사양**&#x200B;은(는) 데이터 원본의 커넥터 속성을 제공합니다. 여기에는 **기본** 및 **소스** 연결을 모두 만들기 위한 인증 사양 및 요구 사항과 같은 세부 정보가 포함됩니다. [!DNL Azure Synapse Analytics]의 경우 연결 사양 ID는 `a49bcc7d-8038-43af-b1e4-5a7a089a7d79`입니다. **참고:** 이 자격 증명은 API를 통해 연결할 때만 필요합니다. |

>[!TAB 서비스 사용자 키 인증]

서비스 사용자 키 인증을 위한 자격 증명을 검색하려면 [[!DNL Microsfot Entra admin center]](https://entra.microsoft.com/#home)&#x200B;(으)로 이동하여 다음 값을 검색하십시오.

* 앱 ID
* 표시 이름
* Secret
* 테넌트 ID

그런 다음 [[!DNL Azure Synapse Analytics] 인스턴스](https://azure.microsoft.com/en-ca/products/synapse-analytics)&#x200B;(으)로 이동한 다음 외부 공급자에서 사용자를 만드는 옵션을 선택합니다. 여기에서 스키마에 대한 서비스 사용자에 대한 적절한 권한을 제공합니다. **참고:**: 스키마 미리 보기에 필요하므로 &quot;COPY&quot;와 비슷한 &quot;SELECT&quot;를 포함해야 합니다. 예를 들어 명령 예는 다음과 같습니다.

```SQL
GRANT SELECT ON SCHEMA::dbo TO {APP_ID};
```

서비스 주체 키 인증을 사용하여 [!DNL Azure Synapse Analytics] 데이터베이스를 Experience Platform에 연결하려면 다음 자격 증명의 값을 제공하십시오.

| 자격 증명 | 설명 |
| --- | --- |
| 서버 | [!DNL Azure Synapse Analytics] SQL 끝점의 정규화된 도메인 이름입니다. |
| 데이터베이스 | [!DNL Azure Synapse Analytics] 작업 영역의 특정 데이터베이스 이름입니다. |
| 테넌트 | [!DNL Azure] 구독과 연결된 [!DNL Azure Active Directory] 테넌트 ID입니다. |
| 서비스 주체 ID | [!DNL Azure Active Directory] 응용 프로그램의 클라이언트 ID. |
| 서비스 주체 키 | 서비스 주체와 연계된 클라이언트 암호. |
| 연결 사양 ID | **연결 사양**&#x200B;은(는) 데이터 원본의 커넥터 속성을 제공합니다. 여기에는 **기본** 및 **소스** 연결을 모두 만들기 위한 인증 사양 및 요구 사항과 같은 세부 정보가 포함됩니다. [!DNL Azure Synapse Analytics]의 경우 연결 사양 ID는 `a49bcc7d-8038-43af-b1e4-5a7a089a7d79`입니다. **참고:** 이 자격 증명은 API를 통해 연결할 때만 필요합니다. |

자세한 내용은  [!DNL Azure Synapse Analytics][&#128279;](https://learn.microsoft.com/en-us/azure/synapse-analytics/synapse-service-identity)에 대한 ID 관리에 대한 [!DNL Azure] 설명서를 참조하십시오.

>[!ENDTABS]

## API를 사용하여 [!DNL Azure Synapse Analytics]을(를) Experience Platform에 연결

* [흐름 서비스 API를 사용하여  [!DNL Azure Synapse Analytics] 을(를) Experience Platform에 연결](../../tutorials/api/create/databases/synapse-analytics.md)
* [흐름 서비스 API를 사용하여 데이터 테이블 탐색](../../tutorials/api/explore/tabular.md)
* [흐름 서비스 API를 사용하여 데이터베이스 소스에 대한 데이터 흐름 만들기](../../tutorials/api/collect/database-nosql.md)

## UI를 사용하여 [!DNL Azure Synapse Analytics]을(를) Experience Platform에 연결

* [UI에서  [!DNL Azure Synapse Analytics] 을(를) Experience Platform에 연결](../../tutorials/ui/create/databases/synapse-analytics.md)
* [UI에서 데이터베이스 소스 연결을 위한 데이터 흐름 만들기](../../tutorials/ui/dataflow/databases.md)

