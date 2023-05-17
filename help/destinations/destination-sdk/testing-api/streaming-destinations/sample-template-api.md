---
description: 대상 테스트 API를 사용하여 대상에 대한 테스트 메시지 변환 템플릿을 생성하는 방법을 알아봅니다.
title: 샘플 메시지 변환 템플릿 생성
exl-id: d18a06f7-0c3a-4b4d-a7d5-011690d00e2c
source-git-commit: adf75720f3e13c066b5c244d6749dd0939865a6f
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 1%

---


# 샘플 메시지 변환 템플릿 생성 {#get-sample-template-api-operations}

>[!IMPORTANT]
>
>**API 엔드포인트**: `https://platform.adobe.io/data/core/activation/authoring/testing/template/sample`

이 페이지에서는 를 사용하여 수행할 수 있는 모든 API 작업을 나열하고 설명합니다. `/authoring/testing/template/sample` API 엔드포인트 : [메시지 변환 템플릿](../../functionality/destination-server/message-format.md#using-templating) 목적지에 대해 지정합니다. 이 종단점에서 지원하는 기능에 대한 설명은 다음을 참조하십시오 [템플릿 만들기](create-template.md).

## 샘플 템플릿 API 작업 시작 {#get-started}

계속하기 전에 [시작 안내서](../../getting-started.md) api를 성공적으로 호출하기 위해 알고 있어야 하는 중요한 정보(필수 대상 작성 권한 및 필수 헤더를 가져오는 방법)입니다.

## 샘플 템플릿 가져오기 {#generate-sample-template}

에 GET 요청을 작성하여 샘플 템플릿을 가져올 수 있습니다. `authoring/testing/template/sample/` 템플릿을 만들고 있는 대상에 따라 대상 구성의 대상 ID를 제공하는 종단점입니다.

>[!TIP]
>
>* 여기에서 사용해야 하는 대상 ID는 `instanceId` 대상 구성에 해당하며 `/destinations` 엔드포인트. 자세한 내용은 [대상 구성 검색](../../authoring-api/destination-configuration/retrieve-destination-configuration.md) 자세한 내용


**API 형식**

```http
GET authoring/testing/template/sample/{DESTINATION_ID}
```

| 매개변수 | 설명 |
| -------- | ----------- |
| `{DESTINATION_ID}` | 메시지 변환 템플릿을 생성하는 대상 구성의 ID입니다. |

**요청**

다음 요청은 페이로드에 제공된 매개 변수로 구성된 새로운 샘플 템플릿을 생성합니다.

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

제공하는 대상 ID가 [최상의 작업 집계](../../functionality/destination-configuration/aggregation-policy.md) 및 `maxUsersPerRequest=1` 집계 정책에서 요청은 이 템플릿과 유사한 샘플 템플릿을 반환합니다.

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
        {#- Alternative syntax for filtering segments by status: -#}
        {% for segment in removedSegments(input.profile.segmentMembership.ups) %}
            "{{ segment.key }}"{%- if not loop.last -%},{%- endif -%}
        {% endfor %}
        ]
    }
}
```

제공하는 대상 ID가 [구성 가능한 합계](../../functionality/destination-configuration/aggregation-policy.md#configurable-aggregation) 또는 [최상의 작업 집계](../../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation) with `maxUsersPerRequest` 요청이 두 개 이상이면 다음과 유사한 샘플 템플릿을 반환합니다.

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
                {#- Alternative syntax for filtering segments by status: -#}
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

Destination SDK API 엔드포인트는 일반 Experience Platform API 오류 메시지 원칙을 따릅니다. 을(를) 참조하십시오. [API 상태 코드](../../../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../../../landing/troubleshooting.md#request-header-errors) 을 참조하십시오.

## 다음 단계 {#next-steps}

이 문서를 읽은 후에는 `/authoring/testing/template/sample` API 엔드포인트. 다음으로, [템플릿 API 엔드포인트 렌더링](render-template-api.md) 템플릿을 기반으로 내보낸 프로필을 생성하여 대상의 예상 데이터 형식과 비교하려면 다음을 수행하십시오.
