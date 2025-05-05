---
keywords: Experience Platform; 쿼리 서비스; IP 액세스 제어; 인증; API; 시작하기
title: Data Distiller Authorization API 안내서
description: Adobe Experience Platform의 쿼리 서비스 내에서 보안 데이터 액세스를 위해 권한 부여 및 IP 범위 제한을 시작하는 방법을 알아봅니다.
role: Developer
exl-id: d93ce774-c8b2-4f15-a4d9-117d9aa5d9e7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 5%

---

# Data Distiller Authorization API 시작

>[!AVAILABILITY]
>
>이 기능은 Data Distiller 추가 기능을 구입한 고객이 사용할 수 있습니다. 자세한 내용은 Adobe 담당자에게 문의하십시오.

Data Distiller Authorization API는 Adobe Experience Platform의 SQL 인터페이스를 통해 조직에 데이터 액세스를 더 강력하게 제어할 수 있도록 합니다. 이 API를 사용하여 IP 제한을 정의하고, 지정된 네트워크에 대한 데이터 액세스를 제한하며, 보안 모니터링을 강화할 수 있습니다.

이 안내서에서는 Data Distiller 인증 API를 호출하는 데 필요한 인증 자격 증명 및 권한을 설정하는 방법에 대해 간략하게 설명합니다.

## 시작하기 {#getting-started}

다음 섹션에서는 필요한 인증 값을 준비하고 Data Distiller 인증 API에 대한 첫 번째 요청을 수행하는 방법에 대한 정보를 제공합니다.

### 필요한 권한 {#required-permissions}

Query Service에서 보안 데이터 액세스 제한을 사용하려면 **[!UICONTROL 허용 목록 관리]** 권한이 필요합니다. 이 권한을 사용하면 조직에서 SQL 인터페이스를 통해 Experience Platform의 데이터에 액세스할 권한이 있는 특정 IP 범위(IPv4 또는 IPv6 형식)를 정의할 수 있습니다. 액세스는 샌드박스 수준에서 관리되며, 사용자는 승인된 IP 주소 또는 허용된 네트워크로만 액세스를 제한하는 CIDR 블록 목록을 구성할 수 있습니다.

>[!NOTE]
>
>시스템 관리자는 Adobe [Admin Console](https://adminconsole.adobe.com/)에서 사용자 권한을 설정할 수 있습니다. 자세한 내용은 [Admin Console 사용 안내서](https://helpx.adobe.com/kr/enterprise/using/admin-console.html)를 참조하십시오.

**[!UICONTROL 허용 목록 관리]** 권한으로 다음 기능을 사용할 수 있습니다.

- **허용된 IP 범위를 정의**: 이러한 정의된 범위의 IP 주소 또는 CIDR 블록만 쿼리 서비스를 통해 SQL을 사용하여 Experience Platform의 데이터에 액세스할 수 있습니다.
- **IP 범위 확인 적용**: 허용된 범위 밖의 IP에서 연결이 거부되었습니다.
- **감사 및 경고 기능**: 거부된 연결을 포함한 모든 액세스 시도가 감사 이벤트로 기록됩니다. 이러한 이벤트는 [Adobe Experience Platform 감사 로그](../../landing/governance-privacy-security/audit-logs/overview.md)에서 사용할 수 있으므로 잠재적인 보안 위반을 모니터링할 수 있습니다.

### 필수 헤더에 대한 값 수집 {#gather-values-for-required-headers}

Data Distiller 권한 부여 API를 호출하려면 API 호출의 필수 헤더에 대한 값을 제공하는 [Experience Platform API 인증 자습서](../../landing/api-authentication.md)를 완료해야 합니다. 각 요청에 다음 헤더를 포함합니다.

- **인증**: `Bearer {ACCESS_TOKEN}`
- **x-api-key**: `{API_KEY}`
- **x-gw-ims-org-id**: `{ORG_ID}`
- **x-sandbox-name**: `{SANDBOX_NAME}`

>[!NOTE]
>
> 샌드박스에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하세요.

페이로드(POST, PUT, PATCH)가 포함된 모든 요청에도 이 헤더가 필요합니다.

- **Content-Type**: `application/json`

### 다음 단계

필요한 권한 및 헤더 값이 수집되면 쿼리 서비스에 대한 IP 제한 구성을 시작할 수 있습니다. 다음을 포함한 CRUD 작업의 세부 예는 엔드포인트 설명서 로 이동합니다.

- API 형식 및 샘플 요청/응답 쌍.
- 각 작업에 대한 헤더, 페이로드 및 응답 코드.

각 API 호출 예는 요청의 형식을 지정하고 응답을 해석하는 방법을 보여 주므로 Query Service에서 데이터에 안전하게 액세스할 수 있습니다.

IP 제한 구성 및 유효성 검사에 대한 특정 지침은 [IP 액세스 끝점 설명서](./ip-access.md) 및 [IP 유효성 검사 끝점 설명서](./validate.md)를 참조하세요.

보다 쉬운 통합, 테스트 및 탐색을 위해 표준화되고 기계가 읽을 수 있는 형식을 보려면 [데이터 Distiller Authorization OpenAPI 참조 설명서](https://developer.adobe.com/experience-platform-apis/references/data-distiller-auth/)를 참조하세요.
