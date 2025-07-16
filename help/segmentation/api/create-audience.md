---
title: 대상 API 끝점 만들기
description: API를 사용하여 외부 대상자를 위한 메타데이터를 만드는 방법을 알아봅니다.
hide: true
hidefromtoc: true
source-git-commit: 74fa66e78ac36c8007eb89e8c271d989845c96f0
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 6%

---


# 대상 엔드포인트 만들기

POST `/audiences` 끝점은 외부 대상에 대한 메타데이터를 만드는 데 사용할 수 있습니다. 대상 수집이 배치 수집과 같은 별도의 서비스에서 관리되는 경우 이 끝점을 사용해야 합니다.

## 시작

>[!IMPORTANT]
>
>이 안내서의 끝점에는 `/core/ais`이(가) 아닌 `/core/ups`이(가) 접두사로 사용됩니다.

Experience Platform API를 사용하려면 [인증 자습서](https://www.adobe.com/go/platform-api-authentication-en)를 완료해야 합니다. 인증 자습서를 완료하면 아래와 같이 Experience Platform API 호출에서 필요한 각 헤더에 대한 값이 제공됩니다.

- 인증: `Bearer {ACCESS_TOKEN}`
- x-api 키: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

[!DNL Experience Platform]의 모든 리소스는 특정 가상 샌드박스로 격리되어 있습니다. [!DNL Experience Platform] API에 대한 모든 요청에는 작업을 수행할 샌드박스의 이름을 지정하는 헤더가 필요합니다.

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>[!DNL Experience Platform]의 샌드박스 작업에 대한 자세한 내용은 [샌드박스 개요 설명서](../../sandboxes/home.md)를 참조하세요.

**API 형식**

>[!IMPORTANT]
>
>**은(는)** 쿼리 매개 변수를 요청의 일부로 포함해야`createAudienceMetaOnly=true`합니다.

```http
POST /audiences?createAudienceMetaOnly=true
```

**요청**

>[!IMPORTANT]
>
>**must**&#x200B;이(가) `Accept: application/vnd.adobe.external.audiences+json; version=2` 헤더를 API 요청의 일부로 포함합니다.

```shell
curl -X POST https://platform.adobe.io/core/ais/audiences?createAudienceMetaOnly=true \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'\
 -H 'Accept: application/vnd.adobe.external.audiences+json; version=2'
 -d '{
    "name": "Sample audience name",
    "description" "A sample description for the audience.",
    "namespace": "agora",
    "originName": "Agora_Collaboration"
 }'
```

| 속성 | 유형 | 설명 |
| -------- | ---- | ----------- |
| `name` | 문자열 | 대상자의 이름입니다. |
| `description` | 문자열 | 대상자에 대한 선택적 설명입니다. |
| `namespace` | 문자열 | 대상자를 위한 네임스페이스입니다. |
| `originName` | 문자열 | 대상자의 기원 이름. |

**응답**

성공적인 응답은 새로 생성된 대상자에 대한 정보와 함께 HTTP 상태 200을 반환합니다.

```json
{
    "name": "Sample audience name",
    "audienceId": "4a815904-f2f9-4237-82fb-55605bcc2ad7"
}
```

| 속성 | 유형 | 설명 |
| -------- | ---- | ----------- |
| `name` | 문자열 | 만든 대상자의 이름입니다. |
| `audienceId` | 문자열 | 만든 대상자의 ID입니다. |
