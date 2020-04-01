---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: ID에 대한 기본 ID 가져오기
topic: API guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


# ID용 XID 가져오기

ID 데이터는 일반적으로 인제스트된 XDM 데이터에서 ID 문자열 값 및 ID 네임스페이스로 제공되며 API 호출에서 사용할 ID를 제공할 때 제공됩니다. ID가 Identity Service에서 지속되는 경우 ID가 생성되어 기본 XID라고 하는 ID에 할당됩니다. 플랫폼 API는 집계된 ID 및 네임스페이스에 대해 이 보다 압축된 양식을 사용하여 ID 데이터를 지원해야 합니다. XID는 base64 인코딩 문자열입니다.

>[!NOTE] 이 포맷은 주로 내부 Adobe에서 사용할 수 있습니다. 단일 값으로 기본 XID를 사용하면 공간 효율성이 향상되며 스토리지 및 직렬화를 위해 플랫폼 솔루션에서 내부적으로 사용되는 것이 그 예입니다. 그러나 사람이 읽을 수 없고 불투명하며 사용할 별도의 호출이 필요합니다.

이 섹션에 설명된 서비스를 사용하여 지정된 ID 값과 네임스페이스에 대한 XID를 얻습니다.

**API 형식**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/identity?namespace={NAMESPACE}&id={ID_VALUE}
```

**요청**

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/identity?namespace=email&id=test@adobetest.com' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

```json
{
    "xid":"BVrqzwVuzbXrLfmnaG3rXrLf3KJg"
}
```
