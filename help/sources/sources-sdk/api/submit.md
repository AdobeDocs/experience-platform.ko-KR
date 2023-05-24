---
keywords: Experience Platform;홈;인기 항목;소스;커넥터;소스 커넥터;소스 sdk;sdk;SDK
title: 소스 제출
description: 다음 문서에서는 Flow Service API를 사용하여 새 소스를 테스트 및 확인하고 셀프서비스 소스(일괄 처리 SDK)를 통해 새 소스를 통합하는 방법에 대한 단계를 제공합니다.
exl-id: 9e945ba1-51b6-40a9-b92f-e0a52b3f92fa
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 0%

---

# 소스 제출

셀프 서비스 소스(Batch SDK)를 사용하여 새 소스를 Adobe Experience Platform에 통합하는 마지막 단계는 소스를 테스트하여 확인하는 것입니다. 성공하면 Adobe 담당자에게 연락하여 새 소스를 제출할 수 있습니다.

다음 문서에서는 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## 시작하기

* Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 의 안내서를 참조하십시오. [platform API 시작하기](../../../landing/api-guide.md).
* Platform API에 대한 자격 증명을 생성하는 방법에 대한 자세한 내용은 다음 자습서를 참조하십시오. [Experience Platform API 인증 및 액세스](../../../landing/api-authentication.md).
* 설정 방법에 대한 자세한 정보 [!DNL Postman] platform API에 대해서는 다음 자습서를 참조하십시오. [개발자 콘솔 설정 및 [!DNL Postman]](../../../landing/postman.md).
* 테스트 및 디버깅 프로세스를 지원하려면 [여기에서 셀프 서비스 소스 확인 수집 및 환경](../assets/sdk-verification.zip) 아래에 설명된 단계를 수행합니다.

## 소스 테스트

소스를 테스트하려면 다음을 실행해야 합니다 [셀프 서비스 소스 확인 수집 및 환경](../assets/sdk-verification.zip) 날짜 [!DNL Postman] 를 사용하여 소스와 관련된 적절한 환경 변수를 제공할 수 있습니다.

테스트를 시작하려면 먼저 다음에서 컬렉션 및 환경을 설정해야 합니다. [!DNL Postman]. 그런 다음 테스트할 연결 사양 ID를 지정합니다.

### 분류에 사용할 `authSpecName`

연결 사양 ID를 입력한 후에는 다음을 지정해야 합니다. `authSpecName` 기본 연결에 사용하는 것입니다. 선택에 따라 다음 중 하나가 될 수 있습니다. `OAuth 2 Refresh Code` 또는  `Basic Authentication`. 을(를) 지정하고 나면 `authSpecName`그런 다음 환경에 필요한 자격 증명을 포함해야 합니다. 예를 들어, `authSpecName` 다음으로: `OAuth 2 Refresh Code`, OAuth 2에 필요한 자격 증명을 제공해야 합니다. `host` 및 `accessToken`.

### 분류에 사용할 `sourceSpec`

인증 사양 매개변수가 추가되면 다음에 소스 사양에서 필요한 속성을 추가해야 합니다. 필요한 속성은에서 찾을 수 있습니다. `sourceSpec.spec.properties`. 의 경우 [!DNL MailChimp Members] 아래 예제에서 필요한 속성은 다음과 같습니다. `listId`, 즉 `listId` 및에 해당하는 ID 값입니다. [!DNL Postman] 환경.

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
>아래의 모든 예제 변수는 업데이트해야 하는 자리 표시자 값이며, 단, `flowSpecificationId` 및 `targetConnectionSpecId`- 고정 값입니다.

| 매개변수 | 설명 | 예 |
| --- | --- | --- |
| `x-api-key` | Experience Platform API 호출을 인증하는 데 사용되는 고유 식별자입니다. 다음 튜토리얼 참조: [Experience Platform API 인증 및 액세스](../../../landing/api-authentication.md) 을(를) 검색하는 방법에 대한 자세한 내용은 `x-api-key`. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `x-gw-ims-org-id` | 제품 및 서비스를 소유하거나 라이선스를 부여하고 해당 구성원에 대한 액세스를 허용할 수 있는 법인 엔티티입니다. 다음 튜토리얼 참조: [개발자 콘솔 설정 및 [!DNL Postman]](../../../landing/postman.md) 을(를) 검색하는 방법에 대한 지침을 보려면 `x-gw-ims-org-id` 정보. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `authorizationToken` | Experience Platform API 호출을 완료하는 데 필요한 인증 토큰입니다. 다음 튜토리얼 참조: [Experience Platform API 인증 및 액세스](../../../landing/api-authentication.md) 을(를) 검색하는 방법에 대한 자세한 내용은 `authorizationToken`. | `Bearer authorizationToken` |
| `schemaId` | 소스 데이터를 플랫폼에서 사용하려면 타겟 스키마를 만들어 필요에 따라 소스 데이터를 구조화해야 합니다. 대상 XDM 스키마를 만드는 방법에 대한 자세한 단계는 다음 자습서를 참조하십시오. [api를 사용하여 스키마 만들기](../../../xdm/api/schemas.md). | `https://ns.adobe.com/{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `schemaVersion` | 스키마에 해당하는 고유 버전. | `application/vnd.adobe.xed-full-notext+json; version=1` |
| `schemaAltId` | 다음 `meta:altId` that is returned반환 with the  `schemaId` 새 스키마를 만들 때 | `_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `dataSetId` | Target 데이터 세트를 만드는 방법에 대한 자세한 단계는 의 자습서를 참조하십시오. [api를 사용하여 데이터 세트 만들기](../../../catalog/api/create-dataset.md). | `5f3c3cedb2805c194ff0b69a` |
| `mappings` | 매핑 세트를 사용하여 소스 스키마의 데이터를 대상 스키마의 데이터에 매핑하는 방법을 정의할 수 있습니다. 매핑을 만드는 방법에 대한 자세한 단계는 다음 자습서를 참조하십시오. [api를 사용하여 매핑 세트 만들기](../../../data-prep/api/mapping-set.md). | `[{"destinationXdmPath":"person.name.firstName","sourceAttribute":"email.email_id","identity":false,"version":0},{"destinationXdmPath":"person.name.lastName","sourceAttribute":"email.activity.action","identity":false,"version":0}]` |
| `mappingId` | 매핑 세트에 해당하는 고유 ID입니다. | `bf5286a9c1ad4266baca76ba3adc9366` |
| `connectionSpecId` | 소스에 해당하는 연결 사양 ID입니다. 다음에 생성한 ID입니다 [새 연결 사양 생성](./create.md). | `2e8580db-6489-4726-96de-e33f5f60295f` |
| `flowSpecificationId` | 의 흐름 사양 ID `RestStorageToAEP`. **고정 값입니다.**. | `6499120c-0b15-42dc-936e-847ea3c24d72` |
| `targetConnectionSpecId` | 수집된 데이터가 도착하는 데이터 레이크의 대상 연결 ID입니다. **고정 값입니다.**. | `c604ff05-7f1a-43c0-8e18-33bf874cb11c` |
| `verifyWatTimeInSecond` | 흐름 실행이 완료되었는지 확인할 때 따르는 지정된 시간 간격입니다. | `40` |
| `startTime` | 데이터 흐름의 지정된 시작 시간입니다. 시작 시간은 unix 시간으로 포맷해야 합니다. | `1597784298` |

모든 환경 변수를 제공했으면 다음을 사용하여 컬렉션 실행을 시작할 수 있습니다. [!DNL Postman] 인터페이스. 다음에서 [!DNL Postman] 인터페이스에서 줄임표(**...**) 옆에 [!DNL Sources SSSs Verification Collection] 다음을 선택합니다. **컬렉션 실행**.

![러너](../assets/runner.png)

다음 [!DNL Runner] 데이터 흐름의 실행 순서를 구성할 수 있는 인터페이스가 나타납니다. 선택 **SSS 확인 컬렉션 실행** 컬렉션을 실행합니다.

>[!NOTE]
>
>비활성화할 수 있습니다. **플로우 삭제** 플랫폼 UI에서 소스 모니터링 대시보드를 사용하려는 경우 실행 주문 체크리스트에서 다음을 수행합니다. 그러나 테스트를 완료한 후에는 테스트 흐름이 삭제되었는지 확인해야 합니다.

![실행 컬렉션](../assets/run-collection.png)

## 소스 제출

소스에서 전체 워크플로우를 완료할 수 있으면 계속 Adobe 담당자에게 연락하여 소스를 제출하여 통합할 수 있습니다.
