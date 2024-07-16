---
title: Source 테스트 및 제출
description: 다음 문서에서는 Flow Service API를 사용하여 새 소스를 테스트 및 확인하고 셀프서비스 소스(Streaming SDK)를 통해 새 소스를 통합하는 방법에 대한 단계를 제공합니다.
exl-id: 2ae0c3ad-1501-42ab-aaaa-319acea94ec2
badge: Beta
source-git-commit: 256857103b4037b2cd7b5b52d6c5385121af5a9f
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 0%

---

# 소스 테스트 및 제출

>[!NOTE]
>
>Streaming SDK는 베타 버전입니다. 베타 레이블 소스를 사용하는 방법에 대한 자세한 내용은 [소스 개요](../../home.md#terms-and-conditions)를 참조하십시오.

셀프 서비스 소스(Streaming SDK)를 사용하여 새 소스를 Adobe Experience Platform에 통합하는 마지막 단계는 새 소스를 테스트하고 제출하는 것입니다. 연결 사양을 완료하고 스트리밍 흐름 사양을 업데이트하면 API 또는 UI를 통해 소스의 기능 테스트를 시작할 수 있습니다. 성공하면 Adobe 담당자에게 연락하여 새 소스를 제출할 수 있습니다.

다음 문서에서는 [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/)를 사용하여 소스를 테스트하고 디버깅하는 방법에 대한 단계를 제공합니다.

## 시작하기

* Platform API를 성공적으로 호출하는 방법에 대한 자세한 내용은 [Platform API 시작](../../../landing/api-guide.md)에 대한 안내서를 참조하십시오.
* Platform API에 대한 자격 증명을 생성하는 방법에 대한 자세한 내용은 [Experience Platform API 인증 및 액세스](../../../landing/api-authentication.md)에 대한 자습서를 참조하십시오.
* 플랫폼 API용 [!DNL Postman]을(를) 설정하는 방법에 대한 자세한 내용은 [개발자 콘솔 설정 및 [!DNL Postman]](../../../landing/postman.md)에 대한 자습서를 참조하십시오.
* 테스트 및 디버깅 프로세스에 도움이 되도록 [여기에서 셀프 서비스 원본 확인 컬렉션 및 환경을 다운로드](../assets/sdk-verification.zip)하고 아래에 설명된 단계를 수행합니다.

## API를 사용하여 소스 테스트

API를 사용하여 소스를 테스트하려면 해당 소스와 관련된 적절한 환경 변수를 제공하면서 [!DNL Postman]에서 [셀프 서비스 소스 확인 컬렉션 및 환경](../assets/sdk-verification.zip)을 실행해야 합니다.

테스트를 시작하려면 먼저 [!DNL Postman]에서 컬렉션 및 환경을 설정해야 합니다. 그런 다음 테스트할 연결 사양 ID를 지정합니다.

>[!NOTE]
>
>아래의 예제 변수는 모두 업데이트해야 하는 자리 표시자 값입니다. 단, 고정 값인 `flowSpecificationId`과(와) `targetConnectionSpecId`은(는) 예외입니다.

| 매개변수 | 설명 | 예 |
| --- | --- | --- |
| `x-api-key` | Experience Platform API 호출을 인증하는 데 사용되는 고유 식별자입니다. `x-api-key`을(를) 검색하는 방법에 대한 자세한 내용은 [Experience Platform API 인증 및 액세스](../../../landing/api-authentication.md)에 대한 자습서를 참조하십시오. | `c8d9a2f5c1e03789bd22e8efdd1bdc1b` |
| `x-gw-ims-org-id` | 제품 및 서비스를 소유하거나 라이선스를 부여하고 해당 구성원에 대한 액세스를 허용할 수 있는 법인 엔티티입니다. `x-gw-ims-org-id` 정보를 검색하는 방법에 대한 지침은 [개발자 콘솔 설정 및 [!DNL Postman]](../../../landing/postman.md)에 대한 자습서를 참조하십시오. | `ABCEH0D9KX6A7WA7ATQE0TE@adobeOrg` |
| `authorizationToken` | Experience Platform API 호출을 완료하는 데 필요한 인증 토큰입니다. `authorizationToken`을(를) 검색하는 방법에 대한 자세한 내용은 [Experience Platform API 인증 및 액세스](../../../landing/api-authentication.md)에 대한 자습서를 참조하십시오. | `Bearer authorizationToken` |
| `schemaId` | 소스 데이터를 플랫폼에서 사용하려면 타겟 스키마를 만들어 필요에 따라 소스 데이터를 구조화해야 합니다. 대상 XDM 스키마를 만드는 방법에 대한 자세한 단계는 [API를 사용하여 스키마 만들기](../../../xdm/api/schemas.md)에 대한 자습서를 참조하십시오. | `https://ns.adobe.com/{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `schemaVersion` | 스키마에 해당하는 고유 버전. | `application/vnd.adobe.xed-full-notext+json; version=1` |
| `schemaAltId` | 새 스키마를 만들 때 `schemaId`과(와) 함께 반환되는 `meta:altId`입니다. | `_{TENANT_ID}.schemas.0ef4ce0d390f0809fad490802f53d30b` |
| `dataSetId` | 대상 데이터 집합을 만드는 방법에 대한 자세한 단계는 [API를 사용하여 데이터 집합 만들기](../../../catalog/api/create-dataset.md)에 대한 자습서를 참조하십시오. | `5f3c3cedb2805c194ff0b69a` |
| `mappings` | 매핑 세트를 사용하여 소스 스키마의 데이터를 대상 스키마의 데이터에 매핑하는 방법을 정의할 수 있습니다. 매핑을 만드는 방법에 대한 자세한 단계는 [API를 사용하여 매핑 집합을 만드는 방법](../../../data-prep/api/mapping-set.md)에 대한 자습서를 참조하십시오. | `[{"destinationXdmPath":"person.name.firstName","sourceAttribute":"email.email_id","identity":false,"version":0},{"destinationXdmPath":"person.name.lastName","sourceAttribute":"email.activity.action","identity":false,"version":0}]` |
| `mappingId` | 매핑 세트에 해당하는 고유 ID입니다. | `bf5286a9c1ad4266baca76ba3adc9366` |
| `connectionSpecId` | 소스에 해당하는 연결 사양 ID입니다. [새 연결 사양을 만든 후](./create.md)에 생성한 ID입니다. | `2e8580db-6489-4726-96de-e33f5f60295f` |
| `flowSpecificationId` | 흐름 사양 ID `GenericStreamingAEP`입니다. **고정 값**&#x200B;입니다. | `e77fde5a-22a8-11ed-861d-0242ac120002` |
| `targetConnectionSpecId` | 수집된 데이터가 도착하는 데이터 레이크의 대상 연결 ID입니다. **고정 값**&#x200B;입니다. | `c604ff05-7f1a-43c0-8e18-33bf874cb11c` |
| `verifyWatTimeInSecond` | 흐름 실행이 완료되었는지 확인할 때 따르는 지정된 시간 간격입니다. | `40` |
| `startTime` | 데이터 흐름의 지정된 시작 시간입니다. 시작 시간은 unix 시간으로 포맷해야 합니다. | `1597784298` |

환경 변수를 모두 제공했으면 [!DNL Postman] 인터페이스를 사용하여 컬렉션 실행을 시작할 수 있습니다. [!DNL Postman] 인터페이스에서 [!DNL Sources SSSs Verification Collection] 옆의 생략 부호(**...**)를 선택한 다음 **컬렉션 실행**&#x200B;을 선택합니다.

![runner](../assets/runner.png)

데이터 흐름의 실행 순서를 구성할 수 있는 [!DNL Runner] 인터페이스가 나타납니다. **SSS 확인 컬렉션 실행**&#x200B;을 선택하여 컬렉션을 실행합니다.

>[!NOTE]
>
>플랫폼 UI에서 소스 모니터링 대시보드를 사용하려면 실행 순서 검사 목록에서 **흐름 삭제**&#x200B;를 비활성화할 수 있습니다. 그러나 테스트를 완료한 후에는 테스트 흐름이 삭제되었는지 확인해야 합니다.

![run-collection](../assets/run-collection.png)

## UI를 사용하여 소스 테스트

UI에서 소스를 테스트하려면 Platform UI에서 조직 샌드박스의 소스 카탈로그로 이동합니다. 여기에서 새 소스가 *스트리밍* 범주 아래에 표시되는 것을 볼 수 있습니다.

이제 샌드박스에서 새 소스를 사용할 수 있으므로 소스 워크플로우에 따라 기능을 테스트해야 합니다. 시작하려면 **[!UICONTROL 설정]**&#x200B;을 선택하세요.

![새 스트리밍 원본을 표시하는 원본 카탈로그입니다.](../assets/testing/catalog-test.png)

[!UICONTROL 데이터 추가] 단계가 나타납니다. 소스가 데이터를 스트리밍할 수 있는지 테스트하려면 인터페이스 왼쪽을 사용하여 [샘플 JSON 데이터](../assets/testing/raw.json.zip)를 업로드하십시오. 데이터가 업로드되면 인터페이스의 오른쪽이 데이터 파일 계층 구조의 미리보기로 업데이트됩니다. 계속하려면 **[!UICONTROL 다음]**&#x200B;을(를) 선택하십시오.

![수집 전에 데이터를 업로드하고 미리 볼 수 있는 소스 워크플로우의 데이터 추가 단계입니다.](../assets/testing/add-data-test.png)

[!UICONTROL 데이터 흐름 세부 정보] 페이지에서 기존 데이터 집합을 사용할지 새 데이터 집합을 사용할지 여부를 선택할 수 있습니다. 이 프로세스 중에 프로필에 수집될 데이터를 구성하고 [!UICONTROL 오류 진단] 및 [!UICONTROL 부분 수집]과 같은 설정을 활성화할 수도 있습니다.

테스트를 위해 **[!UICONTROL 새 데이터 세트]**&#x200B;를 선택하고 출력 데이터 세트 이름을 제공하십시오. 이 단계에서는 데이터 세트에 정보를 추가하기 위한 선택적 설명을 제공할 수도 있습니다. 그런 다음 [!UICONTROL 고급 검색] 옵션을 사용하거나 드롭다운 메뉴에서 기존 스키마 목록을 스크롤하여 매핑할 스키마를 선택합니다. 스키마를 선택하면 데이터 흐름의 이름과 설명을 입력합니다.

완료되면 **[!UICONTROL 다음]**&#x200B;을 선택합니다.

![원본 워크플로의 데이터 흐름 세부 정보 단계입니다.](../assets/testing/dataflow-details-test.png)

소스 스키마의 소스 필드를 대상 스키마의 해당 대상 XDM 필드에 매핑할 수 있는 인터페이스를 제공하는 [!UICONTROL 매핑] 단계가 나타납니다.

Platform은 선택한 대상 스키마 또는 데이터 세트를 기반으로 자동 매핑된 필드에 대한 지능형 권장 사항을 제공합니다. 사용 사례에 맞게 매핑 규칙을 수동으로 조정할 수 있습니다. 필요에 따라 필드를 직접 매핑하도록 선택하거나 데이터 준비 함수를 사용하여 소스 데이터를 변환하여 계산된 값 또는 계산된 값을 파생할 수 있습니다. 매퍼 인터페이스 및 계산된 필드 사용에 대한 포괄적인 단계는 [데이터 준비 UI 안내서](../../../data-prep/ui/mapping.md)를 참조하십시오.

원본 데이터가 성공적으로 매핑되면 **[!UICONTROL 다음]**&#x200B;을(를) 선택하십시오.

![원본 워크플로의 매핑 단계입니다.](../assets/testing/mapping-test.png)

새 데이터 흐름을 만들기 전에 검토할 수 있는 **[!UICONTROL 검토]** 단계가 나타납니다. 세부 사항은 다음 범주 내에서 그룹화됩니다.

* **[!UICONTROL 연결]**: 사용 중인 스트리밍 클라우드 저장소 원본과 관련된 계정 이름, 원본 유형 및 기타 정보를 표시합니다.
* **[!UICONTROL 데이터 집합 및 맵 필드 할당]**: 데이터 흐름에 사용 중인 대상 데이터 집합 및 스키마를 표시합니다.

데이터 흐름을 검토한 후 **[!UICONTROL 완료]**&#x200B;를 선택하고 데이터 흐름이 만들어지도록 잠시 기다립니다.

![원본 워크플로의 검토 단계입니다.](../assets/testing/review-test.png)

마지막으로 데이터 흐름의 스트리밍 끝점을 검색해야 합니다. 이 끝점은 Webhook에 가입하는 데 사용되며 스트리밍 소스에서 Experience Platform과 통신할 수 있습니다. 스트리밍 끝점을 검색하려면 방금 만든 데이터 흐름의 [!UICONTROL 데이터 흐름 활동] 페이지로 이동한 다음, [!UICONTROL 속성] 패널 아래쪽에서 끝점을 복사합니다.

![데이터 흐름 활동의 스트리밍 끝점입니다.](../assets/testing/endpoint-test.png)

## 소스 제출

소스가 전체 워크플로우를 완료할 수 있으면 계속 Adobe 담당자에게 연락하여 다른 Experience Platform 조직 간 통합을 위해 소스를 제출할 수 있습니다.
