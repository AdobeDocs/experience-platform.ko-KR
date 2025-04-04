---
keywords: Experience Platform;홈;인기 항목;ID xid;XID
solution: Experience Platform
title: ID에 대한 기본 ID 가져오기
description: ID 데이터는 일반적으로 수집된 XDM 데이터에서, 그리고 API 호출에 사용할 ID를 제공할 때 ID 문자열 값과 ID 네임스페이스로 제공됩니다. ID가 ID 서비스에서 유지되면 ID가 생성되어 기본 XID라고 하는 해당 ID에 할당됩니다. 집계된 ID 및 네임스페이스에 대해 보다 컴팩트한 양식을 사용하여 ID 데이터 지원이 필요한 Experience Platform API. XID는 base64로 인코딩된 문자열입니다.
role: Developer
exl-id: e734f5d8-e00b-43fa-b06c-97c73e1f7c71
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# ID에 대한 기본 ID 가져오기

ID 데이터는 일반적으로 수집된 XDM 데이터에서, 그리고 API 호출에 사용할 ID를 제공할 때 ID 문자열 값과 ID 네임스페이스로 제공됩니다. ID가 [!DNL Identity Service]에서 유지되면 ID가 생성되어 기본 XID라고 하는 해당 ID에 할당됩니다. 집계된 ID와 네임스페이스에 대해 이 더 컴팩트한 양식을 사용하여 ID 데이터 지원이 필요한 API [!DNL Experience Platform]개 XID는 base64로 인코딩된 문자열입니다.

>[!NOTE]
>
>이 형식은 주로 내부 Adobe 용입니다. 단일 값으로 네이티브 XID를 사용하는 것이 공간 효율적이며, 저장소 및 직렬화를 위해 [!DNL Experience Platform] 솔루션 내에서 내부적으로 사용됩니다. 그러나 사람이 읽을 수 있는 것은 아니며 불투명하고 사용하기 위해 이를 얻기 위해 별도의 호출이 필요합니다.

이 섹션에 설명된 서비스를 사용하여 주어진 ID 값 및 네임스페이스에 대한 XID를 얻습니다.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**응답**

```json
{
    "xid":"BVrqzwVuzbXrLfmnaG3rXrLf3KJg"
}
```
