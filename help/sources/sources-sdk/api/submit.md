---
keywords: Experience Platform;홈;인기 항목;소스;커넥터;소스 커넥터;소스 sdk;sdk;SDK
title: Source 제출
description: 다음 문서에서는 Flow Service API를 사용하여 새 소스를 테스트 및 확인하고 셀프서비스 소스(일괄 SDK)를 통해 새 소스를 통합하는 방법에 대한 단계를 제공합니다.
exl-id: 9e945ba1-51b6-40a9-b92f-e0a52b3f92fa
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---

# 소스 제출

셀프 서비스 소스(일괄 SDK)를 사용하여 새 소스를 Adobe Experience Platform에 통합하는 마지막 단계는 소스를 테스트하여 확인하는 것입니다. 성공하면 Adobe 담당자에게 연락하여 새 소스를 제출할 수 있습니다.

다음 문서에서는 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)를 사용하여 소스를 테스트하고 디버깅하는 방법에 대한 단계를 제공합니다.

## 시작하기

* Experience Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Experience Platform API 시작](../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.
* Experience Platform API에 대한 자격 증명을 생성하는 방법에 대한 자세한 내용은 [Experience Platform API 인증 및 액세스](../../../landing/api-authentication.md)에 대한 자습서를 참조하십시오.
* Experience Platform API용 [!DNL Postman]을(를) 설정하는 방법에 대한 자세한 내용은 [개발자 콘솔 설정 및 [!DNL Postman]](../../../landing/postman.md)에 대한 자습서를 참조하십시오.
* 테스트 및 디버깅 프로세스에 도움이 되도록 [여기에서 셀프 서비스 원본 확인 컬렉션 및 환경을 다운로드](../assets/sdk-verification.zip)하고 아래에 설명된 단계를 수행합니다.

## 소스 테스트

소스를 테스트하려면 해당 소스와 관련된 적절한 환경 변수를 제공하면서 [!DNL Postman]에서 [셀프 서비스 소스 확인 컬렉션 및 환경](../assets/sdk-verification.zip)을 실행해야 합니다.

테스트를 시작하려면 먼저 [!DNL Postman]에서 컬렉션 및 환경을 설정해야 합니다. 그런 다음 테스트할 연결 사양 ID를 지정합니다.

### `authSpecName` 지정

연결 사양 ID를 입력한 후에는 기본 연결에 사용할 `authSpecName`을(를) 지정해야 합니다. 선택에 따라 `OAuth 2 Refresh Code` 또는 `Basic Authentication`일 수 있습니다. `authSpecName`을(를) 지정한 후에는 환경에 필요한 자격 증명을 포함해야 합니다. 예를 들어 `authSpecName`을(를) `OAuth 2 Refresh Code`(으)로 지정하는 경우 OAuth 2에 필요한 자격 증명(`host` 및 `accessToken`)을 제공해야 합니다.

### `sourceSpec` 지정

인증 사양 매개변수가 추가되면 다음에 소스 사양에서 필요한 속성을 추가해야 합니다. `sourceSpec.spec.properties`에서 필요한 속성을 찾을 수 있습니다. 아래 [!DNL MailChimp Members] 예제의 경우 필요한 속성은 `listId`뿐입니다. 즉, `listId`이고 [!DNL Postman] 환경에 해당하는 ID 값입니다.

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

인증 및 소스 사양 매개 변수가 제공되면 나머지 환경 변수를 채우는 작업을 시작할 수 있습니다. 참조는 아래 표를 참조하십시오.

>[!NOTE]
>
>아래의 예제 변수는 모두 업데이트해야 하는 자리 표시자 값입니다. 단, 고정 값인 `flowSpecificationId`과(와) `targetConnectionSpecId`은(는) 예외입니다.

| 매개변수 | 설명 | 예 |
| --- | --- | --- |
| `x-api-key` | Experience Platform API 호출을 인증하는 데 사용되는 고유 식별자입니다. `x-api-key`을(를) 검색하는 방법에 대한 자세한 내용은 [Experience Platform API 인증 및 액세스](../../../landing/api-authentication.md)에 대한 자습서를 참조하십시오. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `x-gw-ims-org-id` | 제품 및 서비스를 소유하거나 라이선스를 부여하고 해당 구성원에 대한 액세스를 허용할 수 있는 법인 엔티티입니다. `x-gw-ims-org-id` 정보를 검색하는 방법에 대한 지침은 [개발자 콘솔 설정 및 [!DNL Postman]](../../../landing/postman.md)에 대한 자습서를 참조하십시오. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `authorizationToken` | Experience Platform API 호출을 완료하는 데 필요한 인증 토큰입니다. `authorizationToken`을(를) 검색하는 방법에 대한 자세한 내용은 [Experience Platform API 인증 및 액세스](../../../landing/api-authentication.md)에 대한 자습서를 참조하십시오. | `Bearer authorizationToken` |
| `schemaId` | 소스 데이터를 Experience Platform에서 사용하려면 타겟 스키마를 만들어 필요에 따라 소스 데이터를 구조화해야 합니다. 대상 XDM 스키마를 만드는 방법에 대한 자세한 단계는 [API를 사용하여 스키마 만들기](../../../xdm/api/schemas.md)에 대한 자습서를 참조하십시오. | `https://ns.adobe.com/{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `schemaVersion` | 스키마에 해당하는 고유 버전. | `application/vnd.adobe.xed-full-notext+json; version=1` |
| `schemaAltId` | 새 스키마를 만들 때 `schemaId`과(와) 함께 반환되는 `meta:altId`입니다. | `_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `dataSetId` | 대상 데이터 집합을 만드는 방법에 대한 자세한 단계는 [API를 사용하여 데이터 집합 만들기](../../../catalog/api/create-dataset.md)에 대한 자습서를 참조하십시오. | `5f3c3cedb2805c194ff0b69a` |
| `mappings` | 매핑 세트를 사용하여 소스 스키마의 데이터를 대상 스키마의 데이터에 매핑하는 방법을 정의할 수 있습니다. 매핑을 만드는 방법에 대한 자세한 단계는 [API를 사용하여 매핑 집합을 만드는 방법](../../../data-prep/api/mapping-set.md)에 대한 자습서를 참조하십시오. | `[{"destinationXdmPath":"person.name.firstName","sourceAttribute":"email.email_id","identity":false,"version":0},{"destinationXdmPath":"person.name.lastName","sourceAttribute":"email.activity.action","identity":false,"version":0}]` |
| `mappingId` | 매핑 세트에 해당하는 고유 ID입니다. | `bf5286a9c1ad4266baca76ba3adc9366` |
| `connectionSpecId` | 소스에 해당하는 연결 사양 ID입니다. [새 연결 사양을 만든 후](./create.md)에 생성한 ID입니다. | `2e8580db-6489-4726-96de-e33f5f60295f` |
| `flowSpecificationId` | 흐름 사양 ID `RestStorageToAEP`입니다. **고정 값**&#x200B;입니다. | `6499120c-0b15-42dc-936e-847ea3c24d72` |
| `targetConnectionSpecId` | 수집된 데이터가 도착하는 데이터 레이크의 대상 연결 ID입니다. **고정 값**&#x200B;입니다. | `c604ff05-7f1a-43c0-8e18-33bf874cb11c` |
| `verifyWatTimeInSecond` | 흐름 실행이 완료되었는지 확인할 때 따르는 지정된 시간 간격입니다. | `40` |
| `startTime` | 데이터 흐름의 지정된 시작 시간입니다. 시작 시간은 unix 시간으로 포맷해야 합니다. | `1597784298` |

환경 변수를 모두 제공했으면 [!DNL Postman] 인터페이스를 사용하여 컬렉션 실행을 시작할 수 있습니다. [!DNL Postman] 인터페이스에서 [!DNL Sources SSSs Verification Collection] 옆의 생략 부호(**...**)를 선택한 다음 **컬렉션 실행**&#x200B;을 선택합니다.

![runner](../assets/runner.png)

데이터 흐름의 실행 순서를 구성할 수 있는 [!DNL Runner] 인터페이스가 나타납니다. **SSS 확인 컬렉션 실행**&#x200B;을 선택하여 컬렉션을 실행합니다.

>[!NOTE]
>
>Experience Platform UI에서 소스 모니터링 대시보드를 사용하려면 실행 순서 검사 목록에서 **흐름 삭제**&#x200B;를 비활성화할 수 있습니다. 그러나 테스트를 완료한 후에는 테스트 흐름이 삭제되었는지 확인해야 합니다.

![run-collection](../assets/run-collection.png)

## 소스 제출

소스가 전체 워크플로우를 완료할 수 있으면 계속 Adobe 담당자에게 연락하여 소스를 제출하여 통합할 수 있습니다.
