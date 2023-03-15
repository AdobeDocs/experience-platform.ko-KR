---
description: 이 페이지에서는 대상에 대한 테스트 메시지 변환 템플릿을 가져오기 위해 "/authoring/testing/template/sample" API 엔드포인트를 사용하여 수행할 수 있는 모든 API 작업을 나열하고 설명합니다.
title: 샘플 템플릿 API 작업 가져오기
exl-id: d18a06f7-0c3a-4b4d-a7d5-011690d00e2c
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 1%

---

# 샘플 템플릿 API 작업 가져오기 {#get=sample-template-api-operations}

>[!IMPORTANT]
>
>**API 엔드포인트**: `https://platform.adobe.io/data/core/activation/authoring/testing/template/sample`

이 페이지에서는 다음을 사용하여 수행할 수 있는 모든 API 작업을 나열하고 설명합니다. `/authoring/testing/template/sample` API 엔드포인트, API 엔드포인트 [메시지 변환 템플릿](./message-format.md#using-templating) 목적지로요 이 끝점에서 지원하는 기능에 대한 설명은 다음을 참조하십시오. [템플릿 만들기](./create-template.md).

## 샘플 템플릿 API 작업 시작 {#get-started}

계속하기 전에 다음을 검토하십시오. [시작 안내서](./getting-started.md) 필수 대상 작성 권한 및 필수 헤더를 가져오는 방법을 포함하여 API를 성공적으로 호출하기 위해 알아야 하는 중요한 정보입니다.

## 샘플 템플릿 가져오기 {#generate-sample-template}

에 GET 요청을 하여 샘플 템플릿을 가져올 수 있습니다. `authoring/testing/template/sample/` 엔드포인트 및 템플릿 생성 시 기준이 되는 대상 구성의 대상 ID 제공

>[!TIP]
>
>* 여기에서 사용해야 하는 대상 ID는 입니다. `instanceId` 대상 구성에 해당하며 `/destinations` 엔드포인트. 다음을 참조하십시오. [대상 구성 API 참조](./destination-configuration-api.md#retrieve-list).


**API 형식**


```http
GET authoring/testing/template/sample/{DESTINATION_ID}
```

| 매개 변수 | 설명 |
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

제공한 대상 ID가 의 대상 구성에 해당하는 경우 [최적 작업 집계](./destination-configuration.md#best-effort-aggregation) 및 `maxUsersPerRequest=1` 집계 정책에서 요청은 다음과 유사한 샘플 템플릿을 반환합니다.

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

제공한 대상 ID가 [구성 가능한 집계](./destination-configuration.md#configurable-aggregation) 또는 [최적 작업 집계](./destination-configuration.md#best-effort-aggregation) 포함 `maxUsersPerRequest` 둘 이상인 경우 요청은 이 템플릿과 유사한 샘플 템플릿을 반환합니다.

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

Destination SDK API 엔드포인트는 일반적인 Experience Platform API 오류 메시지 원칙을 따릅니다. 을(를) 참조하십시오 [API 상태 코드](../../landing/troubleshooting.md#api-status-codes) 및 [요청 헤더 오류](../../landing/troubleshooting.md#request-header-errors) 플랫폼 문제 해결 안내서에서 확인할 수 있습니다.

## 다음 단계 {#next-steps}

이 문서를 읽고 나면 이제 를 사용하여 메시지 변형 템플릿을 생성하는 방법을 이해할 수 있습니다. `/authoring/testing/template/sample` API 엔드포인트. 다음으로, 다음을 사용할 수 있습니다. [템플릿 API 끝점 렌더링](./render-template-api.md) 템플릿을 기반으로 내보낸 프로필을 생성하고 대상의 예상 데이터 형식과 비교할 수 있습니다.
