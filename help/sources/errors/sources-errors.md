---
title: 소스 오류 메시지
description: 소스에 대해 흐름 서비스를 사용할 때 발생할 수 있는 오류 메시지에 대해 알아봅니다.
exl-id: cfba9780-4ab9-447b-8c60-c9f813107d11
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '3188'
ht-degree: 90%

---

# 소스 오류 메시지

이 문서에서는 오류 메시지, 설명 및 소스에 대해 제안된 해결 방법에 대한 카탈로그를 제공합니다.

## 일반 오류

| 오류 코드 | 제목 | 자세한 메시지 |
| --- | --- | --- |
| `1000-400` | 잘못된 요청 | 잘못된 요청입니다. 요청을 확인하고 다시 시도하십시오. |
| `1001-401` | 인증되지 않음 | 사용자는 권한이 없습니다. 관리자에게 문의하여 리소스에 대한 액세스 권한을 받으십시오. |
| `1002-403` | 금지 | 요청한 작업을 사용할 수 없습니다 . 요청한 작업을 확인하고 다시 시도하십시오. |
| `1003-404` | 리소스를 찾을 수 없음 | 요청한 리소스를 찾을 수 없습니다. 입력된 요청을 확인하고 다시 시도하십시오. |
| `1004-415` | 지원되지 않는 미디어 유형 | 입력된 페이로드 포맷이 지원되지 않습니다. 입력된 요청을 확인하고 다시 시도하십시오. |
| `1005-500` | 내부 오류 | 내부 오류가 발생했습니다. 다시 시도해 주십시오. 문제가 지속되면 고객 지원 센터에 문의하십시오. |
| `1006-408` | 요청 시간 초과 | 요청을 처리하는 동안 오류가 발생했습니다. 요청의 시간이 초과되었습니다. 다시 시도해보고 문제가 지속되면 고객 지원 센터에 문의하십시오. |
| `1007-400` | 잘못된 헤더 매개변수 | 잘못된 헤더 매개변수: {headerName}이(가) 수신되었습니다. 헤더 매개변수를 확인하고 다시 시도하십시오. |
| `1008-401` | | 잘못된 인증 토큰 | 인증 토큰에 이 조직에 대한 액세스 권한이 없거나 조직이 존재하지 않습니다. 조직이 존재하는지 확인하거나 관리자에게 액세스 권한을 요청하십시오. |
| `1009-403` | IMS org id가 누락되거나 비어 있음 | 조직 ID 요청 헤더가 누락되거나 비어 있습니다. 헤더 값을 업데이트하고 다시 시도하십시오. |
| `1010-500` | 잘못된 상세 메세지 | 상세 메시지의 매개변수가 제대로 입력되지 않았습니다. 상세 메시지에서 매개변수를 확인하고 다시 시도하십시오. |
| `1011-503` | 서비스를 사용할 수 없음 | 서비스를 일시적으로 사용할 수 없습니다. 다시 시도해보고 문제가 지속되면 고객 지원 센터에 문의하십시오. |
| `1012-504` | 게이트웨이 시간 초과 | 게이트웨이 시간 초과 오류가 발생했습니다. 다시 시도해 주십시오. 문제가 지속되면 고객 지원 센터에 문의하십시오. |
| `1013-412` | 사전 조건 오류 | If-Unmodified-Since 또는 If-None-Match 헤더에 의해 정의된 조건이 충족되지 않습니다. 확인하고 다시 시도해 보십시오. |
| `1014-400` | 잘못된 요청 잘못된 인수 | 요청을 처리할 수 없습니다. {detailedMessage} |

## 프레임워크 오류

| 오류 코드 | 제목 | 자세한 메시지 |
| --- | --- | --- |
| `1100-400` | 잘못된 요청 | 요청을 처리할 수 없습니다. {detailedMessage} |
| `1101-500` | 내부 오류 | 내부 오류가 발생했습니다. 다시 시도해 주십시오. 문제가 지속되면 고객 지원 센터에 문의하십시오. |
| `1102-404` | 리소스를 찾을 수 없음 | 요청한 리소스를 찾을 수 없습니다. {detailedMessage} |
| `1103-503` | 서비스를 사용할 수 없음 | 서비스를 일시적으로 사용할 수 없습니다. 다시 시도해보고 문제가 지속되면 고객 지원 센터에 문의하십시오. |
| `1104-504` | 게이트웨이 시간 초과 | 게이트웨이 시간 초과 오류가 발생했습니다. 다시 시도해 주십시오. 문제가 지속되면 고객 지원 센터에 문의하십시오. |
| `1105-401` | 인증되지 않음 | 사용자가 권한이 없습니다. {detailedMessage} |
| `1106-403` | 금지 | 요청한 작업을 사용할 수 없습니다. {detailedMessage} |
| `1107-412` | 사전 조건 오류 | If-Unmodified-Since 또는 If-None-Match 헤더에 의해 정의된 조건이 충족되지 않습니다. {detailedMessage} |

## 암호화 오류

| 오류 코드 | 제목 | 자세한 메시지 |
| --- | --- | --- |
| `1200-500` | 내부 오류 | 내부 오류가 발생했습니다. 다시 시도해 주십시오. 문제가 지속되면 고객 지원 센터에 문의하십시오. |
| `1201-400` | 잘못된 요청 | flowId는 비어 있거나 null일 수 없습니다. 요청에 유효한 flowId를 입력하고 다시 시도하십시오. |
| `1202-400` | 잘못된 요청 | 흐름의 transformations={transformations}에서 publicKeyId가 누락되었습니다. 요청에 publicKeyId를 입력하고 다시 시도하십시오. |
| `1203-400` | 잘못된 요청 | 흐름의 transformations={transformations}에서 keyID={keyID}에 대한 암호화 키가 존재하지 않습니다. 입력된 keyID를 확인하고 다시 시도하십시오. |
| `1204-400` | 잘못된 요청 | 입력된 암호화 알고리즘이 유효하지 않습니다. 유효한 암호화 알고리즘을 입력하고 다시 시도해 주십시오. |
| `1205-400` | 잘못된 요청 | 입력된 요청의 매개변수 섹션에 암호구가 없습니다. 매개변수에 암호구를 입력하고 다시 시도하십시오. |

## REST API 오류

| 오류 코드 | 제목 | 자세한 메시지 |
| --- | --- | --- |
| `1300-400` | 잘못된 요청 | 패치 연결 요청은 {connectorType} 커넥터에 대해 지원되지 않습니다. 입력된 요청을 확인하고 다시 시도하십시오. |
| `1301-400` | 잘못된 요청 | 입력된 authSpecType 매개변수: {authSpecType}이(가) 지원되지 않습니다. 유효한 인증 사양 유형을 제공하고 다시 시도하십시오. |
| `1302-400` | 잘못된 요청 | 입력된 인증 유형 = {authType}은 connector={connectorType}에 대해 지원되지 않습니다. 주어진 커넥터에 유효한 인증 유형을 입력하십시오. |
| `1303-400` | 잘못된 요청 | URL 인코딩이 {value}에 대해 지원되지 않기 때문에 지정된 인증 매개변수로 URL을 인코딩할 수 없습니다. 인증 매개변수를 확인하고 다시 시도하십시오. |
| `1304-400` | 잘못된 요청 | 필수 필드 {field}가 입력되지 않았습니다. {field}를 입력하고 다시 시도하십시오. |
| `1305-400` | 잘못된 요청 | 입력된 커넥터 유형 = {connectorType}은(는) 이 작업에서 지원되지 않습니다. |
| `1306-400` | 잘못된 요청 | 대상 연결 사양 ID의 유효성을 검사하는 동안 대상 연결은 null일 수 없습니다. 제공된 요청을 확인하고 다시 시도하십시오. |
| `1307-400` | 잘못된 요청 | 대상 연결 사양 ID가 잘못되었습니다={targetConnectionSpecId}. 허용되는 값은 `c604ff05-7f1a-43c0-8e18-33bf874cb11c`입니다. |
| `1308-400` | 잘못된 요청 | 요청을 처리할 수 없습니다. 오류 메시지: {msftErrorMessage} |
| `1309-400` | 잘못된 요청 | 매개변수에 {requiredParam}이(가) 없기 때문에 입력된 암호화 변환이 유효하지 않습니다. {requiredParam}을 입력하고 다시 시도하십시오. |
| `1310-400` | 잘못된 요청 | 매개변수에 입력된 publicKeyId가 만료되었습니다. 유효한 publicKeyId를 입력하고 다시 시도하십시오. |
| `1311-400` | 잘못된 요청 | 매개변수에 입력된 publicKeyId가 잘못되었습니다. 유효한 publicKeyId를 입력하고 다시 시도하십시오. |
| 1312-400 | 잘못된 요청 | 입력된 매개변수 값 {paramValue}은(는) property={requestParam}에 대한 유효한 입력이 아닙니다. 유효한 매개변수 값을 입력하고 다시 시도하십시오. |
| `1313-400` | 잘못된 요청 | 경로 속성 {attribute}이(가) 존재하지 않습니다. 속성이 존재하는지 확인하고 다시 시도하십시오. |
| `1314-400` | 잘못된 요청 | 복잡한 경로가 입력되었지만 허용되지 않습니다. 복잡한 경로가 입력되지 않도록 확인하고 다시 시도하십시오. |
| `1315-400` | 잘못된 요청 | 입력된 경로 {path}는 레코드 배열로 지정되어야 합니다. 입력된 경로가 레코드 배열로 지정되었는지 확인하고 다시 시도하십시오. |
| `1316-400` | 잘못된 요청 | 입력된 페이지 매기기 매개변수는 비어 있으면 안 됩니다. 유효한 페이지 매기기 매개변수를 입력하고 다시 시도하십시오. |
| `1317-400` | 잘못된 요청 | 입력된 일정 매개변수는 비어 있으면 안 됩니다. 유효한 일정 매개변수를 입력하고 다시 시도하십시오. |
| `1318-400` | 잘못된 요청 | {combinedMessage}. 입력된 요청을 확인하고 다시 시도하십시오. |
| `1319-400` | 잘못된 요청 | {param}은 상위 컬렉션의 일부여야 합니다. 상위 컬렉션에 {param}을 입력하고 다시 시도하십시오. |
| `1320-400` | 잘못된 요청 | {idType}는 비어 있거나 null일 수 없습니다. 유효한 {idType}를 입력하고 다시 시도하십시오. |
| `1321-400` | 잘못된 요청 | {idType}의 길이는 1이어야 하며 입력된 크기는 {size}입니다. 유효한 크기를 입력하고 다시 시도하십시오. |
| `1322-400` | 잘못된 요청 | 스키마 참조를 빌드할 때 소스 연결은 null일 수 없습니다. 유효한 소스 연결을 입력하고 다시 시도하십시오. |
| `1323-400` | 잘못된 요청 | 소스 연결: {sourceConnection}에서 {entity}는 null이거나 비어 있을 수 없습니다. 유효한 {entity}를 입력하고 다시 시도하십시오. |
| `1324-400` | 잘못된 요청 | 데이터 세트 ID를 추출하는 동안 대상 연결은 null일 수 없습니다. 유효한 대상 연결을 입력하고 다시 시도하십시오. |
| `1325-400` | 잘못된 요청 | 대상 연결: {TargetConnection}에서 dataSetId 매개변수는 null이거나 비어 있을 수 없습니다. 유효한 dataSetId 매개변수를 입력하고 다시 시도하십시오. |
| `1326-400` | 잘못된 요청 | 소스 포맷을 가져올 때 소스 연결은 null일 수 없습니다. 유효한 소스 연결을 사용해서 다시 시도하십시오. |
| `1327-400` | 잘못된 요청 | SourceConnection에서 제공되는 소스 데이터의 포맷={sourceFormat}은 지원되지 않습니다. 허용되는 값은 {values}입니다. 허용되는 값을 입력하고 다시 시도하십시오. |
| `1328-400` | 잘못된 요청 | 매핑 변환은 {param}을 추출할 때 null일 수 없습니다. 유효한 매핑 변환을 입력하고 다시 시도하십시오. |
| `1329-400` | 잘못된 요청 | 매개변수: {param}은(는) 입력된 요청에서 null이거나 비어 있을 수 없습니다. 유효한 {param}을 입력하고 다시 시도하십시오. |
| `1330-400` | 잘못된 요청 | 테이블 {tableName}에 대한 열이 없습니다. 유효한 테이블 이름을 입력하고 다시 시도하십시오. |
| `1331-400` | 잘못된 요청 | 열 구분 기호는 SourceConnection: {sourceConnection}에서 두 문자 이상일 수 없습니다. 유효한 열 구분 기호를 사용해서 다시 시도하십시오. |
| `1332-400` | 잘못된 요청 | connectionSpecId: {connectionSpecId}가 있는 소스 연결 요청은 baseConnectionId를 가질 수 없습니다. baseConnectionId를 제거하고 다시 시도하십시오. |
| `1333-400` | 잘못된 요청 | Spec id={specId}인 소스에 대해 flowRunAction={flowRunAction}이 지원되지 않습니다. 유효한 흐름 실행 액션을 입력하고 다시 시도하십시오. |
| `1334-400` | 잘못된 요청 | 쿼리 매개변수: {param}은 비워둘 수 없습니다. 유효한 {param}을 입력하고 다시 시도하십시오. |
| `1335-400` | 잘못된 요청 | 탐색을 위해 필터 매개변수를 직렬화하는 동안 오류가 발생했습니다. 필터 매개변수 요청을 확인하고 다시 시도하십시오. |
| `1336-400` | 잘못된 요청 | 연결 사양 ID: {connectionSpecId}에 대해 탐색 연결이 지원되지 않습니다. 지원되는 연결 사양 ID를 입력하고 다시 시도하십시오. |
| `1337-400` | 잘못된 요청 | {QueryParam}은 objectType={objectType}에 대해 비워둘 수 없습니다. 유효한 {QueryParam}을 입력하고 다시 시도하십시오. |
| `1338-400` | 잘못된 요청 | {connectionType} 연결 ID는 flowRequest에서 null일 수 없습니다. flowRequest에 유효한 {connectionType} 연결 ID를 입력하세요. |
| `1339-400` | 잘못된 요청 | 요청에 입력한 조직={imsOrg} 형식이 잘못되었습니다. 유효한 조직 ID를 입력하고 다시 시도하십시오. |
| `1340-400` | 잘못된 요청 | {time} 구문 분석 중 오류가 발생했습니다. 요청에 입력된 시간 포맷을 확인하고 다시 시도하십시오. |
| `1341-400` | 잘못된 요청 | 입력된 ODI Json이 비어 있습니다. 유효한 ODI Json을 입력하고 다시 시도하십시오. |
| `1342-400` | 잘못된 요청 | &#39;odi.json&#39;의 &#39;dls:folder&#39; 세그먼트에 정의가 누락되었습니다. &#39;odi.json&#39;에 적절한 정의를 입력하고 다시 시도하십시오. |
| `1343-400` | 잘못된 요청 | &#39;odi.json&#39;의 &#39;dls:entityReferences&#39; 및 &#39;dls:partitionSpec&#39; 세그먼트는 모두 누락된 정의입니다. &#39;odi.json&#39;에 적절한 정의를 입력하고 다시 시도하십시오. |
| `1344-400` | 잘못된 요청 | 둘 이상의 partitionSpec이 발견되었기 때문에 &#39;odi.json&#39;의 &#39;dls:partitionSpec&#39;에 대한 정의가 잘못되었습니다. &#39;odi.json&#39;에 적절한 정의를 입력하고 다시 시도하십시오. |
| `1345-400` | 잘못된 요청 | 경로의 1개 이상의 세그먼트에서 누락된 정의: &#39;dls:partitionSpec/dls:fileFormat&#39;, &#39;dls:partitionSpec/dls:partitionTemplate&#39;,&#39;dls:partitionSpec/dls:fileFormat/@type&#39;, &#39;dls:partitionSpec/dls :fileFormat/dls:csvDelimiters&#39; &#39;odi.json&#39;. &#39;odi.json&#39;에 적절한 정의를 입력하고 다시 시도하십시오. |
| `1346-400` | 잘못된 요청 | &#39;odi.json&#39;의 &#39;dls:fileFormat&#39;에 입력된 &#39;@type&#39; 정의가 잘못되었습니다. &#39;odi.json&#39;에 적절한 정의를 입력하고 다시 시도하십시오. |
| `1347-400` | 잘못된 요청 | &#39;odi.json&#39;의 dls:csvDelimiters&#39; 정의는 지원되지 않습니다. 지원되는 csvDelimiter는 [&#39;,&#39;]입니다. &#39;odi.json&#39;에 적절한 정의를 입력하고 다시 시도하십시오. |
| `1348-400` | 잘못된 요청 | &#39;dls:entityReferences&#39;를 역직렬화하는 동안 오류가 발생했습니다. 데이터가 유효한 형식인지 확인하고 다시 시도하십시오. |
| `1349-400` | 잘못된 요청 | 입력된 필터 매개변수가 잘못되었습니다. 유효한 필터 매개변수를 입력하고 다시 시도하십시오. |
| `1350-400` | 잘못된 요청 | 소스에서 필터에 대해 연산자가 제공되지 않았습니다. 적절한 연산자와 함께 유효한 필터 요청을 입력하고 다시 시도하십시오. |
| `1351-400` | 잘못된 요청 | 제공된 연산자 {operator}은(는) 이 커넥터의 소스에서 필터링할 수 없습니다. 유효한 연산자를 입력하고 다시 시도하십시오. |
| `1352-400` | 잘못된 요청 | 제공된 연산자 {operator}을(를) {ql}에 대해 지원되는 네이티브 연산자에 매핑할 수 없습니다. 유효한 연산자를 입력하고 다시 시도하십시오. |
| `1353-400` | 잘못된 요청 | 소스의 필터는 {connectorType} 커넥터에 대해 아직 지원되지 않습니다. 다음 문서에서 지원되는 커넥터를 확인하십시오. https://experienceleague.adobe.com/docs/experience-platform/sources/api-tutorials/filter.html?lang=ko. |
| `1354-400` | 잘못된 요청 | 쿼리 언어 {ql}은(는) 아직 원본의 필터에서 지원되지 않습니다. 유효한 쿼리 언어를 입력하고 다시 시도하십시오. |
| `1355-400` | 잘못된 요청 | 입력된 필터 유형이 잘못되었습니다. 지원되는 필터 유형은 PQL입니다. 유효한 필터 유형을 입력하고 다시 시도하십시오. |
| `1356-400` | 잘못된 요청 | 입력된 필터 포맷이 잘못되었습니다. 지원되는 필터 포맷은 pql/json입니다. 유효한 필터 포맷을 입력하고 다시 시도하십시오. |
| `1357-400` | 잘못된 요청 | 입력된 필터가 유효하지 않습니다. 자세한 필터와 함께 값을 입력해야 합니다. 유효한 필터를 입력하고 다시 시도하십시오. |
| `1358-400` | 잘못된 요청 | 입력된 매개변수 &#39;objectType&#39;이 유효하지 않습니다. 유효한 objectType을 입력하고 다시 시도하십시오. |
| `1359-400` | 잘못된 요청 | 요청에 매개변수 {header}이(가) 누락되었습니다. 유효한 {param}를 입력하고 다시 시도하십시오. |
| `1360-400` | 잘못된 요청 | 시작 시간을 과거로 설정할 수 없습니다. 유효한 시작 시간을 입력하고 다시 시도하십시오. |
| `1361-400` | 잘못된 요청 | 1회 수집에선 간격이 허용되지 않습니다. 간격을 제거하거나 빈도를 변경한 다음 다시 시도하십시오. |
| `1362-400` | 잘못된 요청 | 간격은 {minInterval}보다 작을 수 없습니다. 유효한 간격 값을 입력하고 다시 시도하십시오. |
| `1363-400` | 잘못된 요청 | 간격 {interval}은(는) 주파수: {frequency}에서 허용되지 않습니다. 유효한 간격 값을 입력하고 다시 시도하십시오. |
| `1364-400` | 잘못된 요청 | 빈도가 1로 설정된 경우 다시 채우기 플래그가 허용되지 않습니다. 빈도가 한 번으로 설정된 경우 다시 채우기 플래그를 제거하고 다시 시도하십시오. |
| `1365-400` | 잘못된 요청 | 작업에 입력된 경로 {path}가 잘못되었습니다. 유효한 경로 {path}를 입력하고 다시 시도하십시오. |
| `1366-400` | 잘못된 요청 | 시작 시간이 지났고 더 이상 업데이트 작업은 허용되지 않습니다. |
| `1367-400` | 잘못된 요청 | 델타 열은 CRM 커넥터를 만들 때 복사 변환에 필요합니다. 델타 열을 사용해서 다시 시도하십시오. |
| `1368-400` | 잘못된 요청 | 흐름 요청에서 모드는 허용되지 않습니다. 요청을 확인하고 다시 시도해 주십시오. |
| `1369-400` | 잘못된 요청 | 복사 변환의 델타 열은 빈도가 한 번으로 설정된 경우 허용되지 않습니다. 델타 열을 제거하고 다시 시도하십시오. |
| `1370-400` | 잘못된 요청 | 매핑 변환이 없기 때문에 수집을 위해 소스 열을 가져올 수 없습니다. 매핑 변환을 추가하고 다시 시도하십시오. |
| `1371-400` | 잘못된 요청 | 파일 속성 감지는 {connectorType} 커넥터에 대해 지원되지 않습니다. 파일 속성을 수동으로 입력하십시오. |
| `1372-400` | 잘못된 요청 | 현재 작업이 허용되지 않습니다. 연결 사양 ID={connectionSpecId}에는 연결 사양을 통한 탐색이 허용되지 않습니다. |
| `1373-400` | 잘못된 요청 | 요청에 flowSpecType이 누락되었습니다. 유효한 flowSpecType을 입력하고 다시 시도하십시오. |
| `1374-400` | 잘못된 요청 | 입력된 쿼리 매개변수가 잘못되었습니다. 동일한 요청에 determineProperties 플래그와 사용자 정의 속성을 포함할 수 없습니다. 요청을 수정하고 다시 시도하십시오. |
| `1375-400` | 잘못된 요청 | 파일 속성 검색에 실패했습니다. 속성을 수동으로 입력하십시오. |
| `1376-400` | 잘못된 요청 | 파일 속성 감지는 연결 사양 ID= {connectionSpecId}에 대해 지원되지 않습니다. 파일 속성을 수동으로 입력하십시오. |
| `1377-400` | 잘못된 요청 | 입력된 값 매개변수가 null이며 {operator} 연산자와 비교할 수 없습니다. 유효한 값 매개변수를 입력하고 다시 시도하십시오. |
| `1378-400` | 잘못된 요청 | 소스에서 필터에 대한 입력 열 {column}의 유효성을 검사하는 동안 오류가 발생했습니다. 열 이름은 테이블에서 유효한 열이어야 합니다. 유효한 열 이름을 입력하고 다시 시도하십시오. |
| `1379-400` | 잘못된 요청 | 소스에서 필터에 대한 입력 {value}의 유효성을 검사하는 동안 오류가 발생했습니다. 원본의 열 DataType이 {columnDataType}이고 값 DataType [String]이(가) 일치하지 않습니다. 올바른 {value}을(를) 입력하고 다시 시도하십시오. |
| `1380-400` | 잘못된 요청 | 흐름 실행을 만들지 못했습니다. 오류 메시지: {message} |
| `1381-400` | 잘못된 요청 | WindowEndTime={endTime}은 Window StartTime={startTime} 이전일 수 없습니다. 유효한 종료 시간을 입력하고 다시 시도하십시오. |
| `1382-400` | 잘못된 요청 | 델타 열은 흐름의 복사 변환에 있는 값과 일치해야 합니다. 유효한 델타 열을 입력하고 다시 시도하십시오. |
| `1383-400` | 잘못된 요청 | 흐름 실행을 만들기 위해 받은 매개변수에 델타 열이 없습니다. 매개변수에 델타 열을 입력하고 다시 시도하십시오. |
| `1384-400` | 잘못된 요청 | 흐름 실행 생성을 위해 입력된 params={params}가 잘못되었거나 비어 있습니다. 유효한 매개변수를 입력하고 다시 시도하십시오. |
| `1385-400` | 잘못된 요청 | 입력된 connectorType={connectorType}은 흐름 실행 생성에 지원되지 않습니다. 유효한 connectorType을 입력하고 다시 시도하십시오. |
| `1386-400` | 잘못된 요청 | scheduleParams frequency={frequency}의 flowId={flowId}은(는) 흐름 실행을 만드는 데 지원되지 않습니다. 유효한 빈도를 입력하고 다시 시도하십시오. |
| `1387-400` | 잘못된 요청 | flowRunId={flowRunId}이(가) 다시 트리거할 수 없는 상태={state}입니다. 잠시 후 다시 시도해 보고 문제가 지속되면 고객 지원 센터에 문의하십시오. |
| `1388-400` | 잘못된 요청 | 흐름={flow}은(는) state={state}에 있으며 다시 트리거할 수 없습니다. 다시 트리거하려면 흐름이 활성화된 상태여야 합니다. |
| `1389-400` | 잘못된 요청 | 제공된 base64 인코딩 문자열을 구문분석하는 동안 오류가 발생했습니다. 유효한 인코딩 필터 문자열을 입력하고 다시 시도하십시오. |
| `1390-400` | 잘못된 요청 | &#39;not&#39; 연산자는 둘 이상의 비교를 가질 수 없습니다. 유효한 비교 수를 입력하고 다시 시도하십시오. |
| `1391-400` | 잘못된 요청 | Id={sourceConnectionId}에 대해 sourceConnection에서 SchemaMetaData를 구문분석하지 못했습니다. 요청에서 schemaMetaData를 확인하고 다시 시도하십시오. |
| `1392-400` | 잘못된 요청 | flowId={flowId}에 대한 흐름 요청에서 변환을 구문분석하지 못했습니다. 요청의 변환을 확인하고 다시 시도하십시오. |
| `1393-400` | 잘못된 요청 | 입력된 매개변수 {parameter}가 null이거나 비어 있습니다. 유효한 {parameter}를 입력하고 다시 시도하십시오. |
| `1394-400` | 잘못된 요청 | 매개변수 {parameter}에 대한 최소값이 null이거나 비어 있습니다. 유효한 {parameter}를 입력하고 다시 시도하십시오. |
| `1395-400` | 잘못된 요청 | 흐름에서 찾은 소스 연결이 null이거나 비어 있습니다. 흐름에 유효한 소스 연결을 입력하고 다시 시도하십시오. |
| `1396-400` | 잘못된 요청 | 일치하는 포맷을 찾을 수 없습니다. 일치하는 포맷을 입력하고 다시 시도하십시오. |
| `1397-400` | 잘못된 요청 | 입력된 빈도: {frequency}가 유효하지 않습니다. 유효한 빈도를 입력하고 다시 시도해 주십시오. |
| `1398-400` | 잘못된 요청 | 입력된 작업: {action}이(가) 지원되지 않습니다. 입력된 작업을 확인하고 다시 시도하십시오. |
| `1399-400` | 잘못된 요청 | 유효한 requestFileType을 찾을 수 없습니다. 유효한 requestFileType을 입력하고 다시 시도하십시오. |
| `1400-400` | 잘못된 요청 | 입력된 매개변수 &#39;templateType&#39;이 유효하지 않습니다. 유효한 템플릿 유형을 입력하고 다시 시도하십시오. |
| `1401-400` | 잘못된 요청 | 입력된 흐름 실행 액션={flowRunAction}은 지원되지 않습니다. 유효한 흐름 실행 액션을 입력하고 다시 시도하십시오. |
| `1402-500` | 내부 오류 | 내부 오류가 발생했습니다. 다시 시도해 주십시오. 문제가 지속되면 고객 지원 센터에 문의하십시오. |
| `1403-400` | 잘못된 요청 | 시작 시간이 지났고 더 이상 빈도를 한 번으로 변경할 수 없습니다. |
| `1404-400` | 잘못된 요청 | 시작 시간이 지났고 더 이상 다시 채우기를 업데이트할 수 없습니다. |

## 흐름 서비스 예외(1600-1699)

| 오류 코드 | 제목 | 자세한 메시지 |
| --- | --- | --- |
| `1600-400` | 잘못된 요청 | 요청을 처리할 수 없습니다. {detailedMessage} |
| `1601-500` | 내부 오류 | 내부 오류가 발생했습니다. 다시 시도해 주십시오. 문제가 지속되면 고객 지원 센터에 문의하십시오. |
| `1602-404` | 리소스를 찾을 수 없음 | 요청한 리소스를 찾을 수 없습니다. {detailedMessage} |
| `1603-503` | 서비스를 사용할 수 없음 | 서비스를 일시적으로 사용할 수 없습니다. 다시 시도해 주십시오. 문제가 지속되면 고객 지원 센터에 문의하십시오. |
| `1604-504` | 게이트웨이 시간 초과 | 게이트웨이 시간 초과 오류가 발생했습니다. 다시 시도해 주십시오. 문제가 지속되면 고객 지원 센터에 문의하십시오. |
| `1605-401` | 인증되지 않음 | 사용자가 권한이 없습니다. {detailedMessage} |
| `1606-403` | 금지 | 요청한 작업을 사용할 수 없습니다. {detailedMessage} |
| `1607-412` | 사전 조건 오류 | If-Unmodified-Since 또는 If-None-Match 헤더에 의해 정의된 조건이 충족되지 않습니다. {detailedMessage} |

## 데이터 랜딩 영역 오류

| 오류 코드 | 제목 | 자세한 메시지 |
| --- | --- | --- |
| `1700-500` | 내부 오류 | 내부 오류가 발생했습니다. 다시 시도해 주십시오. 문제가 지속되면 고객 지원 센터에 문의하십시오. |
| `1701-400` | 잘못된 요청 | 입력된 랜딩 구역이 비활성 상태입니다. 랜딩 구역을 활성화하고 다시 시도하십시오. |
| `1702-400` | 잘못된 요청 | 랜딩 구역에 입력된 SAS Type={sasType}은(는) 허용되지 않습니다. 유효한 SAS를 입력하고 다시 시도하십시오. |
| `1703-400` | 잘못된 요청 | 자격 증명 새로 고침이 허용되지 않습니다. |
| `1704-400` | 잘못된 요청 | subscriptionId={subscriptionId} 및 resourceGroupName={resourceGroupName}의 storageAccountName={accountName}에 대해 반환된 키의 형식이 잘못되었습니다. 요청을 확인하고 다시 시도하십시오. 문제가 지속되면 고객 지원 센터에 문의하십시오. |
| `1705-400` | 잘못된 요청 | 입력된 데이터 랜딩 구역 액션은 지원되지 않습니다. 유효한 액션을 입력하고 다시 시도하십시오. |
| `1706-400` | 잘못된 요청 | 랜딩 구역={landingZoneType}에 대해 허용된 활성화 구성이 올바르게 구성되지 않았습니다. 다시 시도하고 문제가 지속되면 고객 지원 센터에 문의하십시오. |
| `1707-400` | 잘못된 요청 | 랜딩 구역 구성이 null이거나 비어 있을 수 없기 때문에 서비스를 시작하지 못했습니다. 랜딩 구역 구성이 null이 아닌지 확인하고 다시 시도하십시오. |
| `1708-400` | 잘못된 요청 | 컨테이너 구성은 landingZoneType={landingZoneType}에서 null일 수 없습니다. 컨테이너 구성이 null이 아닌지 확인하고 다시 시도하십시오. |
| `1709-400` | 잘못된 요청 | landingZoneType={landingZoneType}의 {tokenConfig}에 대한 SAS 세부 정보는 null일 수 없습니다. 구성에 유효한 SAS를 입력하고 다시 시도하십시오. |
| `1710-400` | 잘못된 요청 | 입력된 랜딩 구역 유형: {landingZoneUseCase}은(는) 허용되지 않습니다. 유효한 랜딩 구역 유형을 입력하고 다시 시도하십시오. |
| `1711-400` | 잘못된 요청 | 입력된 데이터 랜딩 구역: {landingZoneUseCase}에 대한 SAS 세부 정보를 찾을 수 없습니다. 입력된 랜딩 구역 유형에 대한 SAS 세부 정보가 입력되었는지 확인하십시오. |
| `1712-400` | 잘못된 요청 | 입력된 랜딩 존 액션: {actionType}은(는) 허용되지 않습니다. 유효한 데이터 랜딩 존 액션을 입력하고 다시 시도하십시오. |
| `1713-400` | 잘못된 요청 | 입력된 {tokenType}에는 {OperationType}이(가) 허용되지 않습니다. 요청을 확인하고 다시 시도하십시오. |
| `1714-400` | 잘못된 요청 | clientId={clientId}는 이 작업을 수행할 수 없습니다. 권한이 있는 요청을 확인하고 다시 시도하십시오. |
