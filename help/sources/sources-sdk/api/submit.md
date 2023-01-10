---
keywords: Experience Platform;홈;인기 항목;소스;커넥터;소스 커넥터;소스 sdk;sdk;SDK
title: 소스 제출
description: 다음 문서에서는 Flow Service API를 사용하여 새 소스를 테스트 및 확인하고 자체 서비스 소스(배치 SDK)를 통해 새 소스를 통합하는 방법에 대한 단계를 제공합니다.
exl-id: 9e945ba1-51b6-40a9-b92f-e0a52b3f92fa
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 0%

---

# 소스 제출

셀프 서비스 소스(배치 SDK)를 사용하여 Adobe Experience Platform에 새 소스를 통합하는 마지막 단계는 확인을 위해 소스를 테스트하는 것입니다. 성공하면 Adobe 담당자에게 연락하여 새 소스를 제출할 수 있습니다.

다음 문서에서는 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 시작하기

* Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [플랫폼 API 시작](../../../landing/api-guide.md).
* Platform API용 자격 증명을 생성하는 방법에 대한 자세한 내용은 [Experience Platform API 인증 및 액세스](../../../landing/api-authentication.md).
* 설정 방법에 대한 자세한 내용 [!DNL Postman] 플랫폼 API의 경우 다음 위치에서 자습서를 참조하십시오. [개발자 콘솔 설정 및 [!DNL Postman]](../../../landing/postman.md).
* 테스트 및 디버깅 프로세스에 도움이 되도록 [여기서 Self-Serve Sources 확인 수집 및 환경](../assets/sdk-verification.zip) 및 아래에 설명된 단계를 따릅니다.

## 소스 테스트

소스를 테스트하려면 [셀프 서비스 소스 검증 수집 및 환경](../assets/sdk-verification.zip) on [!DNL Postman] 를 통해 소스와 관련된 적절한 환경 변수를 제공할 수 있습니다.

테스트를 시작하려면 먼저 수집 및 환경을 설정해야 합니다 [!DNL Postman]. 다음으로 테스트할 연결 사양 ID를 지정합니다.

### 분류에 사용할 `authSpecName`

연결 사양 ID를 입력한 후에는 `authSpecName` 기본 연결에 사용할 수 있습니다. 선택한 내용에 따라 다음 중 하나일 수 있습니다 `OAuth 2 Refresh Code` 또는  `Basic Authentication`. 을 지정하고 `authSpecName`그런 다음 환경에 필요한 자격 증명을 포함해야 합니다. 예를 들어 `authSpecName` 로서의 `OAuth 2 Refresh Code`를 입력한 다음 OAuth 2에 필요한 자격 증명을 제공해야 합니다. `host` 및 `accessToken`.

### 분류에 사용할 `sourceSpec`

인증 사양 매개 변수가 추가되면 소스 사양에 필요한 속성을 추가해야 합니다. 에서 필요한 속성을 찾을 수 있습니다. `sourceSpec.spec.properties`. 의 경우 [!DNL MailChimp Members] 아래 예제에서 유일한 필수 속성은 다음과 같습니다. `listId`즉, `listId` 그리고 이는 [!DNL Postman] 환경.

```json
"spec": {
  "$schema": "http://json-schema.org/draft-07/schema#",
  "type": "object",
  "description": "Define user input parameters to fetch resource values.",
  "properties": {
    "listId": {
      "type": "string",
      "description": "listId for which members need to fetch."
    }
  }
}
```

인증 및 소스 사양 매개 변수가 제공되면 나머지 환경 변수에 채우기를 시작할 수 있습니다. 자세한 내용은 아래 표를 참조하십시오.

>[!NOTE]
>
>아래 예제 변수는 모두 를 제외하고 업데이트해야 하는 자리 표시자 값입니다 `flowSpecificationId` 및 `targetConnectionSpecId`: 고정 값입니다.

| 매개 변수 | 설명 | 예 |
| --- | --- | --- |
| `x-api-key` | Experience Platform API에 대한 호출을 인증하는 데 사용되는 고유 식별자입니다. 다음에서 자습서를 참조하십시오. [Experience Platform API 인증 및 액세스](../../../landing/api-authentication.md) 을 검색하는 방법에 대한 자세한 내용은 `x-api-key`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `x-gw-ims-org-id` | 제품 및 서비스를 소유하거나 라이센스를 부여하고 해당 구성원에 대한 액세스를 허용할 수 있는 법인. 다음에서 자습서를 참조하십시오. [개발자 콘솔 설정 및 [!DNL Postman]](../../../landing/postman.md) 을 검색하는 방법에 대한 지침 `x-gw-ims-org-id` 정보. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `authorizationToken` | Experience Platform API 호출을 완료하는 데 필요한 인증 토큰. 다음에서 자습서를 참조하십시오. [Experience Platform API 인증 및 액세스](../../../landing/api-authentication.md) 을 검색하는 방법에 대한 자세한 내용은 `authorizationToken`. | `Bearer authorizationToken` |
| `schemaId` | Platform에서 소스 데이터를 사용하려면 필요에 따라 소스 데이터를 구조화하기 위해 대상 스키마를 만들어야 합니다. 대상 XDM 스키마를 만드는 방법에 대한 자세한 내용은 다음 문서를 참조하십시오 [api를 사용하여 스키마 만들기](../../../xdm/api/schemas.md). | `https://ns.adobe.com/{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `schemaVersion` | 스키마에 해당하는 고유한 버전입니다. | `application/vnd.adobe.xed-full-notext+json; version=1` |
| `schemaAltId` | 다음 `meta:altId` 해당 변수와 함께 반환됩니다  `schemaId` 새 스키마를 생성할 때. | `_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `dataSetId` | 대상 데이터 세트를 만드는 방법에 대한 자세한 단계는 다음 사항에 대한 자습서를 참조하십시오. [api를 사용하여 데이터 세트 만들기](../../../catalog/api/create-dataset.md). | `5f3c3cedb2805c194ff0b69a` |
| `mappings` | 매핑 세트를 사용하여 소스 스키마의 데이터가 대상 스키마의 데이터에 매핑되는 방법을 정의할 수 있습니다. 매핑을 만드는 방법에 대한 자세한 단계는 다음을 참조하십시오. [api를 사용하여 매핑 세트 만들기](../../../data-prep/api/mapping-set.md). | `[{"destinationXdmPath":"person.name.firstName","sourceAttribute":"email.email_id","identity":false,"version":0},{"destinationXdmPath":"person.name.lastName","sourceAttribute":"email.activity.action","identity":false,"version":0}]` |
| `mappingId` | 매핑 세트에 해당하는 고유한 ID입니다. | `bf5286a9c1ad4266baca76ba3adc9366` |
| `connectionSpecId` | 소스와 일치하는 연결 사양 ID입니다. 이후에 생성한 ID입니다 [새 연결 사양 생성](./create.md). | `2e8580db-6489-4726-96de-e33f5f60295f` |
| `flowSpecificationId` | 흐름 사양 ID `RestStorageToAEP`. **고정 값입니다**. | `6499120c-0b15-42dc-936e-847ea3c24d72` |
| `targetConnectionSpecId` | 수집된 데이터가 들어오는 데이터 레이크의 타겟 연결 ID입니다. **고정 값입니다**. | `c604ff05-7f1a-43c0-8e18-33bf874cb11c` |
| `verifyWatTimeInSecond` | 흐름 실행 완료를 확인할 때 따라야 할 지정된 시간 간격입니다. | `40` |
| `startTime` | 데이터 흐름의 지정된 시작 시간입니다. 시작 시간은 unix 시간으로 포맷해야 합니다. | `1597784298` |

모든 환경 변수를 제공했으면 를 사용하여 컬렉션 실행을 시작할 수 있습니다. [!DNL Postman] 인터페이스. 에서 [!DNL Postman] 인터페이스에서 줄임표( )를 선택합니다&#x200B;**...**) 옆의 [!DNL Sources SSSs Verification Collection] 그런 다음 **컬렉션 실행**.

![주자](../assets/runner.png)

다음 [!DNL Runner] 데이터 흐름의 실행 순서를 구성할 수 있는 인터페이스가 표시됩니다. 선택 **SSS 검증 수집 실행** 컬렉션을 실행하려면

>[!NOTE]
>
>비활성화할 수 있습니다 **흐름 삭제** 플랫폼 UI에서 소스 모니터링 대시보드를 사용하려는 경우 실행 순서 확인 목록에서 를 선택합니다. 그러나 테스트가 완료되면 테스트 흐름이 삭제되었는지 확인해야 합니다.

![run-collection](../assets/run-collection.png)

## 소스 제출

소스가 전체 워크플로우를 완료할 수 있게 되면 Adobe 담당자에게 연락하여 통합을 위한 소스를 제출할 수 있습니다.
