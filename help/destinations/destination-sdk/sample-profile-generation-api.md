---
description: 이 페이지에서는 대상 테스트에 사용할 샘플 프로필을 생성하기 위해 '/authoring/sample-profiles' API 종단점을 사용하여 수행할 수 있는 모든 API 작업을 나열하고 설명합니다.
title: 샘플 프로필 생성 API 작업
exl-id: 5f1cd00a-8eee-4454-bcae-07b05afa54af
source-git-commit: 2ed132cd16db64b5921c5632445956f750fead56
workflow-type: tm+mt
source-wordcount: '833'
ht-degree: 2%

---

# 샘플 프로필 생성 API 작업 {#sample-profile-api-operations}

>[!IMPORTANT]
>
>**API 엔드포인트**:  `https://platform.adobe.io/data/core/activation/authoring/sample-profiles`

이 페이지에서는 `/authoring/sample-profiles` API 종단점을 사용하여 수행할 수 있는 모든 API 작업을 나열하고 설명합니다.

이 API 엔드포인트를 사용하면 사용할 샘플 프로필을 생성할 수 있습니다.
* 메시지 변환 템플릿을 테스트할 때 [메시지 변환 템플릿을 만들고 테스트합니다](./create-template.md).
* 대상이 올바르게 구성되었는지 테스트할 때 [대상 구성을 테스트합니다](./test-destination.md).

Adobe XDM 소스 스키마 또는 대상에서 지원하는 대상 스키마를 기반으로 샘플 프로필을 생성할 수 있습니다. Adobe XDM 소스 스키마와 대상 스키마의 차이점을 이해하려면 [메시지 형식](./message-format.md) 문서를 참조하십시오.

## 샘플 프로필 생성 API 작업 시작 {#get-started}

계속하기 전에 필요한 대상 작성 권한 및 필수 헤더를 가져오는 방법을 포함하여 API를 성공적으로 호출하기 위해 알고 있어야 하는 중요한 정보가 필요하면 [시작 안내서](./getting-started.md)를 검토하십시오.

## 소스 스키마를 기반으로 샘플 프로필 생성 {#generate-sample-profiles-source-schema}

>[!IMPORTANT]
>
>[대상](./test-destination.md)을 테스트할 때 여기에 생성된 샘플 프로필을 HTTP 호출에 추가합니다.

`authoring/sample-profiles/` 종단점에 GET 요청을 하고 테스트할 대상 구성을 기반으로 만든 대상 인스턴스의 ID를 제공하여 소스 스키마를 기반으로 샘플 프로필을 생성할 수 있습니다.

>[!TIP]
>
>* 대상과의 연결을 검색할 때 URL에서 여기서 사용해야 하는 대상 인스턴스 ID를 가져옵니다.
   >![UI 이미지 대상 인스턴스 ID를 가져오는 방법](./assets/get-destination-instance-id.png)


**API 형식**


```http
GET authoring/sample-profiles?destinationInstanceId={DESTINATION_INSTANCE_ID}&count={COUNT}
```

| 쿼리 매개 변수 | 설명 |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | 샘플 프로필을 생성하는 대상 인스턴스의 ID입니다. |
| `{COUNT}` | *선택 사항입니다*. 생성 중인 샘플 프로필 수입니다. 매개 변수는 `1 - 1000` 사이에 값을 사용할 수 있습니다. <br> count 매개 변수를 지정하지 않으면 생성된 프로필의 기본 수는 대상 서버 구성 `maxUsersPerRequest` 의 값 [으로 결정됩니다](./destination-server-api.md#create). 이 속성이 정의되지 않으면 Adobe이 하나의 샘플 프로필을 생성합니다. |

{style=&quot;table-layout:auto&quot;}


**요청**

다음 요청은 `{DESTINATION_INSTANCE_ID}` 및 `{COUNT}` 쿼리 매개 변수로 구성된 샘플 프로필을 생성합니다.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationInstanceId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

성공적인 응답은 소스 XDM 스키마에 해당하는 세그먼트 멤버십, ID 및 프로필 속성을 사용하여 지정된 수의 샘플 프로필과 함께 HTTP 상태 200을 반환합니다.

>[!TIP]
>
> 응답에서는 대상 인스턴스에 사용되는 세그먼트 멤버십, ID 및 프로필 속성만 반환합니다. 소스 스키마에 다른 필드가 있더라도 이러한 필드는 무시됩니다.

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
| `segmentMembership` | 개인의 세그먼트 멤버십을 설명하는 맵 개체입니다. `segmentMembership`에 대한 자세한 내용은 [세그먼트 멤버십 세부 정보](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/segmentation.html)를 참조하십시오. |
| `lastQualificationTime` | 이 프로필이 세그먼트에 대해 자격이 있는 마지막 시간의 타임스탬프입니다. |
| `xdm:status` | 세그먼트 멤버십이 현재 요청의 일부로 실현되었는지 여부를 나타냅니다. 다음 값이 허용됩니다. <ul><li>`existing`: 프로필은 요청 전에 이미 세그먼트의 일부였으며 계속해서 멤버십을 유지합니다.</li><li>`realized`: 프로필이 현재 요청의 일부로 세그먼트를 입력하고 있습니다.</li><li>`exited`: 프로필이 현재 요청의 일부로 세그먼트를 종료하고 있습니다.</li></ul> |
| `identityMap` | 연관된 네임스페이스와 함께 개인의 다양한 ID 값을 설명하는 맵 유형 필드입니다. `identityMap`에 대한 자세한 내용은 [스키마 컴포지션](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=en#identityMap)을 참조하십시오. |

{style=&quot;table-layout:auto&quot;}

## 대상 스키마를 기반으로 샘플 프로필 생성 {#generate-sample-profiles-target-schema}

>[!IMPORTANT]
>
>템플릿을 작성할 때 여기서 생성한 샘플 프로필을 [렌더링 템플릿 단계에서 사용합니다](./render-template-api.md#multiple-profiles-with-body).

대상 스키마를 기반으로 하여 샘플 프로필을 생성하여 `authoring/sample-profiles/` 종단점에 GET을 요청하고 템플릿을 만드는 데 따라 대상 구성의 대상 ID를 제공할 수 있습니다.

>[!TIP]
>
>* 여기서 사용해야 하는 대상 ID는 `/destinations` 종단점을 사용하여 만든 대상 구성에 해당하는 `instanceId` 입니다. [대상 구성 API 참조](./destination-configuration-api.md#retrieve-list)를 참조하십시오.


**API 형식**


```http
GET authoring/sample-profiles?destinationId={DESTINATION_ID}&count={COUNT}
```

| 쿼리 매개 변수 | 설명 |
| -------- | ----------- |
| `{DESTINATION_ID}` | 샘플 프로필을 생성하는 대상 구성의 ID입니다. |
| `{COUNT}` | *선택 사항입니다*. 생성 중인 샘플 프로필 수입니다. 매개 변수는 `1 - 1000` 사이에 값을 사용할 수 있습니다. <br> count 매개 변수를 지정하지 않으면 생성된 프로필의 기본 수는 대상 서버 구성 `maxUsersPerRequest` 의 값 [으로 결정됩니다](./destination-server-api.md#create). 이 속성이 정의되지 않으면 Adobe이 하나의 샘플 프로필을 생성합니다. |

{style=&quot;table-layout:auto&quot;}

**요청**

다음 요청은 `{DESTINATION_ID}` 및 `{COUNT}` 쿼리 매개 변수로 구성된 샘플 프로필을 생성합니다.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/sample-profiles?destinationId=49966037-32cd-4457-a105-2cbf9c01826a&count=3' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {IMS_ORG}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

성공적인 응답은 대상 XDM 스키마에 해당하는 세그먼트 멤버십, ID 및 프로필 속성을 사용하여 지정된 수의 샘플 프로필과 함께 HTTP 상태 200을 반환합니다.

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

대상 SDK API 엔드포인트는 일반 Experience Platform API 오류 메시지 원칙을 따릅니다. 플랫폼 문제 해결 안내서에서 [API 상태 코드](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) 및 [요청 헤더 오류](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors)를 참조하십시오.

## 다음 단계

이 문서를 읽은 후에는 이제 [메시지 변환 템플릿을 테스트하거나 ](./create-template.md) 대상이 올바르게 구성되어 있는지 테스트할 때 사용할 샘플 프로필을 생성하는 방법을 알 수 있습니다](./test-destination.md).[
