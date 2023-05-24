---
title: 감사 이벤트 내보내기 API 끝점
description: 감사 쿼리 API를 사용하여 Experience Platform에서 감사 이벤트를 내보내는 방법을 알아봅니다.
exl-id: 76c5de76-e391-4258-afd8-ddb2c8a9443f
source-git-commit: c7887391481def872c40dd6ed1193bf562b9d0cf
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 5%

---

# 감사 이벤트 목록 내보내기

에 GET 요청을 하여 이벤트 데이터를 검색할 수 있습니다. `/audit/export` 페이로드에서 검색할 이벤트를 지정하는 엔드포인트.

**API 형식**

```http
GET /audit/export
```

| 매개변수 | 설명 |
| --------- | ----------- |
| `timestamp` | 타임스탬프로 필터링할 때는 정확한 값이 아닌 > 및 &lt; 연산자를 사용하여 범위를 사용하는 것이 좋습니다. <br/>예: `?property=timestamp<2020-02-08T02:46:48.610862Z&property=timestamp>2020-01-01T02:46:48.610862Z`. |
| `status` | 작업의 상태입니다. 상태는 다음 중 하나일 수 있습니다. </li><li>`Allow` </li><li>`Deny` </li><li>`Failure` </li><li>`Success` </li></ul><br/>예: `?property=status==Deny`. |
| `action` | 이벤트에 대해 기록된 작업 유형입니다. 작업은 다음 중 하나일 수 있습니다. <ul><li>`Add` </li><li>`Create` </li><li>`Dataset activate` </li><li>`Dataset remove` </li><li>`Delete` </li><li>`Disable for profile` </li><li>`Enable` </li><li>`Enable for profile` </li><li>`Profile activate` </li><li>`Profile remove` </li><li>`Remove` </li><li>`Reset` </li><li>`Segment Activate` </li><li>`Segment remove` </li><li>`Update` </li></ul> 예: `?property=action==Create`. |
| `user` | 이벤트를 수행한 사용자입니다. |
| `assetType` | 작업이 수행된 플랫폼 리소스의 유형입니다. <br/>예: `?property=assetType==<an asset type>`. |

**요청**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/audit/events
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-request-id: {TRACING_ID}' \
```

**응답**

내보내기를 위해 결과가 CSV 파일로 생성됩니다. 성공적인 응답은 응답 본문이 없는 HTTP 307을 반환합니다. 내보내기 파일에 대한 링크는에 제공됩니다. `Location` 응답 헤더.
