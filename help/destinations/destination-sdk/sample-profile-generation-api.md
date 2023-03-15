---
description: 이 페이지에서는 대상 테스트에 사용할 샘플 프로필을 생성하기 위해 '/authoring/sample-profiles' API 끝점을 사용하여 수행할 수 있는 모든 API 작업을 나열하고 설명합니다.
title: 샘플 프로필 생성 API 작업
exl-id: 5f1cd00a-8eee-4454-bcae-07b05afa54af
source-git-commit: 789a3928379d200af292c722806f7ca72441d9f3
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 1%

---

# 샘플 프로필 생성 API 작업 {#sample-profile-api-operations}

>[!IMPORTANT]
>
>**API 엔드포인트**: `https://platform.adobe.io/data/core/activation/authoring/sample-profiles`

이 페이지에서는 다음을 사용하여 수행할 수 있는 모든 API 작업을 나열하고 설명합니다. `/authoring/sample-profiles` API 엔드포인트.

## API에 따라 다른 프로필 유형 생성 {#different-profiles-different-apis}

>[!IMPORTANT]
>
>이 API 끝점을 사용하여 두 개의 별도 사용 사례에 대한 샘플 프로필을 생성합니다. 다음과 같은 작업을 수행할 수 있습니다.
>* 사용할 프로필 생성 [메시지 변환 템플릿 만들기 및 테스트](./create-template.md) - 를 사용하여 *대상 ID* 를 쿼리 매개 변수로 사용하십시오.
>* 을(를) 호출할 때 사용할 프로필 생성 [대상이 올바르게 구성되었는지 테스트](./test-destination.md) - 를 사용하여 *대상 인스턴스 ID* 를 쿼리 매개 변수로 사용하십시오.


Adobe XDM 소스 스키마(대상을 테스트할 때 사용) 또는 대상에서 지원하는 대상 스키마(템플릿을 만들 때 사용)를 기반으로 샘플 프로필을 생성할 수 있습니다. Adobe XDM 소스 스키마와 대상 스키마 간의 차이점을 이해하려면 [메시지 포맷](./message-format.md) 기사.

샘플 프로필을 사용할 수 있는 목적은 서로 바꿀 수 없습니다. 다음을 기반으로 생성된 프로필 *대상 ID* 를 기반으로 생성된 메시지 변환 템플릿과 프로필을 만드는 데만 사용할 수 있습니다. *대상 인스턴스 ID* 은 대상 끝점을 테스트하는 데만 사용할 수 있습니다.

## 샘플 프로필 생성 API 작업 시작 {#get-started}

계속하기 전에 다음을 검토하십시오. [시작 안내서](./getting-started.md) 필수 대상 작성 권한 및 필수 헤더를 가져오는 방법을 포함하여 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보입니다.

## 대상을 테스트할 때 사용할 소스 스키마를 기반으로 샘플 프로필 생성 {#generate-sample-profiles-source-schema}

>[!IMPORTANT]
>
>다음과 같은 경우 여기에 생성된 샘플 프로필을 HTTP 호출에 추가합니다. [대상 테스트](./test-destination.md).

에 GET 요청을 하여 소스 스키마를 기반으로 샘플 프로필을 생성할 수 있습니다. `authoring/sample-profiles/` 끝점을 지정하고 테스트할 대상 구성을 기반으로 만든 대상 인스턴스의 ID를 제공합니다.

대상 인스턴스의 ID를 가져오려면 먼저 대상 테스트를 시도하기 전에 Experience Platform UI에서 대상에 대한 연결을 만들어야 합니다. 읽기 [대상 튜토리얼 활성화](/help/destinations/ui/activation-overview.md) 이 API에 사용할 대상 인스턴스 ID를 가져오는 방법은 아래 팁을 참조하십시오.

>[!TIP]
>
>* 대상으로 연결을 검색할 때 URL에서 여기에서 사용해야 하는 대상 인스턴스 ID를 가져옵니다.
   >![UI 이미지 대상 인스턴스 ID를 가져오는 방법](./assets/get-destination-instance-id.png)


**API 형식**


```http
GET authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={COUNT}
```

| 쿼리 매개 변수 | 설명 |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | 샘플 프로필을 생성하는 데 기준이 되는 대상 인스턴스의 ID입니다. |
| `{COUNT}` | *선택 사항입니다*. 생성 중인 샘플 프로필 수입니다. 매개 변수는 다음 범위의 값을 가질 수 있습니다. `1 - 1000`. <br> count 매개 변수를 지정하지 않으면 생성된 프로필의 기본 수가 `maxUsersPerRequest` 의 값 [대상 서버 구성](./destination-server-api.md#create). 이 속성이 정의되지 않으면 Adobe에서 샘플 프로필이 생성됩니다. |

{style="table-layout:auto"}


**요청**

다음 요청은 다음을 통해 구성된 샘플 프로필을 생성합니다. `{DESTINATION_INSTANCE_ID}` 및 `{COUNT}` 쿼리 매개 변수.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

성공적인 응답은 지정된 수의 샘플 프로필과 함께, 소스 XDM 스키마에 해당하는 세그먼트 멤버십, ID 및 프로필 속성이 포함된 HTTP 상태 200을 반환합니다.

>[!TIP]
>
> 응답에서는 대상 인스턴스에 사용된 세그먼트 멤버십, ID 및 프로필 속성만 반환합니다. 소스 스키마에 다른 필드가 있더라도 무시됩니다.

```json
[
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-7VEsJ"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-Y55JJ"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "03fb9938-8537-4b4c-87f9-9c4d413a0ee5": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591378Z",
                    "status": "realized"
                },
                "27e05542-d6a3-46c7-9c8e-d59d50229530": {
                    "lastQualificationTime": "2021-06-30T18:40:07.591380Z",
                    "status": "realized"
                }
            }
        },
        "personalEmail": {
            "address": "john.smith@abc.com"
        },
        "identityMap": {
            "ECID": [
                {
                    "id": "ECID-Nd9GK"
                }
            ]
        },
        "person": {
            "name": {
                "firstName": "string"
            }
        }
    }
]
```

| 속성 | 설명 |
| -------- | ----------- |
| `segmentMembership` | 개인의 세그먼트 멤버십을 설명하는 맵 개체입니다. 에 대한 자세한 내용 `segmentMembership`, 읽기 [세그먼트 멤버십 세부 정보](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html). |
| `lastQualificationTime` | 이 프로필이 세그먼트에 대해 마지막으로 적격한 타임스탬프입니다. |
| `xdm:status` | 세그먼트 멤버십이 현재 요청의 일부로 실현되었는지 여부를 나타내는 문자열 필드입니다. 다음 값이 허용됩니다. <ul><li>`existing`: 프로필은 요청 전에 이미 세그먼트에 속했으며 멤버십을 계속 유지합니다.</li><li>`realized`: 프로필이 현재 요청의 일부로 세그먼트를 입력하고 있습니다.</li><li>`exited`: 프로필이 현재 요청의 일부로 세그먼트를 종료합니다.</li></ul> |
| `identityMap` | 연관된 네임스페이스와 함께 개인에 대한 다양한 ID 값을 설명하는 맵 유형 필드입니다. 에 대한 자세한 내용 `identityMap`, 읽기 [스키마 구성 기준](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en#identityMap). |

{style="table-layout:auto"}

## 메시지 변환 템플릿을 만들 때 사용할 대상 스키마를 기반으로 샘플 프로필 생성 {#generate-sample-profiles-target-schema}

>[!IMPORTANT]
>
>여기에서 생성된 샘플 프로필을 사용하여 템플릿을 만듭니다. [렌더링 템플릿 단계](./render-template-api.md#multiple-profiles-with-body).

에 GET 요청을 하는 대상 스키마를 기반으로 샘플 프로필을 생성할 수 있습니다. `authoring/sample-profiles/` 엔드포인트 및 템플릿 생성 시 기준이 되는 대상 구성의 대상 ID 제공

>[!TIP]
>
>* 여기에서 사용해야 하는 대상 ID는 입니다. `instanceId` 대상 구성에 해당하며 `/destinations` 엔드포인트. 다음을 참조하십시오. [대상 구성 API 참조](./destination-configuration-api.md#retrieve-list).


**API 형식**


```http
GET authoring/sample-profiles?destinationId={DESTINATION_ID}&count={COUNT}
```

| 쿼리 매개 변수 | 설명 |
| -------- | ----------- |
| `{DESTINATION_ID}` | 샘플 프로필을 생성하는 데 기준이 되는 대상 구성의 ID입니다. |
| `{COUNT}` | *선택 사항입니다*. 생성 중인 샘플 프로필 수입니다. 매개 변수는 다음 범위의 값을 가질 수 있습니다. `1 - 1000`. <br> count 매개 변수를 지정하지 않으면 생성된 프로필의 기본 수가 `maxUsersPerRequest` 의 값 [대상 서버 구성](./destination-server-api.md#create). 이 속성이 정의되지 않으면 Adobe에서 샘플 프로필이 생성됩니다. |

{style="table-layout:auto"}

**요청**

다음 요청은 다음을 통해 구성된 샘플 프로필을 생성합니다. `{DESTINATION_ID}` 및 `{COUNT}` 쿼리 매개 변수.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

성공적인 응답은 지정된 수의 샘플 프로필과 함께, 세그먼트 멤버십, ID 및 대상 XDM 스키마에 해당하는 프로필 속성이 있는 HTTP 상태 200을 반환합니다.

```json
[
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609326Z",
                    "status": "existing"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609328Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609328Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-vizii"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-adKYs"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-t4sKv"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-C3enB"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-bfnbs"
                }
            ]
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609626Z",
                    "status": "existing"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609627Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609627Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-6YjGc"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-SfJ21"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-eQMWS"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-d3WzP"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-eWfFn"
                }
            ]
        }
    },
    {
        "segmentMembership": {
            "ups": {
                "segmentid1": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609823Z",
                    "status": "existing"
                },
                "segmentid3": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609824Z",
                    "status": "exited"
                },
                "segmentid2": {
                    "lastQualificationTime": "2021-06-30T18:42:27.609824Z",
                    "status": "realized"
                }
            }
        },
        "identityMap": {
            "phone_sha256": [
                {
                    "id": "phone_sha256-2PMjZ"
                }
            ],
            "gaid": [
                {
                    "id": "gaid-3aLez"
                }
            ],
            "idfa": [
                {
                    "id": "idfa-D2H1J"
                }
            ],
            "extern_id": [
                {
                    "id": "extern_id-i6PsF"
                }
            ],
            "email_lc_sha256": [
                {
                    "id": "email_lc_sha256-VPUtZ"
                }
            ]
        }
    }
]
```

## API 오류 처리 {#api-error-handling}

Destination SDK API 엔드포인트는 일반적인 Experience Platform API 오류 메시지 원칙을 따릅니다. 을(를) 참조하십시오 [API 상태 코드](../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../landing/troubleshooting.md#request-header-errors) 플랫폼 문제 해결 안내서에서 확인할 수 있습니다.

## 다음 단계

이제 이 문서를 읽고 다음과 같은 경우에 사용할 샘플 프로필을 생성하는 방법을 알 수 있습니다. [메시지 변환 템플릿 테스트](./create-template.md) 또는 다음과 같은 경우 [대상이 올바르게 구성되었는지 테스트](./test-destination.md).
