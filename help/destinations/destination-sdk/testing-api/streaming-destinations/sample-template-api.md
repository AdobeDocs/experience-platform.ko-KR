---
description: 대상 테스트 API를 사용하여 대상에 대한 테스트 메시지 변형 템플릿을 생성하는 방법을 알아봅니다.
title: 샘플 메시지 변환 템플릿 생성
exl-id: d18a06f7-0c3a-4b4d-a7d5-011690d00e2c
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 1%

---


# 샘플 메시지 변환 템플릿 생성 {#get-sample-template-api-operations}

>[!IMPORTANT]
>
>**API 끝점**: `https://platform.adobe.io/data/core/activation/authoring/testing/template/sample`

이 페이지에서는 `/authoring/testing/template/sample` API 끝점을 사용하여 대상에 대한 [메시지 변환 템플릿](../../functionality/destination-server/message-format.md#using-templating)을(를) 생성하기 위해 수행할 수 있는 모든 API 작업을 나열하고 설명합니다. 이 끝점에서 지원하는 기능에 대한 설명은 [템플릿 만들기](create-template.md)를 참조하십시오.

## 샘플 템플릿 API 작업 시작 {#get-started}

계속하기 전에 [시작 안내서](../../getting-started.md)에서 필요한 대상 작성 권한 및 필수 헤더를 얻는 방법을 포함하여 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보를 검토하십시오.

## 샘플 템플릿 가져오기 {#generate-sample-template}

`authoring/testing/template/sample/` 끝점에 대한 GET 요청을 만들고 템플릿을 만드는 데 사용할 대상 구성의 대상 ID를 제공하여 샘플 템플릿을 가져올 수 있습니다.

>[!TIP]
>
>* 여기에서 사용해야 하는 대상 ID는 `/destinations` 끝점을 사용하여 만든 대상 구성에 해당하는 `instanceId`입니다. 자세한 내용은 [대상 구성 검색](../../authoring-api/destination-configuration/retrieve-destination-configuration.md)을 참조하세요.

**API 형식**

```http
GET authoring/testing/template/sample/{DESTINATION_ID}
```

| 매개변수 | 설명 |
| -------- | ----------- |
| `{DESTINATION_ID}` | 메시지 변환 템플릿을 생성하는 대상 구성의 ID입니다. |

**요청**

다음 요청은 페이로드에 제공된 매개 변수로 구성된 새 샘플 템플릿을 생성합니다.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/testing/template/sample/5114d758-ce71-43ba-b53e-e2a91d67b67f' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

**응답**

성공적인 응답은 예상 데이터 형식과 일치하도록 편집할 수 있는 샘플 템플릿과 함께 HTTP 상태 200을 반환합니다.

제공한 대상 ID가 집계 정책에서 [우수 사례 집계](../../functionality/destination-configuration/aggregation-policy.md) 및 `maxUsersPerRequest=1`을(를) 사용하는 대상 구성에 해당하는 경우 요청은 다음과 유사한 샘플 템플릿을 반환합니다.

```python
{#- THIS is an example template for a single profile -#}
{#- A '-' at the beginning or end of a tag removes all whitespace on that side of the tag. -#}
{
    "identities": [
    {%- for idMapEntry in input.profile.identityMap -%}
    {%- set namespace = idMapEntry.key -%}
        {%- for identity in idMapEntry.value %}
        {
            "type": "{{ namespace }}",
            "id": "{{ identity.id }}"
        }{%- if not loop.last -%},{%- endif -%}
        {%- endfor -%}{%- if not loop.last -%},{%- endif -%}
    {% endfor %}
    ],
    "AdobeExperiencePlatformSegments": {
        "add": [
        {%- for segment in input.profile.segmentMembership.ups | added %}
            "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
        {% endfor %}
        ],
        "remove": [
        {#- Alternative syntax for filtering audiences by status: -#}
        {% for segment in removedSegments(input.profile.segmentMembership.ups) %}
            "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
        {% endfor %}
        ]
    }
}
```

제공한 대상 ID가 [구성 가능한 집계](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) 또는 `maxUsersPerRequest`이(가) 둘 이상인 [최상의 노력 집계](../../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation)인 대상 서버 템플릿에 해당하는 경우 요청은 다음과 유사한 샘플 템플릿을 반환합니다.

```python
{#- THIS is an example template for multiple profiles -#}
{#- A '-' at the beginning or end of a tag removes all whitespace on that side of the tag. -#}
{
    "profiles": [
    {%- for profile in input.profiles %}
        {
            "identities": [
            {%- for idMapEntry in profile.identityMap -%}
            {%- set namespace = idMapEntry.key -%}
                {%- for identity in idMapEntry.value %}
                {
                    "type": "{{ namespace }}",
                    "id": "{{ identity.id }}"
                }{%- if not loop.last -%},{%- endif -%}
                {%- endfor -%}{%- if not loop.last -%},{%- endif -%}
            {% endfor %}
            ],
            "AdobeExperiencePlatformSegments": {
                "add": [
                {%- for segment in profile.segmentMembership.ups | added %}
                    "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
                {% endfor %}
                ],
                "remove": [
                {#- Alternative syntax for filtering audiences by status: -#}
                {% for segment in removedSegments(profile.segmentMembership.ups) %}
                    "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
                {% endfor %}
                ]
            }
        }{%- if not loop.last -%},{%- endif -%}
    {% endfor %}
    ]
}
```

## API 오류 처리 {#api-error-handling}

Destination SDK API 엔드포인트는 일반적인 Experience Platform API 오류 메시지 원칙을 따릅니다. 플랫폼 문제 해결 안내서에서 [API 상태 코드](../../../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../../../landing/troubleshooting.md#request-header-errors)를 참조하십시오.

## 다음 단계 {#next-steps}

이 문서를 읽은 후에는 `/authoring/testing/template/sample` API 끝점을 사용하여 메시지 변환 템플릿을 생성하는 방법을 이해할 수 있습니다. 그런 다음 [템플릿 API 끝점 렌더링](render-template-api.md)을 사용하여 템플릿을 기반으로 내보낸 프로필을 생성하고 이를 대상의 예상 데이터 형식과 비교할 수 있습니다.
