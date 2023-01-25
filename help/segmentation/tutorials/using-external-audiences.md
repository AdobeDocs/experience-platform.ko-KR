---
keywords: Experience Platform;홈;인기 있는 주제
solution: Experience Platform
title: 외부 대상 가져오기 및 사용
description: Adobe Experience Platform에서 외부 대상을 사용하는 방법을 배우려면 이 자습서를 따르십시오.
exl-id: 56fc8bd3-3e62-4a09-bb9c-6caf0523f3fe
source-git-commit: 57586104f1119f5cda926faf286c1663fbb0b240
workflow-type: tm+mt
source-wordcount: '1664'
ht-degree: 0%

---

# 외부 대상 가져오기 및 사용

Adobe Experience Platform은 외부 대상을 가져오는 기능을 지원하며, 이후 이 기능은 새 세그먼트 정의에 대한 구성 요소로 사용할 수 있습니다. 이 문서에서는 외부 대상을 가져오고 사용할 Experience Platform을 설정하는 자습서를 제공합니다.

## 시작하기

이 자습서에서는 다양한 자습서를 이해하고 있어야 합니다 [!DNL Adobe Experience Platform] 대상 세그먼트 만들기에 관련된 서비스입니다. 이 자습서를 시작하기 전에 다음 서비스에 대한 설명서를 검토하십시오.

- [세분화 서비스](../home.md): 실시간 고객 프로필 데이터에서 대상 세그먼트를 작성할 수 있습니다.
- [실시간 고객 프로필](../../profile/home.md): 여러 소스에서 집계된 데이터를 기반으로 통합된 실시간 소비자 프로필을 제공합니다.
- [XDM(경험 데이터 모델)](../../xdm/home.md): 플랫폼이 고객 경험 데이터를 구성하는 표준화된 프레임워크입니다. 세그멘테이션을 가장 잘 사용하려면 데이터가 [데이터 모델링 우수 사례](../../xdm/schema/best-practices.md).
- [데이터 세트](../../catalog/datasets/overview.md): Experience Platform의 데이터 지속성을 위한 스토리지 및 관리 구성입니다.
- [스트리밍 수집](../../ingestion/streaming-ingestion/overview.md): Experience Platform이 클라이언트 및 서버측 장치에서 데이터를 실시간으로 수집 및 저장하는 방법입니다.

### 세그먼트 데이터와 세그먼트 메타데이터

외부 대상을 가져오고 사용하기 전에 세그먼트 데이터와 세그먼트 메타데이터 간의 차이점을 이해하는 것이 중요합니다.

세그먼트 데이터는 세그먼트 자격 기준을 충족하는 프로필을 나타내며, 따라서 대상의 일부입니다.

세그먼트 메타데이터는 이름, 설명, 표현식(해당되는 경우), 작성 날짜, 마지막 수정 날짜 및 ID를 포함하는 세그먼트 자체에 대한 정보입니다. ID는 세그먼트 자격을 충족하고 결과 대상의 일부인 개별 프로필에 세그먼트 메타데이터를 연결합니다.

| 세그먼트 데이터 | 세그먼트 메타데이터 |
| ------------ | ---------------- |
| 세그먼트 자격을 충족하는 프로필 | 세그먼트 자체에 대한 정보 |

## 외부 대상을 위한 ID 네임스페이스 만들기

외부 대상을 사용하는 첫 번째 단계는 ID 네임스페이스를 만드는 것입니다. ID 네임스페이스를 사용하면 Platform에서 세그먼트가 시작되는 위치를 연결할 수 있습니다.

ID 네임스페이스를 만들려면 [identity namespace 안내서](../../identity-service/namespaces.md#manage-namespaces). ID 네임스페이스를 만들 때 ID 네임스페이스에 소스 세부 정보를 추가하고 해당 네임스페이스에 표시합니다 [!UICONTROL 유형] 로서의 **[!UICONTROL 비사용자 식별자]**.

![개인이 아닌 식별자는 ID 네임스페이스 만들기 모달에 강조 표시됩니다.](../images/tutorials/external-audiences/identity-namespace-info.png)

## 세그먼트 메타데이터에 대한 스키마 만들기

ID 네임스페이스를 만든 후 만들 세그먼트에 대한 새 스키마를 만들어야 합니다.

스키마 작성을 시작하려면 먼저 을 선택합니다 **[!UICONTROL 스키마]** 왼쪽 탐색 막대에서 을 클릭하고 **[!UICONTROL 스키마 만들기]** 스키마 작업 영역의 오른쪽 상단 모서리에서 을(를) 클릭합니다. 여기에서 을 선택합니다. **[!UICONTROL 찾아보기]** 사용 가능한 스키마 유형의 전체 선택을 확인합니다.

![스키마 만들기 와 찾아보기 가 모두 강조 표시됩니다.](../images/tutorials/external-audiences/create-schema-browse.png)

사전 정의된 클래스인 세그먼트 정의를 만들려면, **[!UICONTROL 기존 클래스 사용]**. 이제 **[!UICONTROL 세그먼트 정의]** 클래스, 그 다음 **[!UICONTROL 클래스 할당]**.

![세그먼트 정의 클래스가 강조 표시됩니다.](../images/tutorials/external-audiences/assign-class.png)

스키마가 만들어지면 세그먼트 ID가 포함될 필드를 지정해야 합니다. 이 필드는 기본 ID로 표시하고 이전에 만든 네임스페이스에 할당해야 합니다.

![선택한 필드를 기본 ID로 표시하는 확인란은 스키마 편집기에서 강조 표시됩니다.](../images/tutorials/external-audiences/mark-primary-identifier.png)

표시 후 `_id` 필드를 기본 ID로 선택하고 스키마 제목을 선택한 후 토글이 레이블이 지정됩니다 **[!UICONTROL 프로필]**. 선택 **[!UICONTROL 활성화]** 스키마를 활성화하려면 [!DNL Real-Time Customer Profile].

![프로파일에 대한 스키마를 활성화할 수 있는 토글이 스키마 편집기에서 강조 표시됩니다.](../images/tutorials/external-audiences/schema-profile.png)

이제 이 스키마는 사용자가 만든 비개인 ID 네임스페이스에 기본 ID가 지정된 프로필에 대해 활성화됩니다. 따라서 이 스키마를 사용하여 Platform에 가져온 세그먼트 메타데이터는 다른 사람 관련 프로필 데이터와 병합되지 않고 프로필에 수집됩니다.

## 스키마에 대한 데이터 세트 만들기

스키마를 구성한 후에는 세그먼트 메타데이터에 대한 데이터 세트를 만들어야 합니다.

데이터 세트를 만들려면 [데이터 세트 사용 안내서](../../catalog/datasets/user-guide.md#create). 다음을 수행해야 합니다 **[!UICONTROL 스키마에서 데이터 집합 만들기]** 옵션. 이전에 만든 스키마를 사용합니다.

![데이터 세트를 기반으로 할 스키마가 강조 표시됩니다.](../images/tutorials/external-audiences/select-schema.png)

데이터 세트를 만든 후 [데이터 세트 사용 안내서](../../catalog/datasets/user-guide.md#enable-profile) 실시간 고객 프로필에 대해 이 데이터 세트를 사용하도록 설정하려면 다음을 수행하십시오.

![프로필에 대한 스키마를 활성화하는 토글이 데이터 세트 활동 페이지에서 강조 표시됩니다.](../images/tutorials/external-audiences/dataset-profile.png)

## 대상 데이터 설정 및 가져오기

데이터 세트가 활성화되면 이제 UI를 통해 또는 Experience Platform API를 사용하여 데이터를 Platform으로 전송할 수 있습니다. 일괄 처리 또는 스트리밍 연결을 통해 이 데이터를 수집할 수 있습니다.

### 배치 연결을 사용하여 데이터 수집

배치 연결을 만들려면 일반 [로컬 파일 업로드 UI 안내서](../../sources/tutorials/ui/create/local-system/local-file-upload.md). 에서 수집 데이터를 사용할 수 있는 사용 가능한 소스의 전체 목록을 보려면 [소스 개요](../../sources/home.md).

### 스트리밍 연결을 사용하여 데이터 수집

스트리밍 연결을 만들려면 [API 자습서](../../sources/tutorials/api/create/streaming/http.md) 또는 [UI 자습서](../../sources/tutorials/ui/create/streaming/http.md).

스트리밍 연결을 만들었으면 데이터를 보낼 수 있는 고유한 스트리밍 종단점에 액세스할 수 있습니다. 이러한 종단점으로 데이터를 보내는 방법에 대해 알아보려면 [레코드 데이터 스트리밍에 대한 자습서](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![스트리밍 연결에 대한 스트리밍 끝점은 소스 세부 사항 페이지에 강조 표시됩니다.](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## 대상 메타데이터 구조

이제 연결을 만들면 데이터를 Platform에 수집할 수 있습니다.

외부 대상 페이로드의 메타데이터 샘플은 아래에 나와 있습니다.

```json
{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "source": {
            "name": "Sample External Audience"
        }
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "xdmEntity": {
            "_id": "{SEGMENT_ID}",
            "description": "Sample description",
            "identityMap": {
                "{IDENTITY_NAMESPACE}": [{
                    "id": "{}"
                }]
            },
            "segmentName" : "{SEGMENT_NAME}",
            "segmentStatus": "ACTIVE",
            "version": "1.0"
        }
    }
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `schemaRef` | 스키마 **반드시** 세그먼트 메타데이터에 대해서는 이전에 만든 스키마를 참조하십시오. |
| `datasetId` | 데이터 세트 ID **반드시** 방금 생성한 스키마에 대해서는 이전에 만든 데이터 세트를 참조하십시오. |
| `xdmEntity._id` | ID **반드시** 외부 대상으로 사용하는 것과 동일한 세그먼트 ID를 참조하십시오. |
| `xdmEntity.identityMap` | 이 섹션 **반드시** 이전에 만든 네임스페이스를 만들 때 사용되는 id 레이블을 포함합니다. |
| `{IDENTITY_NAMESPACE}` | 이전에 만든 ID 네임스페이스의 레이블입니다. 따라서 예를 들어 ID 네임스페이스를 &quot;externalAudience&quot;라고 호출하면 배열의 키로 이 네임스페이스를 사용합니다. |
| `segmentName` | 외부 대상을 세그먼트화할 세그먼트의 이름입니다. |

## 가져온 대상을 사용하여 세그먼트 작성

가져온 대상을 설정한 후에는 세그먼테이션 프로세스의 일부로 사용할 수 있습니다. 외부 대상을 찾으려면 세그먼트 빌더로 이동하여 를 선택합니다 **[!UICONTROL 대상]** 탭에서 다음을 수행합니다. **[!UICONTROL 필드]** 섹션을 참조하십시오.

![세그먼트 빌더에 있는 외부 대상 선택기가 강조 표시됩니다.](../images/tutorials/external-audiences/external-audiences.png)

## 다음 단계

세그먼트에서 외부 대상을 사용할 수 있으므로 세그먼트 빌더 를 사용하여 세그먼트를 만들 수 있습니다. 세그먼트를 만드는 방법을 알아보려면 [세그먼트 만들기 튜토리얼](./create-a-segment.md).

## 부록

가져온 외부 대상 메타데이터를 사용하고 세그먼트를 만드는 데 사용하는 것 외에도 외부 세그먼트 멤버십을 Platform으로 가져올 수도 있습니다.

### 외부 세그먼트 멤버십 대상 스키마 설정

스키마 작성을 시작하려면 먼저 을 선택합니다 **[!UICONTROL 스키마]** 왼쪽 탐색 막대에서 을 클릭하고 **[!UICONTROL 스키마 만들기]** 스키마 작업 영역의 오른쪽 상단 모서리에서 을(를) 클릭합니다. 여기에서 을 선택합니다. **[!UICONTROL XDM 개별 프로필]**.

![XDM 개별 프로필 영역이 강조 표시됩니다.](../images/tutorials/external-audiences/create-schema-profile.png)

스키마가 만들어지면 스키마의 일부로 세그먼트 멤버십 필드 그룹을 추가해야 합니다. 이렇게 하려면 을(를) 선택합니다. [!UICONTROL 세그먼트 멤버십 세부 정보], 그 다음 [!UICONTROL 필드 그룹 추가].

![세그먼트 멤버십 세부 사항 필드 그룹이 강조 표시됩니다.](../images/tutorials/external-audiences/segment-membership-details.png)

또한 스키마가 **[!UICONTROL 프로필]**. 이렇게 하려면 필드를 기본 ID로 표시해야 합니다.

![프로파일에 대한 스키마를 활성화할 수 있는 토글이 스키마 편집기에서 강조 표시됩니다.](../images/tutorials/external-audiences/external-segment-profile.png)

### 데이터 세트 설정

스키마를 만들면 데이터 세트를 만들어야 합니다.

데이터 세트를 만들려면 [데이터 세트 사용 안내서](../../catalog/datasets/user-guide.md#create). 다음을 수행해야 합니다 **[!UICONTROL 스키마에서 데이터 집합 만들기]** 옵션. 이전에 만든 스키마를 사용합니다.

![데이터베이스를 만드는 데 사용하는 스키마가 강조 표시됩니다.](../images/tutorials/external-audiences/select-schema.png)

데이터 세트를 만든 후 [데이터 세트 사용 안내서](../../catalog/datasets/user-guide.md#enable-profile) 실시간 고객 프로필에 대해 이 데이터 세트를 사용하도록 설정하려면 다음을 수행하십시오.

![프로필에 대한 스키마를 활성화하는 토글은 데이터 세트 만들기 워크플로우에서 강조 표시됩니다.](../images/tutorials/external-audiences/dataset-profile.png)

## 외부 대상 멤버십 데이터 설정 및 가져오기

데이터 세트가 활성화되면 이제 UI를 통해 또는 Experience Platform API를 사용하여 데이터를 Platform으로 전송할 수 있습니다. 일괄 처리 또는 스트리밍 연결을 통해 이 데이터를 수집할 수 있습니다.

### 배치 연결을 사용하여 데이터 수집

배치 연결을 만들려면 일반 [로컬 파일 업로드 UI 안내서](../../sources/tutorials/ui/create/local-system/local-file-upload.md). 에서 수집 데이터를 사용할 수 있는 사용 가능한 소스의 전체 목록을 보려면 [소스 개요](../../sources/home.md).

### 스트리밍 연결을 사용하여 데이터 수집

스트리밍 연결을 만들려면 [API 자습서](../../sources/tutorials/api/create/streaming/http.md) 또는 [UI 자습서](../../sources/tutorials/ui/create/streaming/http.md).

스트리밍 연결을 만들었으면 데이터를 보낼 수 있는 고유한 스트리밍 종단점에 액세스할 수 있습니다. 이러한 종단점으로 데이터를 보내는 방법에 대해 알아보려면 [레코드 데이터 스트리밍에 대한 자습서](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![스트리밍 연결에 대한 스트리밍 끝점은 소스 세부 사항 페이지에 강조 표시됩니다.](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## 세그먼트 멤버십 구조

이제 연결을 만들면 데이터를 Platform에 수집할 수 있습니다.

외부 대상 멤버십 페이로드 샘플은 아래에 나와 있습니다.

```json
{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "source": {
            "name": "Sample External Audience Membership"
        }
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "xdmEntity": {
            "_id": "{UNIQUE_ID}",
            "description": "Sample description",
            "{TENANT_NAME}": {
                "identities": {
                    "{SCHEMA_IDENTITY}": "sample-id"
                }
            },
            "personId" : "sample-name",
            "segmentMembership": {
                "{IDENTITY_NAMESPACE}": {
                    "{EXTERNAL_IDENTITY}": {
                        "status": "realized",
                        "lastQualificationTime": "2022-03-14T:00:00:00Z"
                    }
                }
            }
        }
    }
}
```

| 속성 | 설명 |
| -------- | ----------- |
| `schemaRef` | 스키마 **반드시** 세그먼트 멤버십 데이터에 대해서는 이전에 만든 스키마를 참조하십시오. |
| `datasetId` | 데이터 세트 ID **반드시** 방금 생성한 멤버십 스키마에 대해서는 이전에 만든 데이터 세트를 참조하십시오. |
| `xdmEntity._id` | 데이터 집합 내의 레코드를 고유하게 식별하는 데 사용되는 적절한 ID입니다. |
| `{TENANT_NAME}.identities` | 이 섹션은 사용자 지정 ID 필드 그룹을 이전에 가져온 사용자와 연결하는 데 사용됩니다. |
| `segmentMembership.{IDENTITY_NAMESPACE}` | 이전에 만든 사용자 지정 ID 네임스페이스의 레이블입니다. 따라서 예를 들어 ID 네임스페이스를 &quot;externalAudience&quot;라고 호출하면 배열의 키로 이 네임스페이스를 사용합니다. |

>[!NOTE]
>
>기본적으로 외부 대상 멤버십은 30일 동안만 유지됩니다. 30일 이상 보관하려면 `validUntil` 대상 데이터를 수집하는 동안 필드를 작성합니다. 이 필드에 대한 자세한 내용은 [세그먼트 멤버십 세부 정보 스키마 필드 그룹](../../xdm/field-groups/profile/segmentation.md).