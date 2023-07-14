---
description: 엔드포인트로 전송되는 HTTP 요청의 형식을 지정하는 방법을 알아봅니다. /authoring/destination-servers 끝점을 사용하여 Adobe Experience Platform Destination SDK에서 대상 서버 템플릿 사양을 구성합니다.
title: Destination SDK으로 만든 대상에 대한 템플릿 사양
source-git-commit: d6402f22ff50963b06c849cf31cc25267ba62bb1
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 4%

---


# Destination SDK으로 생성된 대상의 템플릿 사양

대상 서버 구성의 템플릿 사양 부분을 사용하여 대상으로 전송된 HTTP 요청의 형식을 지정하는 방법을 구성합니다.

템플릿 사양에서 XDM 스키마와 플랫폼이 지원하는 형식 간에 프로필 속성 필드를 변환하는 방법을 정의할 수 있습니다.

템플릿 사양은 실시간(스트리밍) 대상에 대한 대상 서버 구성의 일부입니다.

이 구성 요소가 Destination SDK으로 만든 통합에 어디에 맞는지 이해하려면 의 다이어그램을 참조하십시오. [구성 옵션](../configuration-options.md) 설명서 또는 방법에 대한 안내서 참조 [Destination SDK을 사용하여 스트리밍 대상 구성](../../guides/configure-destination-instructions.md#create-server-template-configuration).

다음을 통해 대상에 대한 템플릿 사양을 구성할 수 있습니다. `/authoring/destination-servers` 엔드포인트. 이 페이지에 표시된 구성 요소를 구성할 수 있는 자세한 API 호출 예는 다음 API 참조 페이지를 참조하십시오.

* [대상 서버 구성 만들기](../../authoring-api/destination-server/create-destination-server.md)
* [대상 서버 구성 업데이트](../../authoring-api/destination-server/update-destination-server.md)

>[!IMPORTANT]
>
>Destination SDK에서 지원하는 모든 매개변수 이름 및 값은 다음과 같습니다. **대소문자 구분**. 대소문자 구분 오류를 방지하려면 설명서에 표시된 대로 매개 변수 이름과 값을 정확히 사용하십시오.

## 지원되는 통합 유형 {#supported-integration-types}

이 페이지에 설명된 기능을 지원하는 통합 유형에 대한 자세한 내용은 아래 표를 참조하십시오.

| 통합 유형 | 기능 지원 |
|---|---|
| 실시간(스트리밍) 통합 | 예 |
| 파일 기반 (일괄 처리) 통합 | 아니요 |

## 템플릿 사양 구성 {#configure-template-spec}

Adobe은 다음과 유사한 템플릿 언어를 사용합니다. [진자](https://jinja.palletsprojects.com/en/2.11.x/) 를 클릭하여 XDM 스키마의 필드를 대상에서 지원하는 형식으로 변환합니다.

![강조 표시된 템플릿 구성](../../assets/functionality/destination-server/template-configuration.png)

변환에 대한 자세한 내용은 아래 링크를 참조하십시오.

* [메시지 포맷](message-format.md)
* [ID, 속성 및 대상자 멤버십 변환에 템플릿 언어 사용](message-format.md#using-templating)

>[!TIP]
>
>Adobe 오퍼 [개발자 도구](../../testing-api/streaming-destinations/create-template.md) 이렇게 하면 메시지 변환 템플릿을 만들고 테스트하는 데 도움이 됩니다.

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
| `httpMethod` | 문자열 | *필수 여부.* Adobe이 서버 호출에 사용할 메서드입니다. 지원되는 메서드: `GET`, `PUT`, `POST`, `DELETE`, `PATCH`. |
| `templatingStrategy` | 문자열 | *필수 여부.*`PEBBLE_V1` 사용. |
| `value` | 문자열 | *필수 여부.* 이 문자열은 Platform에서 보낸 HTTP 요청을 대상에 필요한 형식으로 포맷하는 이스케이프 처리된 템플릿 버전입니다. <br> 템플릿 작성 방법에 대한 자세한 내용은 [템플릿 사용](message-format.md#using-templating). <br> 문자 이스케이프에 대한 자세한 내용은 [RFC JSON 표준, 섹션 7](https://tools.ietf.org/html/rfc8259#section-7). <br> 간단한 변환의 예를 보려면 [프로필 속성](message-format.md#attributes) 변환. |
| `contentType` | 문자열 | *필수 여부.* 서버가 허용하는 콘텐츠 유형입니다. 변환 템플릿에서 생성되는 출력 유형에 따라 지원되는 모든 출력 유형이 될 수 있습니다 [HTTP 애플리케이션 콘텐츠 유형](https://www.iana.org/assignments/media-types/media-types.xhtml#application). 대부분의 경우 이 값은 다음으로 설정되어야 합니다. `application/json`. |

{style="table-layout:auto"}

## 다음 단계 {#next-steps}

이 문서를 읽고 나면 템플릿 사양의 정의와 템플릿 사양을 구성하는 방법을 보다 잘 이해할 수 있습니다.

다른 대상 서버 구성 요소에 대한 자세한 내용은 다음 문서를 참조하십시오.

* [Destination SDK으로 생성된 대상의 서버 사양](server-specs.md)
* [메시지 포맷](message-format.md)
* [파일 서식 구성](file-formatting.md)