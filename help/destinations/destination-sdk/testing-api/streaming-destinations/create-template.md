---
description: 대상을 게시하기 전에 대상 테스트 API를 사용하여 스트리밍 대상 메시지 변환 템플릿을 테스트하는 방법을 알아봅니다.
title: 메시지 변환 템플릿 만들기 및 테스트
exl-id: 15e7f436-4d33-4172-bd14-ad8dfbd5e4a8
source-git-commit: ab87a2b7190a0365729ba7bad472fde7a489ec02
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 0%

---


# 메시지 변환 템플릿 만들기 및 테스트 {#create-template}

## 개요 {#overview}

Adobe은 Destination SDK의 일부로서 대상을 구성하고 테스트하는 데 도움이 되는 개발자 도구를 제공합니다. 이 페이지에서는 메시지 변환 템플릿을 만들고 테스트하는 방법을 설명합니다. 대상을 테스트하는 방법에 대한 자세한 내용은 [대상 구성 테스트](streaming-destination-testing-overview.md).

종료 **메시지 변환 템플릿 만들기 및 테스트** Adobe Experience Platform의 대상 스키마와 대상에서 지원하는 메시지 형식 사이에 *템플릿 작성 도구* 아래에 자세히 설명되어 있습니다.  에서 소스와 대상 스키마 간의 데이터 변환에 대해 자세히 알아보십시오 [메시지 형식 문서](../../functionality/destination-server/message-format.md#using-templating).

아래 그림은 메시지 변환 템플릿을 만들고 테스트하는 방법을 [대상 구성 워크플로우](../../guides/configure-destination-instructions.md) Destination SDK:

![템플릿 만들기 단계가 대상 구성 워크플로우에 맞는 위치의 그래픽](../../assets/testing-api/create-template-step.png)

## 메시지 변환 템플릿을 만들고 테스트해야 하는 이유 {#why-create-message-transformation-template}

Destination SDK에서 대상을 만드는 첫 번째 단계 중 하나는 Adobe Experience Platform에서 대상으로 내보낼 때 세그먼트 멤버십, ID 및 프로필 속성에 대한 데이터 형식이 어떻게 변환되는지 고려하는 것입니다. 에서 Adobe XDM 스키마와 대상 스키마 간의 변환에 대한 정보를 찾습니다 [메시지 형식 문서](../../functionality/destination-server/message-format.md#using-templating).

변환을 성공하려면 다음 예와 유사한 변환 템플릿을 제공해야 합니다. [세그먼트, ID 및 프로필 속성을 보내는 템플릿을 만듭니다](../../functionality/destination-server/message-format.md#segments-identities-attributes).

Adobe은 Adobe XDM 형식의 데이터를 대상에서 지원하는 형식으로 변환하는 메시지 템플릿을 만들고 테스트할 수 있는 템플릿 도구를 제공합니다. 도구에는 사용할 수 있는 두 개의 API 엔드포인트가 있습니다.

* 를 사용하십시오 *샘플 템플릿 API* 샘플 템플릿을 가져오려면 다음을 수행하십시오.
* 를 사용하십시오 *렌더링 템플릿 API* 결과를 대상의 예상 데이터 형식과 비교할 수 있도록 샘플 템플릿을 렌더링하려면 다음을 수행하십시오. 내보낸 데이터를 대상에 필요한 데이터 형식과 비교한 후 템플릿을 편집할 수 있습니다. 이렇게 하면 내보낸 데이터가 대상에 필요한 데이터 형식과 일치합니다.

## 템플릿을 만들기 전에 완료하는 절차 {#prerequisites}

템플릿을 만들려면 먼저 아래 단계를 완료하십시오.

1. [대상 서버 구성 만들기](../../authoring-api/destination-server/create-destination-server.md). 생성할 템플릿은 다음에 제공하는 값에 따라 다릅니다. `maxUsersPerRequest` 매개 변수.
   * 사용 `maxUsersPerRequest=1` 세그먼트 자격, id 및 프로필 속성과 함께 단일 프로필을 포함하도록 대상에 대한 API 호출을 원하는 경우.
   * 사용 `maxUsersPerRequest` 를 사용하여 대상에 대한 API 호출이 세그먼트 자격, ID 및 프로필 속성과 함께 여러 프로필을 포함하려면 1보다 큰 값을 갖습니다.
2. [대상 구성 만들기](../../authoring-api/destination-configuration/create-destination-configuration.md) 및에서 대상 서버 구성의 ID를 추가합니다. `destinationDelivery.destinationServerId`.
3. [대상 구성의 ID 가져오기](../../authoring-api/destination-configuration/retrieve-destination-configuration.md) 방금 생성했으므로 템플릿 생성 도구에서 사용할 수 있습니다.
4. 이해 [사용할 수 있는 함수 및 필터](../../functionality/destination-server/supported-functions.md) 메시지 변환 템플릿에서

## 샘플 템플릿 API를 사용하고 템플릿 API를 렌더링하여 대상에 대한 템플릿을 만드는 방법 {#iterative-process}

>[!TIP]
>
>메시지 변환 템플릿을 만들고 편집하기 전에 [렌더링 템플릿 API 끝점](../../testing-api/streaming-destinations/render-template-api.md#render-exported-data) 변형을 적용하지 않고 원시 프로파일을 내보내는 간단한 템플릿으로 사용할 수 있습니다. 단순 템플릿의 구문은 다음과 같습니다. <br> `"template": "{% for profile in input.profiles %}{{profile|raw}}{% endfor %}}"`

템플릿을 가져오고 테스트하는 프로세스는 반복적입니다. 내보낸 프로필이 대상의 예상 데이터 형식과 일치할 때까지 아래 단계를 반복합니다.

1. 먼저, [샘플 템플릿 가져오기](../../testing-api/streaming-destinations/create-template.md#sample-template-api).
2. 샘플 템플릿을 시작점으로 사용하여 고유한 초안을 만듭니다.
3. 호출 [렌더링 템플릿 API 끝점](../../testing-api/streaming-destinations/create-template.md#render-template-api) 나만의 템플릿으로 사용할 수 있습니다. Adobe은 스키마를 기준으로 샘플 프로필을 생성하고 발생한 결과 또는 오류를 반환합니다.
4. 내보낸 데이터를 대상에 필요한 데이터 형식과 비교합니다. 필요한 경우 템플릿을 편집합니다.
5. 내보낸 프로필이 대상의 예상 데이터 형식과 일치할 때까지 이 프로세스를 반복합니다.

## 샘플 템플릿 API를 사용하여 샘플 템플릿 가져오기 {#sample-template-api}

>[!NOTE]
>
>전체 API 참조 설명서는 다음을 참조하십시오. [샘플 템플릿 API 작업 가져오기](../../testing-api/streaming-destinations/sample-template-api.md).

아래 표시된 대로 호출에 대상 ID를 추가하면 응답에서 대상 ID에 해당하는 템플릿 예를 반환합니다.

```shell
curl --location --request GET 'https://platform.adobe.io/data/core/activation/authoring/testing/template/sample/5114d758-ce71-43ba-b53e-e2a91d67b67f' \
--header 'Content-Type: application/json' \
--header 'Accept: application/json' \
--header 'x-api-key: {API_KEY}' \
--header 'Authorization: Bearer {ACCESS_TOKEN}' \
--header 'x-gw-ims-org-id: {ORG_ID}' \
--header 'x-sandbox-name: {SANDBOX_NAME}' \
```

제공하는 대상 ID가 [최상의 작업 집계](../../functionality/destination-configuration/aggregation-policy.md#best-effort-aggregation) 및 `maxUsersPerRequest=1` 집계 정책에서 요청은 이 템플릿과 유사한 샘플 템플릿을 반환합니다.

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

## 템플릿 문자 이스케이프 처리 {#character-escape-template}

템플릿을 사용하여 대상의 예상 형식과 일치하는 프로필을 렌더링하기 전에 아래 화면 기록에 표시된 대로 템플릿을 문자 이스케이프 처리해야 합니다.

![온라인 문자 이스케이프 도구를 사용하여 템플릿을 문자 이스케이프 처리하는 방법을 보여 주는 비디오입니다](../../assets/testing-api/escape-characters.gif)

온라인 문자 이스케이프 도구를 사용할 수 있습니다. 위의 데모에서는 [JSON 이스케이프 포맷터](https://jsonformatter.org/json-escape).

## 템플릿 API 렌더링 {#render-template-api}

를 사용하여 메시지 변환 템플릿을 만든 후 [샘플 템플릿 API](create-template.md#sample-template-api), 다음 작업을 수행할 수 있습니다. [템플릿 렌더링](render-template-api.md) 를 기반으로 내보낸 데이터를 생성합니다. 이렇게 하면 Adobe Experience Platform에서 대상으로 내보내는 프로필이 대상의 예상 형식과 일치하는지 확인할 수 있습니다.

수행할 수 있는 호출의 예는 API 참조를 참조하십시오.

* [본문에 전송된 프로필이 없는 템플릿 렌더링](render-template-api.md#multiple-profiles-no-body)
* [본문에 전송된 프로필로 템플릿 렌더링](render-template-api.md#multiple-profiles-with-body)

내보낸 프로필이 대상의 예상 데이터 형식과 일치될 때까지 템플릿을 편집하고 렌더링 템플릿 API 엔드포인트를 호출합니다.

## 대상 서버 구성에 문자 이스케이프 처리된 템플릿을 추가합니다

메시지 변환 템플릿에 만족하면 [대상 서버 구성](../../authoring-api/destination-server/create-destination-server.md), in `httpTemplate.requestBody.value`.
