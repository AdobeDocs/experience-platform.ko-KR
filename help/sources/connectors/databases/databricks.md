---
title: Azure Databricks
description: Azure Databricks를 Experience Platform에 연결하는 데 필요한 사전 요구 사항에 대해 알아봅니다.
badgeUltimate: label="Ultimate" type="Positive"
badgeBeta: label="Beta" type="Informative"
last-substantial-update: 2025-04-29T00:00:00Z
exl-id: 2f082898-aa0e-47a1-a4bf-077c21afdfee
source-git-commit: 5637a12d5f9cc14b6cf3d88f018aa92de06ab739
workflow-type: tm+mt
source-wordcount: '593'
ht-degree: 2%

---

# [!DNL Azure Databricks]

>[!IMPORTANT]
>
>[!DNL Azure Databricks] 소스는 Real-Time CDP Ultimate을 구매한 사용자가 소스 카탈로그에서 사용할 수 있습니다.

[!DNL Azure Databricks]은(는) 데이터 분석, 머신 러닝 및 AI용으로 설계된 클라우드 기반 플랫폼입니다. [!DNL Databricks]을(를) 사용하여 [!DNL Azure]과(와) 통합하고 규모에 맞게 데이터 솔루션을 구축, 배포 및 관리할 수 있는 포괄적인 환경을 제공할 수 있습니다.

[!DNL Databricks] 원본을 사용하여 계정을 연결하고 [!DNL Databricks] 데이터를 Adobe Experience Platform으로 수집할 수 있습니다.

## 전제 조건

[!DNL Databricks] 계정을 Experience Platform에 성공적으로 연결하기 위한 필수 구성 요소 단계를 완료합니다.

### 컨테이너 자격 증명 가져오기

[!DNL Databricks] 계정이 나중에 액세스할 수 있도록 하려면 Experience Platform [!DNL Azure Blob Storage] 자격 증명을 검색하십시오.

자격 증명을 검색하려면 [!DNL Connectors] API의 `/credentials` 끝점에 대한 GET 요청을 만드십시오.

**API 형식**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source
```

**요청**

다음 요청은 Experience Platform [!DNL Azure Blob Storage]에 대한 자격 증명을 검색합니다.

+++요청 보기 예

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**응답**

성공적인 응답은 나중에 [!DNL Databricks]에 대한 [!DNL Apache Spark] 구성에서 사용할 자격 증명(`containerName`, `SASToken`, `storageAccountName`)을 제공합니다.

+++응답 보기 예

```json
{
    "containerName": "dlz-databricks-container",
    "SASToken": "sv=2020-10-02&si=dlz-b1f4060b-6bbd-4043-9bd9-a5f5be72de30&sr=c&sp=racwdlm&sig=zVQfmuElZJzOKkUk8z5lChrJ3YQUE2h6EShDZOsVeMc%3D",
    "storageAccountName": "sndbxdtlndga8m7ajbvgc64k",
    "SASUri": "https://sndbxdtlndga8m7ajbvgc64k.blob.core.windows.net/dlz-databricks-container?sv=2020-10-02&si=dlz-b1f4060b-6bbd-4043-9bd9-a5f5be72de30&sr=c&sp=racwdlm&sig=zVQfmuElZJzOKkUk8z5lChrJ3YQUE2h6EShDZOsVeMc%3D",
    "expiryDate": "2025-07-05"
}
```

| 속성 | 설명 |
| --- | --- |
| `containerName` | [!DNL Azure Blob Storage] 컨테이너의 이름입니다. 나중에 [!DNL Databricks]에 대한 [!DNL Apache Spark] 구성을 완료할 때 이 값을 사용합니다. |
| `SASToken` | [!DNL Azure Blob Storage]에 대한 공유 액세스 서명 토큰입니다. 이 문자열에는 요청을 승인하는 데 필요한 모든 정보가 포함되어 있습니다. |
| `storageAccountName` | 저장소 계정의 이름입니다. |
| `SASUri` | [!DNL Azure Blob Storage]에 대한 공유 액세스 서명 URI입니다. 이 문자열은 인증 중인 [!DNL Azure Blob Storage]에 대한 URI와 해당 SAS 토큰의 조합입니다. |
| `expiryDate` | SAS 토큰이 만료되는 날짜. 응용 프로그램에서 토큰을 사용하여 [!DNL Azure Blob Storage]에 데이터를 업로드하려면 만료 날짜 전에 토큰을 새로 고쳐야 합니다. 명시된 만료 날짜 이전에 토큰을 수동으로 새로 고치지 않는 경우, GET 자격 증명 호출이 수행될 때 자동으로 새로 고침되고 새 토큰을 제공합니다. |

+++

### 자격 증명 새로 고침

>[!NOTE]
>
>자격 증명을 새로 고치면 기존 자격 증명이 취소됩니다. 따라서 저장소 자격 증명을 새로 고칠 때마다 그에 따라 [!DNL Spark] 구성을 업데이트해야 합니다. 그렇지 않으면 데이터 흐름이 실패합니다.

자격 증명을 새로 고치려면 POST 요청을 만들고 `action=refresh`을(를) 쿼리 매개 변수로 포함하십시오.

**API 형식**

```http
GET /data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source&action=refresh
```

**요청**

다음 요청은 [!DNL Azure Blob Storage]에 대한 자격 증명을 새로 고칩니다.

+++요청 보기 예

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/connectors/landingzone/credentials?type=dlz_databricks_source&action=refresh' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
```

+++

**응답**

성공적인 응답은 새 자격 증명을 반환합니다.

+++응답 보기 예

```json
{
    "containerName": "dlz-databricks-container",
    "SASToken": "sv=2020-10-02&si=dlz-6e17e5d6-de18-4efc-88c7-45f37d242617&sr=c&sp=racwdlm&sig=wvA4K3fcEmqAA%2FPvcMhB%2FA8y8RLwVJ7zhdWbxvT1uFM%3D",
    "storageAccountName": "sndbxdtlndga8m7ajbvgc64k",
    "SASUri": "https://sndbxdtlndga8m7ajbvgc64k.blob.core.windows.net/dlz-databricks-container?sv=2020-10-02&si=dlz-6e17e5d6-de18-4efc-88c7-45f37d242617&sr=c&sp=racwdlm&sig=wvA4K3fcEmqAA%2FPvcMhB%2FA8y8RLwVJ7zhdWbxvT1uFM%3D",
    "expiryDate": "2025-07-20"
}
```

+++

### [!DNL Azure Blob Storage]에 대한 액세스 구성

>[!IMPORTANT]
>
>* 클러스터가 종료된 경우 흐름 실행 중에 서비스가 자동으로 다시 시작됩니다. 그러나 연결이나 데이터 흐름을 만들 때는 클러스터가 활성 상태인지 확인해야 합니다. 또한 데이터 미리 보기 또는 탐색과 같은 작업을 수행하는 경우에는 종료된 클러스터의 자동 재시작을 요청할 수 없으므로 클러스터가 활성 상태여야 합니다.
>
>* [!DNL Azure] 컨테이너에 이름이 `adobe-managed-staging`인 폴더가 있습니다. 데이터를 원활하게 수집하려면 **이 폴더를 수정하지 마십시오**.


다음으로, [!DNL Databricks] 클러스터가 Experience Platform [!DNL Azure Blob Storage] 계정에 액세스할 수 있는지 확인해야 합니다. 이렇게 하면 [!DNL Azure Blob Storage]을(를) [!DNL delta lake] 테이블 데이터를 쓰는 중간 위치로 사용할 수 있습니다.

액세스를 제공하려면 [!DNL Apache Spark] 구성의 일부로 [!DNL Databricks] 클러스터에 SAS 토큰을 구성해야 합니다.

[!DNL Databricks] 인터페이스에서 **[!DNL Advanced options]**&#x200B;을(를) 선택한 다음 [!DNL Spark config] 입력 상자에 다음을 입력합니다.

```shell
fs.azure.sas.{CONTAINER_NAME}.{STORAGE-ACCOUNT}.blob.core.windows.net {SAS-TOKEN}
```

| 속성 | 설명 |
| --- | --- |
| 컨테이너 이름 | 컨테이너의 이름입니다. [!DNL Azure Blob Storage] 자격 증명을 검색하여 이 값을 가져올 수 있습니다. |
| 저장소 계정 | 저장소 계정의 이름입니다. [!DNL Azure Blob Storage] 자격 증명을 검색하여 이 값을 가져올 수 있습니다. |
| SAS 토큰 | [!DNL Azure Blob Storage]에 대한 공유 액세스 서명 토큰입니다. [!DNL Azure Blob Storage] 자격 증명을 검색하여 이 값을 가져올 수 있습니다. |

![Azure의 Databricks UI입니다.](../../images/tutorials/create/databricks/databricks-ui.png)

## API를 사용하여 [!DNL Databricks]을(를) Experience Platform에 연결

전제 조건 단계를 완료했으므로 이제 [API를 사용하여  [!DNL Databricks] 계정을 Experience Platform에 연결](../../tutorials/api/create/databases/databricks.md)에 대한 안내서로 진행할 수 있습니다.
