---
description: 엔드포인트로 전송되는 HTTP 요청의 형식을 지정하는 방법을 알아봅니다. /authoring/destination-servers 끝점을 사용하여 Adobe Experience Platform Destination SDK에서 대상 서버 템플릿 사양을 구성합니다.
title: Destination SDK으로 만든 대상에 대한 사양 템플릿
exl-id: 066781c8-0af0-4958-b62f-194c6ba13f3a
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '512'
ht-degree: 2%

---

# Destination SDK으로 만든 대상의 템플릿 사양

대상 서버 구성의 템플릿 사양 부분을 사용하여 대상으로 전송된 HTTP 요청의 형식을 지정하는 방법을 구성합니다.

템플릿 사양에서 XDM 스키마와 플랫폼이 지원하는 형식 간에 프로필 속성 필드를 변환하는 방법을 정의할 수 있습니다.

템플릿 사양은 실시간(스트리밍) 대상에 대한 대상 서버 구성의 일부입니다.

이 구성 요소가 Destination SDK으로 만든 통합에 어디에 맞는지 이해하려면 [구성 옵션](../configuration-options.md) 설명서에서 다이어그램을 참조하거나 [Destination SDK을 사용하여 스트리밍 대상을 구성하는 방법](../../guides/configure-destination-instructions.md#create-server-template-configuration)에 대한 안내서를 참조하십시오.

`/authoring/destination-servers` 끝점을 통해 대상에 대한 템플릿 사양을 구성할 수 있습니다. 이 페이지에 표시된 구성 요소를 구성할 수 있는 자세한 API 호출 예는 다음 API 참조 페이지를 참조하십시오.

* [대상 서버 구성 만들기](../../authoring-api/destination-server/create-destination-server.md)
* [대상 서버 구성 업데이트](../../authoring-api/destination-server/update-destination-server.md)

>[!IMPORTANT]
>
>Destination SDK에서 지원하는 모든 매개 변수 이름과 값은 **대/소문자를 구분합니다**. 대소문자 구분 오류를 방지하려면 설명서에 표시된 대로 매개 변수 이름과 값을 정확히 사용하십시오.

## 지원되는 통합 유형 {#supported-integration-types}

이 페이지에 설명된 기능을 지원하는 통합 유형에 대한 자세한 내용은 아래 표를 참조하십시오.

| 통합 유형 | 기능 지원 |
|---|---|
| 실시간(스트리밍) 통합 | 예 |
| 파일 기반 (일괄 처리) 통합 | 아니요 |

## 템플릿 사양 구성 {#configure-template-spec}

Adobe은 [Jinja](https://jinja.palletsprojects.com/en/2.11.x/)와(과) 유사한 템플릿 언어를 사용하여 XDM 스키마의 필드를 대상에서 지원하는 형식으로 변환합니다.

![템플릿 구성 강조 표시](../../assets/functionality/destination-server/template-configuration.png)

변환에 대한 자세한 내용은 아래 링크를 참조하십시오.

* [메시지 포맷](message-format.md)
* [ID, 속성 및 대상자 멤버십 변환에 템플릿 언어 사용](message-format.md#using-templating)

>[!TIP]
>
>Adobe에서는 메시지 변환 템플릿을 만들고 테스트하는 데 도움이 되는 [개발자 도구](../../testing-api/streaming-destinations/create-template.md)를 제공합니다.

각 개별 매개 변수에 대한 설명과 함께 HTTP 요청 템플릿의 아래를 참조하십시오.

```json
{
   "httpTemplate":{
      "httpMethod":"POST",
      "requestBody":{
         "templatingStrategy":"PEBBLE_V1",
         "value":"{ \"attributes\": [ {% for ns in [\"external_id\", \"yourdestination_id\"] %} {% if input.profile.identityMap[ns] is not empty and first_namespace_encountered %} , {% endif %} {% set first_namespace_encountered = true %} {% for identity in input.profile.identityMap[ns]%} { \"{{ ns }}\": \"{{ identity.id }}\" {% if input.profile.segmentMembership.ups is not empty %} , \"AEPSegments\": { \"add\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"realized\" or segment.value.status == \"existing\" %} {% if added_segment_found %} , {% endif %} {% set added_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ], \"remove\": [ {% for segment in input.profile.segmentMembership.ups %} {% if segment.value.status == \"exited\" %} {% if removed_segment_found %} , {% endif %} {% set removed_segment_found = true %} \"{{ destination.segmentAliases[segment.key] }}\" {% endif %} {% endfor %} ] } {% set removed_segment_found = false %} {% set added_segment_found = false %} {% endif %} {% if input.profile.attributes is not empty %} , {% endif %} {% for attribute in input.profile.attributes %} \"{{ attribute.key }}\": {% if attribute.value is empty %} null {% else %} \"{{ attribute.value.value }}\" {% endif %} {% if not loop.last%} , {% endif %} {% endfor %} } {% if not loop.last %} , {% endif %} {% endfor %} {% endfor %} ] }"
      },
      "contentType":"application/json"
   }
}
```

| 매개변수 | 유형 | 설명 |
|---|---|---|
| `httpMethod` | 문자열 | *필수.* Adobe에서 서버 호출에 사용할 메서드입니다. 지원되는 메서드: `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `templatingStrategy` | 문자열 | *필수.* `PEBBLE_V1` 사용. |
| `value` | 문자열 | *필수.* 이 문자열은 Experience Platform에서 보낸 HTTP 요청의 형식을 대상에 필요한 형식으로 지정하는 문자 이스케이프 처리된 템플릿 버전입니다. <br> 서식 파일을 작성하는 방법에 대한 자세한 내용은 [서식 파일 사용](message-format.md#using-templating)의 섹션을 참조하십시오. <br> 문자 이스케이프에 대한 자세한 내용은 [RFC JSON 표준, 섹션 7](https://tools.ietf.org/html/rfc8259#section-7)을 참조하세요. <br> 간단한 변환의 예를 보려면 [프로필 특성](message-format.md#attributes) 변환을 참조하십시오. |
| `contentType` | 문자열 | *필수.* 서버가 허용하는 콘텐츠 형식입니다. 변환 템플릿에서 생성되는 출력 유형에 따라 지원되는 [HTTP 응용 프로그램 콘텐츠 형식](https://www.iana.org/assignments/media-types/media-types.xhtml#application)이 될 수 있습니다. 대부분의 경우 이 값은 `application/json`(으)로 설정해야 합니다. |

{style="table-layout:auto"}

## 다음 단계 {#next-steps}

이 문서를 읽고 나면 템플릿 사양의 정의와 템플릿 사양을 구성하는 방법을 보다 잘 이해할 수 있습니다.

다른 대상 서버 구성 요소에 대한 자세한 내용은 다음 문서를 참조하십시오.

* [Destination SDK으로 만든 대상의 서버 사양](server-specs.md)
* [메시지 포맷](message-format.md)
* [파일 서식 구성](file-formatting.md)
